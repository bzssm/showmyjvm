# Configuration & Externalized Settings Inventory

Configuration is primarily file-based per framework module with a consistent `PORT` override pattern and Maven-driven build configuration in the BOM and module POM files.

## Configuration Sources

| Source | Type | Path/Location | Notes |
| --- | --- | --- | --- |
| Maven parent and module POM files | Build and dependency config | `pom.xml`, `bom/pom.xml`, `*/pom.xml` | Defines modules, Java 25 release, and framework dependencies |
| Spring Boot properties | Runtime properties | `spring-boot/src/main/resources/application.properties` | Includes `server.port=${PORT:8080}` |
| Quarkus properties | Runtime properties | `quarkus/src/main/resources/application.properties` | Includes HTTP host/port and container-image settings |
| Micronaut YAML | Runtime properties | `micronaut/src/main/resources/application.yml` | Includes `micronaut.server.port=${PORT:8080}` |
| Helidon MP YAML | Runtime properties | `helidon-mp/src/main/resources/application.yaml` | Includes server host and port |
| Environment variable lookups in code | Runtime source | `javalin`, `ratpack`, `sparkjava`, `helidon` main classes | Uses `System.getenv("PORT")` fallback to 8080 |

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
| --- | --- | --- | --- |
| default Maven build | standard `mvn` lifecycle | Build all modules | maven-compiler-plugin release 25, surefire, enforcer |
| module-specific run goals | manual per module command | Run a selected adapter | spring-boot-maven-plugin, quarkus plugin, exec plugin, cargo plugin |
| container image packaging | package phase plugin config | Build container images | jib-maven-plugin in BOM/module configuration |

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
| --- | --- | --- | --- |
| default | implicit | module `application.properties/yml` | default port 8080 |
| environment override | `PORT` environment variable | module runtime config and code | replaces default listening port |

## Properties Inventory

| Property Key | Default | Profiles | Source |
| --- | --- | --- | --- |
| `server.port` | `8080` | default and overridden by `PORT` | spring-boot, helidon-mp config |
| `quarkus.http.port` | `8080` | default and overridden by `PORT` | quarkus config |
| `quarkus.http.host` | `0.0.0.0` | default | quarkus config |
| `micronaut.server.port` | `8080` | default and overridden by `PORT` | micronaut config |
| `spring.jackson.serialization.indent_output` | `true` | default | spring-boot config |

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
| --- | --- | --- | --- |
| all modules | Java runtime defaults (no explicit `-Xms/-Xmx` in repo) | not specified | not specified |

## Startup Dependency Chain

1. A selected framework adapter starts and binds to configured port.
2. Adapter initializes route handlers for `/jvm/inspect` and `/jvm/inspect.json`.
3. Requests invoke core library classes to collect JVM telemetry at runtime.

No inter-service startup wait chain or external dependency readiness checks are configured.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage (masked) |
| --- | --- | --- |
| none identified | n/a | n/a |

### Secrets Provisioning Workflow

No secret store integration or credential injection workflow was identified in repository configuration. Runtime behavior appears to rely on non-secret environment values such as `PORT`.

## Feature Flags

| Flag Name | Default | Controlled By |
| --- | --- | --- |
| none identified | n/a | n/a |

## Framework & Runtime Versions

| Component | Version | Source |
| --- | --- | --- |
| Java release target | 25 | BOM and core module POM |
| Spring Boot dependencies/plugin | 4.0.0 | `spring-boot/pom.xml` |
| Maven compiler plugin | 3.14.1 | `bom/pom.xml` |
| Jib Maven plugin | 3.5.1 | `bom/pom.xml` |
| JUnit Jupiter | 5.11.4 to 5.14.1 | BOM and core POM |
