# Configuration & Externalized Settings Inventory

ShowMyJVM uses a small but diverse configuration surface: each framework module externalizes its listening port, a few modules expose management settings, and the .NET Aspire companion adds development-time launch and dashboard configuration. There is no centralized config server or secret store in the repository.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| Spring Boot properties | Application properties | `spring-boot/src/main/resources/application.properties` | Sets server port from `PORT` and enables indented JSON |
| Quarkus properties | Application properties | `quarkus/src/main/resources/application.properties` | Sets host, port, and container-image options |
| Micronaut YAML | Application config | `micronaut/src/main/resources/application.yml` | Sets application name and port from `PORT` |
| Helidon MP config | YAML and MicroProfile properties | `helidon-mp/src/main/resources/application.yaml`, `helidon-mp/src/main/resources/META-INF/microprofile-config.properties` | Defines host, port, greeting, and metrics toggle |
| Aspire app settings | .NET JSON config | `aspire/appsettings.json`, `aspire/appsettings.Development.json` | Controls host logging verbosity |
| Aspire launch settings | Development runtime profile | `aspire/Properties/launchSettings.json` | Supplies development URLs and dashboard endpoint environment variables |
| Maven parent and BOM | Build-time config | `pom.xml`, `bom/pom.xml` | Defines modules, Java release 25, plugin versions, and base container image |
| Environment variables | Runtime externalization | `PORT`, `ASPNETCORE_ENVIRONMENT`, `DOTNET_ENVIRONMENT`, Aspire dashboard URLs | Primary override mechanism across modules |

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| Maven multi-module build | Default | Builds the Java modules listed in the root `pom.xml` | Maven compiler, surefire, enforcer, Jib, Quarkus, Spring Boot plugins |
| .NET Debug | `dotnet build` default | Local developer build for the Aspire host | `Aspire.AppHost.Sdk`, `Aspire.Hosting.AppHost` |
| .NET Release | Explicit configuration | Production-style build of the Aspire host | Same package set with Release compilation settings |
| Quarkus build goals | Maven plugin execution | Generates code and packages Quarkus | `quarkus-maven-plugin` |
| Spring Boot repackage | Maven package phase | Produces executable Spring Boot archive | `spring-boot-maven-plugin` |

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| Default Java runtime | Start any Java module | Framework-specific config file plus environment | `PORT` defaults to 8080 when unset |
| Aspire Development http | `dotnet run` with `http` launch profile | `aspire/Properties/launchSettings.json` | `ASPNETCORE_ENVIRONMENT=Development`, local HTTP dashboard URLs |
| Aspire Development https | `dotnet run` with `https` launch profile | `aspire/Properties/launchSettings.json` | Same development environment with HTTPS URLs |
| Helidon MP metrics toggle | Property value | `microprofile-config.properties` | `metrics.rest-request.enabled=false` by default |

## Properties Inventory

### spring-boot

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `server.port` | `8080` via `${PORT:8080}` | Default | Application properties and environment |
| `spring.jackson.serialization.indent_output` | `true` | Default | Application properties |

### quarkus

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `quarkus.http.host` | `0.0.0.0` | Default | Application properties |
| `quarkus.http.port` | `8080` via `${PORT:8080}` | Default | Application properties and environment |
| `quarkus.container-image.name` | `showmyjvm-quarkus` | Default | Application properties |
| `quarkus.jib.base-jvm-image` | `mcr.microsoft.com/openjdk/jdk:25-ubuntu` | Default | Application properties |

### micronaut

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `micronaut.application.name` | `showmyjvm-micronaut` | Default | Application YAML |
| `micronaut.server.port` | `8080` via `${PORT:8080}` | Default | Application YAML and environment |

### helidon-mp

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `server.port` | `8080` or `${PORT:8080}` | Default | YAML and MicroProfile properties |
| `server.host` | `0.0.0.0` | Default | YAML and MicroProfile properties |
| `metrics.rest-request.enabled` | `false` | Default | MicroProfile properties |
| `app.greeting` | `Hello` | Default | MicroProfile properties |

### aspire apphost

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| `Logging:LogLevel:Default` | `Information` | Default | `appsettings.json` |
| `Logging:LogLevel:Microsoft.AspNetCore` | `Warning` | Default | `appsettings.json` |
| `ASPNETCORE_ENVIRONMENT` | `Development` | `http`, `https` | Launch settings |
| `DOTNET_ENVIRONMENT` | `Development` | `http`, `https` | Launch settings |

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---|
| Java framework modules | No explicit JVM flags in repo; server port comes from `PORT` | No fixed memory settings declared | Single process per module by default |
| tomcat container | Container exposes internal port 8080 | No memory limits declared | Single container in Aspire example |
| aspire apphost | Launch profile URLs plus development environment variables | No explicit resource settings declared | Single host process |

## Startup Dependency Chain

1. `aspire apphost` → starts the local distributed application host and then launches the referenced `tomcat` container image.
2. Each Java framework module can otherwise start independently; no module waits on another module, database, or config service.
3. Readiness is implicit in each framework server binding to its configured HTTP port; no custom wait-for scripts or probe configuration were found in repository sources.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage (masked) |
|---|---|---|
| `UserSecretsId` in `aspire/showmyjvm.csproj` | Development secret-store identifier | Local .NET user secrets store, value is an identifier not a secret payload |
| Aspire dashboard endpoint URLs | Development environment variables | Launch settings JSON |

### Secrets Provisioning Workflow

The repository does not contain concrete secrets or an automated secret-provisioning pipeline. The only secret-related hook is the .NET `UserSecretsId`, which indicates the Aspire host can read developer-local secrets from the standard user-secrets store. Java modules rely on plain environment-variable overrides such as `PORT` and do not reference Key Vault, Vault, or other managed secret stores.

## Feature Flags

| Flag Name | Default | Controlled By |
|---|---|---|
| `metrics.rest-request.enabled` | `false` | Helidon MP MicroProfile properties |

## Framework & Runtime Versions

| Component | Version | Source |
|---|---:|---|
| Java target runtime | 25 | `bom/pom.xml`, module POMs |
| Maven minimum version | 3.9.1 | Root `pom.xml` |
| Spring Boot | 4.0.0 | `spring-boot/pom.xml` |
| Quarkus | 3.30.3 | `quarkus/pom.xml` |
| Micronaut platform | 4.8.3 | `micronaut/pom.xml` |
| Helidon | 4.3.2 | `helidon/pom.xml`, `helidon-mp/pom.xml` |
| Javalin | 6.7.0 | `javalin/pom.xml` |
| Ratpack | 1.10.0-milestone-39 | `ratpack/pom.xml` |
| SparkJava | 2.9.4 | `sparkjava/pom.xml` |
| Jakarta Servlet API | 6.1.0 | `tomcat/pom.xml` |
| Aspire AppHost | 9.5.2 / net9.0 | `aspire/showmyjvm.csproj` |
| Jib base image | `mcr.microsoft.com/openjdk/jdk:25-ubuntu` | `bom/pom.xml`, Quarkus properties |
