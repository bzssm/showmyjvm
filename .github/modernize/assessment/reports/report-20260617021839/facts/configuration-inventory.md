# Configuration & Externalized Settings Inventory

ShowMyJVM uses simple per-module configuration files with a single externalized setting (`PORT`) for each of its nine framework implementations; there are no shared config servers, secret stores, or feature flag systems.

## Configuration Sources

| Source | Type | Path / Location | Notes |
|--------|------|----------------|-------|
| Spring Boot properties | application.properties | spring-boot/src/main/resources/application.properties | server.port, jackson settings |
| Quarkus properties | application.properties | quarkus/src/main/resources/application.properties | HTTP port, Jib container image settings |
| Micronaut YAML | application.yml | micronaut/src/main/resources/application.yml | App name, server port |
| Helidon MP YAML | application.yaml | helidon-mp/src/main/resources/application.yaml | Server port and host |
| Helidon MP MicroProfile | microprofile-config.properties | helidon-mp/src/main/resources/META-INF/microprofile-config.properties | Port, host, metrics toggle |
| Helidon SE logging | logging.properties | helidon/src/main/resources/logging.properties | JUL logging format and levels |
| Helidon MP logging | logging.properties | helidon-mp/src/main/resources/logging.properties | JUL logging format and levels |
| Maven wrapper | maven-wrapper.properties | .mvn/wrapper/maven-wrapper.properties | Maven 3.9.15 distribution URL |
| GitHub Actions CI | maven.yml | .github/workflows/maven.yml | Java 25 (Microsoft distribution), Maven verify |
| Inline port config | Java source | javalin, ratpack, sparkjava, helidon | PORT env var read directly in main() |
| Tomcat Maven profile | pom.xml | tomcat/pom.xml | port-from-env Maven profile for PORT env var |
| Test YAML | application-test.yaml | helidon/src/test/resources, helidon-mp/src/test/resources | Test-specific configuration overrides |

No external config servers, Vault, Azure Key Vault, AWS Secrets Manager, Spring Cloud Config, or Consul KV stores are used.

## Build Profiles

Only one Maven build profile is present across all modules:

| Profile | Module | Activation | Purpose | Key Changes |
|---------|--------|-----------|---------|------------|
| `port-from-env` | tomcat | Auto (when `env.PORT` system property is set) | Propagates `PORT` env var to the embedded Tomcat port | Sets `<tomcat.port>${env.PORT}</tomcat.port>` |

No other Maven build profiles (`dev`, `prod`, `cloud`, etc.) exist in the project. The Spring Boot, Quarkus, Micronaut, Helidon, Javalin, Ratpack, and SparkJava modules do not define any Maven build profiles — they use expression syntax (`${PORT:8080}`) or inline code for port resolution.

## Runtime Profiles

No runtime profiles are defined. No `application-dev.properties`, `application-prod.yml`, or Spring `@Profile` annotations are present. All configuration is single-profile.

| Profile | Module | Activation | Config Files | Key Overrides |
|---------|--------|-----------|-------------|--------------|
| (default only) | spring-boot | Always active | application.properties | server.port = ${PORT:8080} |
| (default only) | quarkus | Always active | application.properties | quarkus.http.port = ${PORT:8080} |
| (default only) | micronaut | Always active | application.yml | micronaut.server.port = ${PORT:8080} |
| (default only) | helidon-mp | Always active | application.yaml | server.port = ${PORT:8080} |
| (default only) | helidon SE, javalin, ratpack, sparkjava | Always active | Java source (inline) | PORT env var read in main() |
| application-test | helidon, helidon-mp | Test execution | application-test.yaml | Test server settings |

## Properties Inventory

### Spring Boot (`spring-boot/src/main/resources/application.properties`)

| Property Key | Default | Source |
|-------------|---------|--------|
| server.port | 8080 | `${PORT:8080}` env var |
| spring.jackson.serialization.indent_output | true | Hardcoded |

### Quarkus (`quarkus/src/main/resources/application.properties`)

| Property Key | Default | Source |
|-------------|---------|--------|
| quarkus.http.host | 0.0.0.0 | Hardcoded |
| quarkus.http.port | 8080 | `${PORT:8080}` env var |
| quarkus.container-image.build | true | Hardcoded |
| quarkus.container-image.push | false | Hardcoded |
| quarkus.container-image.group | (empty) | Hardcoded |
| quarkus.container-image.name | showmyjvm-quarkus | Hardcoded |
| quarkus.container-image.tag | latest | Hardcoded |
| quarkus.container-image.registry | (empty) | Hardcoded |
| quarkus.jib.base-jvm-image | mcr.microsoft.com/openjdk/jdk:25-ubuntu | Hardcoded |

### Micronaut (`micronaut/src/main/resources/application.yml`)

| Property Key | Default | Source |
|-------------|---------|--------|
| micronaut.application.name | showmyjvm-micronaut | Hardcoded |
| micronaut.server.port | 8080 | `${PORT:8080}` env var |

### Helidon MP (`helidon-mp/src/main/resources/application.yaml`)

| Property Key | Default | Source |
|-------------|---------|--------|
| server.port | 8080 | `${PORT:8080}` env var |
| server.host | 0.0.0.0 | Hardcoded |

