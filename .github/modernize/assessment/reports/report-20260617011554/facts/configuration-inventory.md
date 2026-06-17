# Configuration & Externalized Settings Inventory

ShowMyJVM uses minimal, per-module configuration spread across five framework-specific files — all sharing a single externalized setting (`PORT`) and no secret stores, config servers, or complex profile hierarchies.

## Configuration Sources

| Source | Type | Path / Location | Notes |
|--------|------|----------------|-------|
| spring-boot application.properties | Spring Boot properties | `spring-boot/src/main/resources/application.properties` | Port and Jackson settings |
| quarkus application.properties | Quarkus properties | `quarkus/src/main/resources/application.properties` | Port, host, and Jib container image settings |
| micronaut application.yml | Micronaut YAML | `micronaut/src/main/resources/application.yml` | App name and port |
| helidon application.yaml | Helidon SE YAML | `helidon-mp/src/main/resources/application.yaml` | Server port and host |
| helidon-mp microprofile-config.properties | MicroProfile Config | `helidon-mp/src/main/resources/META-INF/microprofile-config.properties` | Port, host, greeting, metrics REST flag |
| helidon logging.properties | JUL logging | `helidon/src/main/resources/logging.properties` | Console handler, log format, global level INFO |
| helidon-mp logging.properties | JUL logging | `helidon-mp/src/main/resources/logging.properties` | Console handler, log format, Weld (org.jboss) set to WARNING |
| helidon-mp native-image.properties | GraalVM native image | `helidon-mp/src/main/resources/META-INF/native-image/.../native-image.properties` | `--initialize-at-build-time` for native compilation |
| helidon-mp test microprofile-config.properties | MicroProfile Config (test) | `helidon-mp/src/test/resources/META-INF/microprofile-config.properties` | Empty — uses runtime defaults |
| aspire appsettings.json | .NET Aspire AppHost | `aspire/appsettings.json` | Log levels for Microsoft.AspNetCore and Aspire.Hosting.Dcp |
| aspire appsettings.Development.json | .NET Aspire Dev | `aspire/appsettings.Development.json` | Log level overrides for development |
| Maven wrapper properties | Maven toolchain | `.mvn/wrapper/maven-wrapper.properties` | Pins Maven version for the wrapper |

No Spring Cloud Config Server, Consul KV, Azure App Configuration, AWS AppConfig, HashiCorp Vault, or any external configuration repository is used.

## Build Profiles

| Profile | Activation | Purpose | Key Plugins / Dependencies Added |
|---------|-----------|---------|----------------------------------|
| (default — no profiles) | Automatic | Standard compile, test, package | maven-compiler-plugin (Java 25), maven-surefire-plugin |
| Jib container build | Manual (`mvn package`) | Builds OCI container image via Jib | `jib-maven-plugin 3.5.1` (configured in BOM, executed at `package` phase) |
| Quarkus container image | Quarkus build | Builds Quarkus Jib container image | `quarkus-container-image-jib` extension; outputs `showmyjvm-quarkus:latest` |
| Cargo run (tomcat) | `mvn cargo:run` | Runs WAR in embedded Tomcat via Cargo | `cargo-maven3-plugin 1.10.19` |

No Maven `<profiles>` sections were found in any `pom.xml`; the project uses a single default build configuration with optional Jib/Cargo goals invoked manually.

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---------|------------------|-------------|--------------|
| (default — no profiles) | All modules start with a single profile | Module-specific `application.*` files | Port via `PORT` environment variable |
| helidon-mp test | Maven Surefire test execution | `src/test/resources/META-INF/microprofile-config.properties`, `application-test.yaml` | Overrides server port for test isolation |

No Spring `application-{profile}.properties`, Quarkus `%prod`/`%dev`/`%test` profile blocks, or Micronaut environment-specific files are used. Each framework module has a single runtime configuration file.

## Properties Inventory

### spring-boot

| Property Key | Default Value | Source |
|-------------|--------------|--------|
| `server.port` | `${PORT:8080}` | `application.properties` — reads `PORT` env var, falls back to 8080 |
| `spring.jackson.serialization.indent_output` | `true` | `application.properties` — pretty-prints JSON responses |

### quarkus

