# Configuration & Externalized Settings Inventory

ShowMyJVM uses framework-native configuration files across nine independent modules, all with minimal settings focused on port binding. There are no external config servers, secret stores, or feature flag frameworks.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|--------|------|---------------|-------|
| Spring Boot application.properties | Properties file | `spring-boot/src/main/resources/application.properties` | Server port, Jackson settings |
| Quarkus application.properties | Properties file | `quarkus/src/main/resources/application.properties` | HTTP host/port, Jib image config |
| Micronaut application.yml | YAML file | `micronaut/src/main/resources/application.yml` | Application name, server port |
| Helidon SE logging.properties | JUL properties | `helidon/src/main/resources/logging.properties` | Java Util Logging config |
| Helidon SE native-image.properties | Native image hints | `helidon/src/main/resources/META-INF/native-image/.../native-image.properties` | GraalVM build-time init |
| Helidon MP application.yaml | YAML file | `helidon-mp/src/main/resources/application.yaml` | Server port and host |
| Helidon MP microprofile-config.properties | MicroProfile config | `helidon-mp/src/main/resources/META-INF/microprofile-config.properties` | MP server port, metrics, app greeting |
| Helidon MP logging.properties | JUL properties | `helidon-mp/src/main/resources/logging.properties` | Logging levels and format |
| Helidon MP native-image.properties | Native image hints | `helidon-mp/src/main/resources/META-INF/native-image/.../native-image.properties` | GraalVM build-time init |
| Helidon SE test application-test.yaml | YAML file | `helidon/src/test/resources/application-test.yaml` | Test-time overrides |
| Helidon MP test application-test.yaml | YAML file | `helidon-mp/src/test/resources/application-test.yaml` | Security disabled for tests |
| Helidon MP test microprofile-config.properties | MicroProfile config | `helidon-mp/src/test/resources/META-INF/microprofile-config.properties` | Empty; test config override |
| .NET Aspire appsettings.json | JSON | `aspire/appsettings.json` | Logging levels for Aspire host |
| .NET Aspire appsettings.Development.json | JSON | `aspire/appsettings.Development.json` | Development logging overrides |
| .NET Aspire .aspire/settings.json | JSON | `aspire/.aspire/settings.json` | Aspire dashboard settings |
| Aspire AppHost.cs | C# / IaC | `aspire/AppHost.cs` | Container orchestration declarations |
| Maven BOM pom.xml | Build config | `bom/pom.xml` | All dependency and plugin versions |
| Root pom.xml | Build config | `pom.xml` | Module list, enforcer rules |
| Per-module pom.xml (×9) | Build config | `{module}/pom.xml` | Framework BOMs, exec plugin config |

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies / Plugins |
|---------|-----------|---------|---------------------------|
| `port-from-env` (tomcat only) | Auto — activated when system property `env.PORT` is set | Maps `$PORT` environment variable to Cargo's `tomcat.port` property | None added; sets `tomcat.port` property |
| Default (all modules) | Always active | Standard compile, test, package, and containerize cycle | Maven Compiler Plugin (release=25), Maven Surefire, Jib Plugin |

No Maven profiles exist in the BOM, root POM, or most framework modules. Profile usage is minimal and confined to the Tomcat module's port-forwarding workaround.

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---------|------------------|-------------|---------------|
| Default (all frameworks) | Always active | `application.properties` / `application.yml` / `microprofile-config.properties` | `PORT` env var overrides server port |
| `test` (Helidon SE/MP) | Maven Surefire test execution | `application-test.yaml` | Helidon MP: `security.enabled=false` |

No Spring `@Profile` annotations, `SPRING_PROFILES_ACTIVE` settings, or `application-{profile}.yml` files exist. Each module has a single default configuration with the option to override the port via environment variable.

## Properties Inventory

### Spring Boot (`spring-boot/src/main/resources/application.properties`)

| Property Key | Default | Source |
|-------------|---------|--------|
| `server.port` | `8080` | Env var `${PORT:8080}` |
| `spring.jackson.serialization.indent_output` | `true` | Static value |

### Quarkus (`quarkus/src/main/resources/application.properties`)

| Property Key | Default | Source |
|-------------|---------|--------|
| `quarkus.http.host` | `0.0.0.0` | Static value |
| `quarkus.http.port` | `8080` | Env var `${PORT:8080}` |
| `quarkus.container-image.build` | `true` | Static value |
| `quarkus.container-image.push` | `false` | Static value |
| `quarkus.container-image.group` | `` (empty) | Static value |
| `quarkus.container-image.name` | `showmyjvm-quarkus` | Static value |
| `quarkus.container-image.tag` | `latest` | Static value |
| `quarkus.container-image.registry` | `` (empty) | Static value |
| `quarkus.jib.base-jvm-image` | `mcr.microsoft.com/openjdk/jdk:25-ubuntu` | Static value |

### Micronaut (`micronaut/src/main/resources/application.yml`)

| Property Key | Default | Source |
|-------------|---------|--------|
| `micronaut.application.name` | `showmyjvm-micronaut` | Static value |
| `micronaut.server.port` | `8080` | Env var `${PORT:8080}` |

### Helidon MP (`helidon-mp/src/main/resources/application.yaml`)

| Property Key | Default | Source |
|-------------|---------|--------|
| `server.port` | `8080` | Env var `${PORT:8080}` |
| `server.host` | `0.0.0.0` | Static value |