### Helidon MP MicroProfile (`helidon-mp/src/main/resources/META-INF/microprofile-config.properties`)

| Property Key | Default | Source |
|-------------|---------|--------|
| server.port | 8080 | Hardcoded |
| server.host | 0.0.0.0 | Hardcoded |
| metrics.rest-request.enabled | false | Hardcoded |
| app.greeting | Hello | Hardcoded |

### Tomcat (`tomcat/pom.xml`)

| Property Key | Default | Source |
|-------------|---------|--------|
| tomcat.port | 8080 | Hardcoded; overridden by `port-from-env` Maven profile |
| cargo.servlet.port | ${tomcat.port} | Resolves to tomcat.port |

### Javalin, Ratpack, SparkJava, Helidon SE

Port is read inline via `System.getenv("PORT")` with a fallback of `8080`. No external config files are used.

## Startup Parameters & Resource Requirements

No JVM heap flags, `-D` system properties, Docker Compose memory limits, or Kubernetes resource limits are specified in the project. Each service starts with default JVM settings.

| Service | JVM Options | Memory Limit | Instance Config |
|---------|------------|-------------|----------------|
| All framework modules | None specified | None specified | Single instance |
| Tomcat | `-Djava.security.egd=file:/dev/./urandom` (Jib container) | None specified | Single instance |

The Jib plugin for all modules uses `mcr.microsoft.com/openjdk/jdk:25-ubuntu` (Quarkus explicit; others default) as the base image. No `-Xms`/`-Xmx` heap settings are configured.

## Startup Dependency Chain

Each service starts independently with no dependencies on other services. There are no shared infrastructure components (no config server, no discovery server, no database) that must be available before application startup.

| Service | Startup Dependencies | Wait Mechanism |
|---------|---------------------|---------------|
| All framework modules | None | None |

Services are individually runnable: `PORT=8080 mvn spring-boot:run -pl spring-boot` starts the Spring Boot module immediately.

## Secrets & Sensitive Configuration

No secrets are configured in this project. There are no database passwords, API keys, or connection strings with credentials in any configuration file. The only sensitive-adjacent configuration is the `PORT` environment variable, which is not a secret.

| Secret Reference | Type | Storage |
|-----------------|------|---------|
| None | N/A | N/A |

### Secrets Provisioning Workflow

No secrets provisioning workflow exists. The application requires no credentials at runtime. The only external configuration required is the `PORT` environment variable to change the listening port.

> **Risk Note**: As documented in `data-architecture.md`, the API endpoints return all environment variables in responses. If secret values are injected as environment variables in a deployment environment (e.g., database passwords, API keys), those values would be exposed in the API response. No filtering, masking, or authentication controls are present.

## Feature Flags

No feature flag frameworks, `@ConditionalOnProperty` annotations, LaunchDarkly, Unleash, or custom feature toggles are present in this project. The single Helidon MP property `metrics.rest-request.enabled=false` is the closest to a feature toggle.

| Flag Name | Default | Controlled By | Notes |
|-----------|---------|--------------|-------|
| metrics.rest-request.enabled | false | microprofile-config.properties | Disables MicroProfile REST request metrics |

## Framework & Runtime Versions

| Component | Version | Source |
|-----------|---------|--------|
| Java / OpenJDK | 25 | bom/pom.xml `maven.compiler.release=25` |
| Maven | 3.9.15 | .mvn/wrapper/maven-wrapper.properties |
| Spring Boot | 4.0.0 | spring-boot/pom.xml |
| Spring Boot Maven Plugin | 4.0.0 | spring-boot/pom.xml |
| Quarkus Platform | 3.30.3 | quarkus/pom.xml |
| Micronaut Platform | 4.8.3 | micronaut/pom.xml |
| Micronaut Core | 4.7.1 | micronaut/pom.xml |
| Micronaut Validation | 4.11.0 | micronaut/pom.xml |
| Helidon (SE and MP) | 4.3.2 | helidon-mp/pom.xml |
| Javalin | 6.7.0 | javalin/pom.xml |
| Jackson Databind (Javalin) | 2.20.1 | javalin/pom.xml |
| Ratpack Core | 1.10.0-milestone-39 | ratpack/pom.xml |
| SparkJava | 2.9.4 | sparkjava/pom.xml |
| Jackson Databind (SparkJava) | 2.15.2 | sparkjava/pom.xml |
| Jakarta Servlet API | 6.1.0 | tomcat/pom.xml |
| Jakarta JSON Bind API | 3.0.1 | tomcat/pom.xml |
| Yasson | 3.0.4 | tomcat/pom.xml |
| Cargo Maven3 Plugin (Tomcat) | 1.10.19 | tomcat/pom.xml |
| Jib Maven Plugin | 3.5.1 | bom/pom.xml |
| JUnit Jupiter | 5.11.4 | bom/pom.xml |
| Mockito Core | 5.20.0 | bom/pom.xml |
| SLF4J Simple | 2.0.16 | bom/pom.xml |
| Container Base Image | mcr.microsoft.com/openjdk/jdk:25-ubuntu | quarkus/pom.xml (explicit); others use Jib default |
| GitHub Actions Java | 25 (microsoft distribution) | .github/workflows/maven.yml |
