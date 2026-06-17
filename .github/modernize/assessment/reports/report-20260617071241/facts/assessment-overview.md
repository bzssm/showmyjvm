# Assessment Overview

This document serves as the navigation entry point for the supplementary assessment documentation generated for the ShowMyJVM project (report ID: `20260617071241`).

## Supplementary Documents

### [Architecture Diagram](./architecture-diagram.md)
Visualizes the application's two-layer architecture: a high-level flowchart showing how the nine web framework modules relate to the shared core library and JVM runtime, and a component-level diagram tracing how HTTP handlers delegate to the core introspection classes. Includes a technology stack summary table and key architectural decisions.

### [Dependency Map](./dependency-map.md)
Catalogs all external library dependencies across the nine framework modules, grouped by functional category (Web Frameworks, Observability, Serialization, Logging, Containerization). Highlights version inconsistencies (dual Jackson versions), SparkJava EOL risk, and Ratpack milestone-only availability. Includes a test dependency summary.

### [API & Service Communication Contracts](./api-service-contracts.md)
Documents the two standardized HTTP endpoints exposed by every framework implementation (`GET /jvm/inspect` and `GET /jvm/inspect.json`), the management/observability endpoints (Spring Boot Actuator, Helidon MP Health/Metrics/OpenAPI), the `JVMDetails` response DTO, and the communication patterns. Explicitly notes that no authentication, authorization, or TLS is configured.

### [Data Architecture](./data-architecture.md)
Documents the in-memory-only data model — there is no persistent database, ORM, or caching layer. Describes the `JVMDetails` object graph (including `MemoryPoolDetails`, `JVMFlag`, and `GCType`) and highlights the key sensitivity concern: `systemProperties` and `environmentVariables` fields are returned verbatim in API responses with no masking.

### [Configuration Inventory](./configuration-inventory.md)
Inventories all configuration files across the nine modules (Spring Boot `application.properties`, Quarkus `application.properties`, Micronaut `application.yml`, Helidon SE/MP logging and MicroProfile config files, .NET Aspire `appsettings.json`). Documents the single Maven build profile (`port-from-env` in the Tomcat module), framework versions, and confirms no secrets are stored in configuration files.

### [Business Workflows](./business-workflows.md)
Describes the two primary workflows (text and JSON JVM inspection), the domain entity model (JVMDetails aggregate), and the business rules governing data collection — including graceful degradation when HotSpot-specific APIs are unavailable and the deliberate full-exposure of environment variables. Includes a Mermaid sequence diagram of the end-to-end inspection flow.