| Property Key | Default Value | Source |
|-------------|--------------|--------|
| `quarkus.http.host` | `0.0.0.0` | `application.properties` — binds to all interfaces |
| `quarkus.http.port` | `${PORT:8080}` | `application.properties` — reads `PORT` env var |
| `quarkus.container-image.build` | `true` | `application.properties` — builds image during package |
| `quarkus.container-image.push` | `false` | `application.properties` — does not push image |
| `quarkus.container-image.name` | `showmyjvm-quarkus` | `application.properties` |
| `quarkus.container-image.tag` | `latest` | `application.properties` |
| `quarkus.container-image.registry` | _(empty)_ | `application.properties` — local Docker only |
| `quarkus.jib.base-jvm-image` | `mcr.microsoft.com/openjdk/jdk:25-ubuntu` | `application.properties` — MS OpenJDK 25 base |

### micronaut

| Property Key | Default Value | Source |
|-------------|--------------|--------|
| `micronaut.application.name` | `showmyjvm-micronaut` | `application.yml` |
| `micronaut.server.port` | `${PORT:8080}` | `application.yml` — reads `PORT` env var |

### helidon SE

| Property Key | Default Value | Source |
|-------------|--------------|--------|
| `server.port` | `${PORT:8080}` | Inline in `Main.java` (reads `System.getenv("PORT")`) |

### helidon-mp (MicroProfile Config)

| Property Key | Default Value | Source |
|-------------|--------------|--------|
| `server.port` | `8080` | `META-INF/microprofile-config.properties` |
| `server.host` | `0.0.0.0` | `META-INF/microprofile-config.properties` |
| `metrics.rest-request.enabled` | `false` | `META-INF/microprofile-config.properties` — disables per-request metrics |
| `app.greeting` | `Hello` | `META-INF/microprofile-config.properties` — unused in current endpoints |
| `server.port` | `${PORT:8080}` | `application.yaml` — reads `PORT` env var |
| `server.host` | `0.0.0.0` | `application.yaml` |

### javalin / ratpack / sparkjava / tomcat

No configuration files — port is read directly in code:
```java
int port = System.getenv("PORT") != null ? Integer.parseInt(System.getenv("PORT")) : 8080;
```

### aspire (AppHost)

| Property Key | Default Value | Source |
|-------------|--------------|--------|
| `Logging:LogLevel:Default` | `Information` | `appsettings.json` |
| `Logging:LogLevel:Microsoft.AspNetCore` | `Warning` | `appsettings.json` |
| `Logging:LogLevel:Aspire.Hosting.Dcp` | `Warning` | `appsettings.json` |

## Startup Parameters & Resource Requirements

| Service | Launch Command | JVM / Runtime Options | Memory | Port |
|---------|---------------|----------------------|--------|------|
| spring-boot | `mvn spring-boot:run` | Standard JVM defaults | Unspecified | `PORT` env var (default 8080) |
| quarkus | `mvn quarkus:run` | Standard JVM defaults | Unspecified | `PORT` env var (default 8080) |
| micronaut | `mvn mn:run` | Standard JVM defaults | Unspecified | `PORT` env var (default 8080) |
| helidon | `mvn exec:exec` | Standard JVM defaults | Unspecified | `PORT` env var (default 8080) |
| helidon-mp | `mvn exec:exec` | `--initialize-at-build-time` (native only) | Unspecified | `PORT` env var (default 8080) |
| javalin | `mvn exec:exec` | Standard JVM defaults | Unspecified | `PORT` env var (default 8080) |
| ratpack | `mvn exec:exec` | Standard JVM defaults | Unspecified | `PORT` env var (default 8080) |
| sparkjava | `mvn exec:exec` | Standard JVM defaults | Unspecified | `PORT` env var (default 8080) |
| tomcat | `mvn cargo:run` | Standard JVM defaults | Unspecified | `PORT` env var (default 8080) |
| aspire (containers) | `dotnet run` (AppHost) | N/A (.NET 9) | Unspecified | Container port 8090 → target 8080 (Tomcat) |

No explicit `-Xms`/`-Xmx` heap settings, `-D` system property overrides, or Kubernetes/Docker resource limits are specified. Each service inherits default JVM memory sizing.

