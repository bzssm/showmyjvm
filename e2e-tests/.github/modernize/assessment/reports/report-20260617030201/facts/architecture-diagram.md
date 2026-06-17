# Architecture Diagram

This document summarizes the E2E test application architecture for the `e2e-tests` workspace and the component relationships used to validate ShowMyJVM endpoints.

## Application Architecture

```mermaid
flowchart TD
    subgraph Client["Client Layer"]
        Runner["Playwright Runner"]
    end

    subgraph App["Application Layer - Node.js + Playwright"]
        Config["playwright.config.ts"]
        Specs["tests/showmyjvm.spec.ts"]
    end

    subgraph Target["Target Application"]
        Api["ShowMyJVM endpoint on localhost:8080"]
    end

    subgraph Output["Output Layer"]
        HtmlReport["Playwright HTML Report"]
        TraceZip["Playwright Trace Artifacts"]
    end

    Runner -->|"loads config"| Config
    Runner -->|"executes"| Specs
    Specs -->|"GET /jvm/inspect and /jvm/inspect.json"| Api
    Runner -->|"writes results"| HtmlReport
    Runner -->|"stores traces on retry"| TraceZip
```

### Technology Stack Summary

| Layer | Technology | Version | Purpose |
|---|---|---|---|
| Test Runner | Playwright Test | ^1.48.0 | Browser/API-driven end-to-end test execution |
| Runtime | Node.js | 22.22.3 (runtime) | Executes the test toolchain |
| Language Tooling | TypeScript typings | @types/node ^22.0.0 | Type support for test config and scripts |
| Target Integration | HTTP over localhost | N/A | Validates ShowMyJVM endpoints |

### Data Storage & External Services

The E2E test workspace does not define its own database, cache, or message broker. It depends on an externally started ShowMyJVM server running on `http://localhost:8080` and records local test artifacts (HTML report and traces) in the workspace.

### Key Architectural Decisions

- Tests are black-box endpoint checks against a running implementation, not in-process unit tests.
- Base URL is centralized in `playwright.config.ts` to keep endpoint targeting consistent.
- A single Playwright project (`showmyjvm`) is used for uniform validation across implementations.

## Component Relationships

```mermaid
flowchart LR
    subgraph Presentation
        CLI["npm test"]
    end

    subgraph Business["Business Logic"]
        Runner["Playwright Test Runner"]
        Spec["showmyjvm.spec.ts"]
    end

    subgraph DataAccess["Data Access"]
        Http["Playwright APIRequestContext"]
    end

    subgraph Infra["Infrastructure"]
        Config["playwright.config.ts"]
        Target["ShowMyJVM Server :8080"]
        Reporter["HTML Reporter"]
    end

    CLI -->|"starts"| Runner
    Runner -->|"reads"| Config
    Runner -->|"runs"| Spec
    Spec -->|"uses"| Http
    Http -->|"HTTP requests"| Target
    Runner -->|"publishes results"| Reporter
```

### Component Inventory

| Component | Layer | Type | Responsibility |
|---|---|---|---|
| npm test | Presentation | CLI entrypoint | Starts Playwright test execution |
| Playwright Test Runner | Business Logic | Test orchestrator | Runs suites, retries, and reporting |
| showmyjvm.spec.ts | Business Logic | Test specification | Validates endpoint availability and content |
| APIRequestContext | Data Access | HTTP client API | Sends requests to `/jvm/inspect*` endpoints |
| playwright.config.ts | Infrastructure | Configuration | Defines base URL, workers, retry policy |
| ShowMyJVM Server :8080 | Infrastructure | External dependency | Provides endpoints under test |
| HTML Reporter | Infrastructure | Report output | Produces human-readable test run reports |
