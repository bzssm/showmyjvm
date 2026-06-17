# Configuration & Externalized Settings Inventory

The `showmyjvm-e2e-tests` project has a minimal configuration surface: **2 configuration files** (`playwright.config.ts` and `tsconfig.json`) with no environment profiles, no secrets, and no externalized properties beyond the single `baseURL` setting.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| `playwright.config.ts` | TypeScript config | `e2e-tests/playwright.config.ts` | Primary Playwright runtime configuration — base URL, retries, parallelism, reporter |
| `tsconfig.json` | TypeScript compiler config | `e2e-tests/tsconfig.json` | TypeScript compilation options — target, module, strict mode |
| `package.json` | npm manifest | `e2e-tests/package.json` | Declares devDependencies and npm scripts |
| `.gitignore` | VCS ignore rules | `e2e-tests/.gitignore` | Excludes `node_modules/`, `playwright-report/`, `test-results/` |
| Environment variables | Runtime env | Process environment | `CI` (boolean) controls retry count and worker count |

No `.env` files, external config servers, secret stores, Spring Cloud Config references, or Kubernetes ConfigMaps are present.

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| Default (dev) | Implicit — no profile system | Local developer test run; parallel workers, zero retries | `@playwright/test` dev dependency |
| CI mode | `process.env.CI` truthy | Serialized workers (1), 2 retries, `forbidOnly` | Same dependencies; behavior changes at runtime, not build time |

This project has no Maven/Gradle/webpack build profiles. The only "profile-like" branching is the `CI` environment variable check in `playwright.config.ts`, which is a runtime distinction, not a build-time one.

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| Local / dev | Default (no env var) | `playwright.config.ts` | `workers: undefined` (max), `retries: 0`, `forbidOnly: false` |
| CI | `CI=true` environment variable | `playwright.config.ts` | `workers: 1`, `retries: 2`, `forbidOnly: true` |

No `.env.development` / `.env.production` files exist. The two modes differ only in the three properties listed above.

## Properties Inventory

### playwright.config.ts

| Property Key | Default | CI Override | Source |
|---|---|---|---|
| `testDir` | `./tests` | — | Hardcoded |
| `fullyParallel` | `true` | — | Hardcoded |
| `forbidOnly` | `false` | `true` | `!!process.env.CI` |
| `retries` | `0` | `2` | `process.env.CI ? 2 : 0` |
| `workers` | `undefined` (Playwright default) | `1` | `process.env.CI ? 1 : undefined` |
| `reporter` | `html` | — | Hardcoded |
| `use.baseURL` | `http://localhost:8080` | — | Hardcoded |
| `use.trace` | `on-first-retry` | — | Hardcoded |
| `projects[0].name` | `showmyjvm` | — | Hardcoded |
| `projects[0].use` | `devices['Desktop Chrome']` | — | Hardcoded |

### tsconfig.json

| Property Key | Default | Notes |
|---|---|---|
| `compilerOptions.target` | `ES2020` | ECMAScript output target |
| `compilerOptions.module` | `commonjs` | Module system |
| `compilerOptions.lib` | `["ES2020"]` | Type library set |
| `compilerOptions.moduleResolution` | `node` | Module resolution strategy |
| `compilerOptions.esModuleInterop` | `true` | CommonJS/ESM interop |
| `compilerOptions.forceConsistentCasingInFileNames` | `true` | Portability guard |
| `compilerOptions.strict` | `true` | Enables all strict type checks |
| `compilerOptions.skipLibCheck` | `true` | Skip type checks on `.d.ts` files |

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---|
| Playwright Test Runner | Node.js 22.x, no explicit flags | Not specified | 1 process (test runner) |
| ShowMyJVM App (under test) | Framework-specific (see framework modules) | Not specified here | 1 per test run |

No `-Xms`/`-Xmx` settings, no Docker resource limits, and no Kubernetes `resources.requests/limits` are configured for the test runner itself.

## Startup Dependency Chain

```
[ShowMyJVM Framework App] must be running on :8080
            ↓  (manual or via test-all.sh)
[Playwright Test Runner] starts and reads playwright.config.ts
            ↓
[Test execution] → HTTP GET http://localhost:8080/jvm/inspect
                → HTTP GET http://localhost:8080/jvm/inspect.json
```

There is no automated wait-for-service mechanism built into the Playwright configuration. The `test-all.sh` script in the parent repository handles the start/stop lifecycle — it starts each framework implementation, waits briefly for readiness, runs the tests, then stops the process. No `dockerize`, Kubernetes readiness probes, or health-check polling are configured.

## Secrets & Sensitive Configuration

No secrets, credentials, API keys, database passwords, or sensitive configuration entries are present in this project. The only externalized value is the target `baseURL` (`http://localhost:8080`), which is not sensitive.

| Secret Reference | Type | Storage |
|---|---|---|
| None | N/A | N/A |

### Secrets Provisioning Workflow

No secrets provisioning workflow is required. This project performs unauthenticated HTTP GET requests to a local development endpoint. There are no service principals, managed identities, Key Vault references, or encrypted property values.

## Feature Flags

No feature flag frameworks (LaunchDarkly, Unleash, Spring Feature Flags, .NET FeatureManagement, or custom toggles) are present in this project.

| Flag Name | Default | Controlled By |
|---|---|---|
| `CI` (implicit) | `false` | `process.env.CI` environment variable — not a feature flag framework, but the only conditional behavior switch |

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| Node.js | 22.x (tested with 22.22.3) | Runtime environment |
| npm | 10.x | Runtime environment |
| TypeScript | Via `@playwright/test` (no explicit `typescript` dep) | Transitive |
| @playwright/test | ^1.48.0 (installed 1.57.0) | `package.json` devDependencies |
| playwright | 1.57.0 (transitive) | `package-lock.json` |
| playwright-core | 1.57.0 (transitive) | `package-lock.json` |
| @types/node | ^22.0.0 (installed 22.19.2) | `package.json` devDependencies |
| ECMAScript target | ES2020 | `tsconfig.json` |