## Startup Dependency Chain

All nine Java services are **independently startable** with no inter-service dependencies. They do not depend on each other, a config server, a discovery server, or a database.

| Service | Waits For | Mechanism | Notes |
|---------|----------|-----------|-------|
| Any Java service | Nothing | N/A | Starts immediately; only dependency is the JVM itself |
| aspire AppHost | Docker daemon | .NET Aspire container orchestration | Pulls / uses pre-built `showmyjvm-tomcat:latest` container image |

No Docker Compose `depends_on`, Kubernetes readiness probes, `dockerize` wait-for-TCP, or Spring Cloud Config retry loops are present.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage | Notes |
|-----------------|------|---------|-------|
| _(none)_ | — | — | No passwords, API keys, or connection strings are configured |

No database credentials, messaging broker passwords, OAuth client secrets, Azure KeyVault URIs, AWS Secrets Manager paths, or encrypted property values exist in any configuration file.

### Secrets Provisioning Workflow

No secrets provisioning workflow exists — the application requires no external credentials to operate. The only externalized setting is `PORT`, which is a non-sensitive integer. If a future deployment environment requires restricting access to the JVM inspection endpoints (which currently expose all environment variables and system properties), secrets should be injected via environment variables from the orchestration platform (Kubernetes Secrets, Azure App Configuration, GitHub Actions secrets) rather than stored in configuration files.

## Feature Flags

| Flag / Property | Default | Controlled By | Notes |
|----------------|---------|--------------|-------|
| `metrics.rest-request.enabled` | `false` | `helidon-mp/META-INF/microprofile-config.properties` | Enables per-request REST metrics in Helidon MP when `true` |

No feature flag framework (LaunchDarkly, Unleash, Spring Feature Flags, .NET FeatureManagement) is used. The single flag above is a framework configuration knob, not a product feature toggle. No `@ConditionalOnProperty` beans or A/B testing configuration is present.

## Framework & Runtime Versions

| Component | Version | Source |
|-----------|---------|--------|
| Java / OpenJDK | 25 | `bom/pom.xml` (`maven.compiler.release=25`) |
| Maven | 3.9.1+ | `pom.xml` enforcer rule; wrapper in `.mvn/wrapper/maven-wrapper.properties` |
| Spring Boot | 4.0.0 | `spring-boot/pom.xml` BOM import |
| Quarkus | 3.30.3 | `quarkus/pom.xml` (`quarkus.platform.version`) |
| Micronaut Platform | 4.8.3 | `micronaut/pom.xml` BOM import |
| Helidon | 4.3.2 | `helidon/pom.xml` and `helidon-mp/pom.xml` BOM import |
| Javalin | 6.7.0 | `javalin/pom.xml` |
| Ratpack | 1.10.0-milestone-39 | `ratpack/pom.xml` |
| SparkJava | 2.9.4 | `sparkjava/pom.xml` |
| Jakarta Servlet API | 6.1.0 | `tomcat/pom.xml` |
| Jackson Databind | 2.20.1 / 2.15.2 | `javalin/pom.xml` (2.20.1), `sparkjava/pom.xml` (2.15.2) |
| Logback Classic | 1.5.21 | `micronaut/pom.xml` |
| SLF4J Simple | 2.0.16 | BOM (`bom/pom.xml`) |
| Micronaut Maven Plugin | 4.11.4 | `micronaut/pom.xml` |
| Jib Maven Plugin | 3.5.1 | BOM (`bom/pom.xml`) |
| Cargo Maven3 Plugin | 1.10.19 | `tomcat/pom.xml` |
| JUnit Jupiter | 5.11.4 | BOM (`bom/pom.xml`) |
| Mockito | 5.20.0 | BOM (`bom/pom.xml`) |
| .NET | 9.0 | `aspire/showmyjvm.csproj` (`TargetFramework=net9.0`) |
| .NET Aspire AppHost SDK | 9.5.2 | `aspire/showmyjvm.csproj` |
| Playwright (`@playwright/test`) | ^1.48.0 | `e2e-tests/package.json` |
| Docker base image | `mcr.microsoft.com/openjdk/jdk:25-ubuntu` | BOM `container.base.image` property |
