# Assessment Overview

This directory contains supplementary architecture and workflow documents generated as part of the ShowMyJVM application assessment. Use the links below to navigate to each document.

## Supplementary Documents

| Document | Description |
|----------|-------------|
| [Architecture Diagram](architecture-diagram.md) | Two-layer visualization of the application architecture: a high-level diagram showing the nine framework modules, the core library, and the .NET Aspire orchestration host; plus a component relationship diagram showing how controllers, handlers, and core classes interact. |
| [Dependency Map](dependency-map.md) | Visual map of all external dependencies grouped by category (Web Frameworks, Serialization, Observability, Logging, Containerization). Includes version and compatibility risk analysis for all nine Java modules and the Node.js e2e test suite. |
| [API & Service Contracts](api-service-contracts.md) | Catalog of all exposed HTTP endpoints (`/jvm/inspect` and `/jvm/inspect.json`) across all nine service implementations, management/observability endpoints, the `JVMDetails` DTO contract, communication patterns, and a sequence diagram of the request flow. |
| [Data Architecture](data-architecture.md) | Documents the in-memory runtime data model (JVMDetails, MemoryPoolDetails, JVMFlag, GCType) sourced from JMX MBeans. Covers the absence of a persistent data store, key data-collection methods, and a data sensitivity analysis highlighting the verbatim exposure of environment variables. |
| [Configuration Inventory](configuration-inventory.md) | Comprehensive inventory of all configuration files, properties, and environment variables across all modules. Documents the single externalized setting (`PORT`), framework versions, startup parameters, and the absence of secrets or feature flags. |
| [Business Workflows](business-workflows.md) | End-to-end documentation of the two primary business workflows (plain-text and JSON JVM inspection), GC identification and flag-access degradation rules, routing decision logic, and a sequence diagram of the full inspection flow. |
