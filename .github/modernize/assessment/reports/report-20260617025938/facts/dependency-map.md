# Dependency Map

ShowMyJVM is a Maven multi-module Java project with framework-adapter dependencies around a shared core library; dependencies are primarily web runtimes, observability libraries, and logging utilities.

## Dependencies

```mermaid
flowchart LR
    App["ShowMyJVM"]

    subgraph Web["Web Frameworks"]
        SpringWeb["spring-boot-starter-web 4.0.0 managed"]
        QuarkusRest["quarkus-rest-jackson BOM managed"]
        MicronautHttp["micronaut-http-server-netty BOM managed"]
        HelidonWeb["helidon-webserver BOM managed"]
        JavalinLib["javalin"]
        RatpackCore["ratpack-core"]
        SparkCore["spark-core"]
        ServletApi["jakarta.servlet-api"]
    end

    subgraph Obs["Observability"]
        SpringActuator["spring-boot-starter-actuator"]
        HelidonHealth["helidon health and metrics"]
    end

    subgraph Logging["Logging"]
        Slf4jApi["slf4j-api 2.0.17"]
        Slf4jSimple["slf4j-simple 2.x"]
    end

    subgraph Utils["Utilities"]
        Jackson["jackson-databind and annotations"]
        JsonBind["jakarta.json.bind-api"]
        Yasson["org.eclipse yasson"]
    end

    subgraph Bom["Version Management"]
        ProjectBom["showmyjvm-bom 1.0.0-SNAPSHOT"]
        SpringBom["spring-boot-dependencies 4.0.0"]
        QuarkusBom["quarkus-bom"]
        MicronautBom["micronaut-platform"]
        HelidonBom["helidon-dependencies"]
    end

    App -->|"web"| Web
    App -->|"observability"| Obs
    App -->|"logging"| Logging
    App -->|"utilities"| Utils
    App -->|"managed by"| Bom
    ProjectBom -.->|"manages shared plugins and Java 25"| App
```

### Dependency Summary

| Category | Count | Key Libraries | Notes |
| --- | --- | --- | --- |
| Web Frameworks | 8 | Spring Boot Web, Quarkus REST, Micronaut HTTP, Helidon Web, Javalin, Ratpack, SparkJava, Servlet API | One adapter module per framework |
| Observability | 2 | Spring Actuator, Helidon health and metrics | Health and metrics features are framework-specific |
| Logging | 2 | slf4j-api, slf4j-simple | Core uses SLF4J abstraction |
| Utilities | 3 | Jackson, JSON-B API, Yasson | Serialization support across adapters |
| Version Management | 5 | showmyjvm BOM plus framework BOMs | Centralized dependency version alignment |

### Version & Compatibility Risks

The project targets Java 25 and uses framework BOM-managed dependencies; environments without JDK 25 fail compilation. Mixed framework families increase operational surface area even though the business capability is the same.

### Notable Observations

- The shared `showmyjvm-core` library avoids duplicated JVM-inspection logic across all adapters.
- Most modules are intentionally thin and rely on framework starter bundles instead of deep custom dependency trees.
- Test dependencies are mostly JUnit 5 and framework test harnesses, isolated by module.

## Test Dependencies

| Framework | Version | Notes |
| --- | --- | --- |
| JUnit Jupiter | 5.11.4 to 5.14.1 | Standard unit-testing framework across modules |
| Mockito Core | 5.20.0 | Present in BOM for mocking |
| Helidon testing JUnit5 | BOM managed | Used in helidon modules |
| Hamcrest | BOM managed | Assertion helpers in helidon tests |

Total test-scope dependencies: 4

Test infrastructure is present for unit and module-level tests; end-to-end coverage is implemented separately in the Playwright `e2e-tests` project.
