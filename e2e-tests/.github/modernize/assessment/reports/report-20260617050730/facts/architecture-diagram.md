# Architecture Diagram

This document summarizes the e2e-tests subproject architecture and its main component relationships.

## Application Architecture

```mermaid
flowchart TD
    subgraph Client["Client Layer"]
        Runner["Playwright Runner"]
    end
    subgraph App["Application Layer - Node.js + Playwright"]
        Config["playwright.config.ts"]
        Specs["showmyjvm.spec.ts"]
        Script["test-all.sh"]
    end
    subgraph Target["Target System"]
        Endpoint1["GET /jvm/inspect"]
        Endpoint2["GET /jvm/inspect.json"]
    end

    Runner -->|"loads config"| Config
    Runner -->|"executes"| Specs
    Script -->|"runs"| Runner
    Specs -->|"HTTP request"| Endpoint1
    Specs -->|"HTTP request"| Endpoint2
```

### Technology Stack Summary

| Layer | Technology | Version | Purpose |
|---|---|---|---|
| Client | Playwright test runner | ^1.48.0 | Execute browser/API end-to-end tests |
| Application | Node.js scripts | Node 18+ (required) | Host and run test commands |
| Test Logic | TypeScript tests | Local project source | Validate ShowMyJVM endpoint behavior |

### Data Storage & External Services

This subproject does not maintain its own database. It interacts with a running ShowMyJVM service at `http://localhost:8080` and validates endpoint behavior over HTTP.

### Key Architectural Decisions

- Configuration is centralized in `playwright.config.ts` with a fixed base URL and retry behavior.
- Tests use API request context directly rather than browser UI flows.
- `test-all.sh` orchestrates multi-implementation validation by starting/stopping framework apps around the same test suite.

## Component Relationships

```mermaid
flowchart LR
    subgraph Presentation
        Cmd["npm test"]
    end
    subgraph Business["Business Logic"]
        Suite["showmyjvm.spec.ts"]
    end
    subgraph DataAccess["Data Access"]
        Req["Playwright request context"]
    end
    subgraph Infra["Infrastructure"]
        Cfg["playwright.config.ts"]
        Orchestrator["test-all.sh"]
        TargetSvc["ShowMyJVM service"]
    end

    Cmd -->|"starts"| Suite
    Suite -->|"uses"| Req
    Req -->|"baseURL from"| Cfg
    Req -->|"calls"| TargetSvc
    Orchestrator -.->|"invokes"| Cmd
```

### Component Inventory

| Component | Layer | Type | Responsibility |
|---|---|---|---|
| npm test | Presentation | Command | Entry-point for the E2E suite |
| showmyjvm.spec.ts | Business Logic | Test spec | Validates endpoint status, headers, and payload shape |
| Playwright request context | Data Access | HTTP client abstraction | Sends requests to running target service |
| playwright.config.ts | Infrastructure | Configuration file | Defines base URL, retries, and project settings |
| test-all.sh | Infrastructure | Shell orchestrator | Runs tests across multiple implementations |