### Helidon MP MicroProfile (`helidon-mp/src/main/resources/META-INF/microprofile-config.properties`)

| Property Key | Default | Source |
|-------------|---------|--------|
| `server.port` | `8080` | Static value |
| `server.host` | `0.0.0.0` | Static value |
| `metrics.rest-request.enabled` | `false` | Static value |
| `app.greeting` | `Hello` | Static value |

### Helidon MP Test (`helidon-mp/src/test/resources/application-test.yaml`)

| Property Key | Default | Source |
|-------------|---------|--------|
| `security.enabled` | `false` | Static value |

## Startup Parameters & Resource Requirements

| Service | JVM / Runtime Options | Memory | Instance Count |
|---------|----------------------|--------|----------------|
| Spring Boot | None specified — uses framework defaults | Not specified | 1 |
| Quarkus | None specified | Not specified | 1 |
| Micronaut | None specified | Not specified | 1 |
| Helidon SE | `--module-path` configured by exec plugin | Not specified | 1 |
| Helidon MP | `--module-path` configured by exec plugin | Not specified | 1 |
| Javalin | None specified | Not specified | 1 |
| Ratpack | None specified | Not specified | 1 |
| SparkJava | None specified | Not specified | 1 |
| Tomcat | Cargo plugin manages JVM startup | Not specified | 1 |

No `-Xms`/`-Xmx` heap settings, Docker resource limits, or Kubernetes resource requests/limits are defined in any configuration file. All heap sizing is left to JVM ergonomics.

## Startup Dependency Chain

All nine services are fully independent — there is no startup dependency chain. Each service:

1. Starts its embedded HTTP server (or Cargo for Tomcat)
2. Binds to `PORT` (default 8080)
3. Is immediately ready to serve requests

No `dockerize`, Kubernetes readiness probes, Spring Cloud Config retry, or Docker Compose `depends_on` dependencies are configured. The Aspire host (`aspire/AppHost.cs`) adds a container for Tomcat mapped to port 8090, but there is no health-check wait mechanism defined.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage |
|-----------------|------|---------|
| None detected | — | — |

No database passwords, API keys, tokens, OAuth2 client secrets, or other sensitive configuration values are present in any configuration file. The tool makes no outbound connections and requires no credentials.

### Secrets Provisioning Workflow

No secrets provisioning is required. All nine services are read-only JVM introspection tools that make no authenticated calls to external systems. The only configuration inputs are the `PORT` environment variable (non-sensitive) and internal JMX access (always available within the same JVM process).

**Note**: While no secrets are stored in configuration files, the `/jvm/inspect.json` endpoint returns all system properties and environment variables at runtime. If the application is deployed in an environment where secrets are injected as environment variables (common cloud practice), those secrets would be exposed via this endpoint. No masking or filtering is configured. This is a runtime data exposure risk, not a configuration file risk.

## Feature Flags

| Flag Name | Default | Controlled By |
|-----------|---------|---------------|
| `metrics.rest-request.enabled` | `false` | Helidon MP microprofile-config.properties |
| `security.enabled` (test profile) | `false` (tests only) | Helidon MP application-test.yaml |
| `quarkus.container-image.build` | `true` | Quarkus application.properties |
| `quarkus.container-image.push` | `false` | Quarkus application.properties |

No feature flag framework (LaunchDarkly, Unleash, Spring Feature Flags) is used. The closest approximation is the Helidon MP `metrics.rest-request.enabled` property and Quarkus container-image build flags, which are simple boolean configuration toggles.

## Framework & Runtime Versions

| Component | Version | Source |
|-----------|---------|--------|
| Java / OpenJDK | 25 | `bom/pom.xml` (`maven.compiler.release=25`) |
| Maven (minimum) | 3.9.1 | `pom.xml` (enforcer rule) |
| Spring Boot | 4.0.0 | `spring-boot/pom.xml` |
| Quarkus | 3.30.3 | `quarkus/pom.xml` |
| Micronaut Platform | 4.8.3 | `micronaut/pom.xml` |
| Micronaut Core | 4.7.1 | `micronaut/pom.xml` |
| Helidon (SE + MP) | 4.3.2 | `helidon/pom.xml`, `helidon-mp/pom.xml` |
| Javalin | 6.7.0 | `javalin/pom.xml` |
| Ratpack | 1.10.0-milestone-39 | `ratpack/pom.xml` |
| SparkJava | 2.9.4 | `sparkjava/pom.xml` |
| Jakarta Servlet API | 6.1.0 | `tomcat/pom.xml` |
| Jackson Databind | 2.20.1 (javalin), 2.15.2 (sparkjava) | `javalin/pom.xml`, `sparkjava/pom.xml` |
| SLF4J API | 2.0.17 | `core/pom.xml` |
| Logback Classic | 1.5.21 | `micronaut/pom.xml` |
| JUnit Jupiter | 5.14.1 (core), 5.11.4 (BOM) | `core/pom.xml`, `bom/pom.xml` |
| Mockito Core | 5.20.0 | `bom/pom.xml` |
| Jib Maven Plugin | 3.5.1 | `bom/pom.xml` |
| .NET Aspire host | (latest SDK) | `aspire/showmyjvm.csproj` |
| Quarkus Jib base image | `mcr.microsoft.com/openjdk/jdk:25-ubuntu` | `quarkus/src/main/resources/application.properties` |
| Playwright (E2E) | See `e2e-tests/package.json` | `e2e-tests/package.json` |
