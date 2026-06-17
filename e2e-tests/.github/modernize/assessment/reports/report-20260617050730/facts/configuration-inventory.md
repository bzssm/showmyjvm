# Configuration & Externalized Settings Inventory

This inventory summarizes configuration sources and runtime settings used by the `e2e-tests` workspace.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| package.json | JavaScript package config | e2e-tests/package.json | Scripts and devDependencies |
| playwright.config.ts | Playwright runtime config | e2e-tests/playwright.config.ts | Base URL, retries, reporter |
| README.md | Human guidance | e2e-tests/README.md | Setup and execution expectations |
| test-all.sh | Shell orchestration | e2e-tests/test-all.sh | Start/wait/test/stop behavior |

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| default npm scripts | Manual (`npm run <script>`) | Run single/all test variants | @playwright/test |

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| local default | Implicit | playwright.config.ts | baseURL=http://localhost:8080 |
| CI mode | `CI` env var | playwright.config.ts | retries=2, workers=1 |

## Properties Inventory

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| use.baseURL | http://localhost:8080 | all | playwright.config.ts |
| reporter | html | all | playwright.config.ts |
| trace | on-first-retry | all | playwright.config.ts |
| retries | 0 | local | playwright.config.ts |
| retries | 2 | CI | playwright.config.ts |
| workers | system default | local | playwright.config.ts |
| workers | 1 | CI | playwright.config.ts |

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---|
| e2e-tests runner | Node.js runtime (no custom flags in repo) | Not specified | 1 process per run |
| target service | External prerequisite on port 8080 | Not specified in e2e-tests | 1 running target required |

## Startup Dependency Chain

1. Target ShowMyJVM implementation starts and binds to port 8080.
2. `npm test` starts Playwright and executes requests against configured base URL.
3. `test-all.sh` repeats this sequence per implementation with port-availability checks.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage (masked) |
|---|---|---|
| None identified | N/A | N/A |

### Secrets Provisioning Workflow

No secrets workflow is defined in the `e2e-tests` workspace. Tests run against localhost using non-secret configuration.

## Feature Flags

| Flag Name | Default | Controlled By |
|---|---|---|
| CI | unset | Environment variable from runner |

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| @playwright/test | ^1.48.0 | e2e-tests/package.json |
| @types/node | ^22.0.0 | e2e-tests/package.json |
| Node.js | 18+ (required) | e2e-tests/README.md |
