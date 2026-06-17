# Assessment Overview

This document provides navigation to all supplementary architectural analysis documents generated for the ShowMyJVM assessment. Each document explores a specific dimension of the application's structure, dependencies, and configuration.

## Supplementary Documents

| Document | Description |
|----------|-------------|
| [Architecture Diagram](./architecture-diagram.md) | Two-layer architecture visualization: high-level application architecture (9 framework modules + core library) and detailed component relationship diagram showing how each framework module delegates to the shared core library |
| [Dependency Map](./dependency-map.md) | Visual map of all external dependencies grouped by functional category (web frameworks, serialization, observability, logging, utilities) across all 9 framework modules, including version compatibility risk analysis |
| [API & Service Contracts](./api-service-contracts.md) | Catalog of all HTTP endpoints (`/jvm/inspect`, `/jvm/inspect.json`) across all 9 framework implementations, including service catalog, management/observability endpoints, DTOs, communication patterns, and security posture |
| [Data Architecture](./data-architecture.md) | In-memory data model documentation (JVMDetails, MemoryPoolDetails, JVMFlag) with ER diagram, data extraction methods acting as the data access layer, and data classification/sensitivity analysis |
| [Configuration Inventory](./configuration-inventory.md) | Comprehensive inventory of all configuration sources, properties, framework versions, build profiles, startup parameters, and secrets workflow across all modules |
| [Business Workflows](./business-workflows.md) | End-to-end documentation of the two core workflows (plain-text and JSON JVM inspection), domain entities, decision logic (GC detection, flag retrieval fallback, port selection), and cross-cutting concerns |
