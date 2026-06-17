# Configuration & Externalized Settings Inventory

This workspace has a compact configuration landscape centered on Playwright test execution. Configuration is sourced mainly from package scripts and Playwright config.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| package.json | Node package config | e2e-tests/package.json | Defines scripts and dev dependencies |
| package-lock.json | Dependency lock file | e2e-tests/package-lock.json | Pins resolved npm dependency graph |
| playwright.config.ts | Test runtime config | e2e-tests/playwright.config.ts | Defines baseURL, retries, workers, reporter |
| README.md | Operational docs | e2e-tests/README.md | Documents prerequisite server on port 8080 |

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| default npm scripts | Manual (`npm run <script>`) | Selects test mode (default, UI, headed, impl-specific) | @playwright/test |

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| local default | `npm test` | playwright.config.ts | baseURL `http://localhost:8080`, retry policy CI-aware |
| CI mode | `CI=true npm test` | playwright.config.ts | retries=2, workers=1 |

## Properties Inventory

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| use.baseURL | http://localhost:8080 | local default, CI mode | playwright.config.ts |
| fullyParallel | true | local default, CI mode | playwright.config.ts |
| retries | 0 (local), 2 (CI) | local default, CI mode | playwright.config.ts |
| workers | undefined (local), 1 (CI) | local default, CI mode | playwright.config.ts |
| reporter | html | local default, CI mode | playwright.config.ts |
| use.trace | on-first-retry | local default, CI mode | playwright.config.ts |

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---:|
| Playwright test runner | Node.js process, no explicit runtime flags | Not explicitly configured | 1 |
| Target ShowMyJVM service | External prerequisite on port 8080 | Not defined in this workspace | 1 expected |

## Startup Dependency Chain

1. Target ShowMyJVM implementation starts and listens on port 8080.
2. `npm test` starts Playwright runner.
3. Playwright executes tests that call target endpoints.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage (masked) |
|---|---|---|
| None detected | N/A | N/A |

### Secrets Provisioning Workflow

No secrets provisioning workflow is defined in this workspace.

## Feature Flags

| Flag Name | Default | Controlled By |
|---|---|---|
| CI | unset/false | Environment variable |

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| Node.js runtime | 22.22.3 (observed) | local command output |
| npm | 10.9.8 (observed) | local command output |
| @playwright/test | ^1.48.0 | package.json |
| @types/node | ^22.0.0 | package.json |
