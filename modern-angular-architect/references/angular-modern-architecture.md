# Angular Modern Architecture Reference

This file gives the architectural defaults for this skill when a repo is ambiguous or greenfield-like.

## 1. Baseline principles

Prefer these principles in order:

1. Follow the repository’s existing conventions where they are coherent.
2. Organize by feature or domain boundary.
3. Keep closely related files together.
4. Extract to shared/core only when reuse or app-wide scope is real.
5. Prefer incremental fit over ideological rewrites.

## 2. Modern Angular signals to recognize

### Standalone-first is the modern default
For new Angular code, prefer standalone components and standalone routing patterns.

Typical indicators:
- `bootstrapApplication(...)`
- `provideRouter(...)`
- components imported directly in `imports`
- absence of feature NgModules for new code

If the repo is module-based, do not force a migration unless requested.

### Routing
Expect routing to be defined in route arrays and provided through router providers or equivalent app config.

Common modern shapes:
- `src/app/app.routes.ts`
- feature route files like `src/app/features/orders/orders.routes.ts`
- lazy feature entrypoints via route-level imports

### Reactivity
Prefer:
- `signal()` for local state
- `computed()` for derived state
- `effect()` only for syncing with imperative external APIs

Do not propose `effect()` for ordinary derived state.

### Dependency injection
Prefer clear provider placement:
- app-wide providers only at app/core level
- route-scoped providers when feature-local scope is appropriate
- component-local providers only when the lifetime truly belongs to the component subtree

## 3. Recommended folder logic

These are heuristics, not rigid rules.

### Feature-owned code
Prefer feature folders such as:

`src/app/features/<feature>/`

Inside a feature, common subareas can include:

- `pages/` or `containers/` for route entry components
- `components/` for feature-local presentational or composite UI
- `data-access/` for API-facing services and repository-style abstractions
- `models/` for feature-local types
- `guards/`, `resolvers/`, `directives/`, `pipes/` when feature-owned
- `store/` or `state/` only if the repo already uses explicit local state organization
- `testing/` only if the repo already centralizes feature test helpers there

Do not introduce every subfolder automatically. Only create what the feature needs.

### Shared
Use shared only for things that are genuinely reused across multiple features:

`src/app/shared/`

Examples:
- reusable UI primitives
- common pipes/directives
- broadly reusable utilities tied to UI concerns

Do not move feature-specific widgets into shared just because they are “components”.

### Core
Use core only for app-wide or infrastructure concerns:

`src/app/core/`

Examples:
- auth session orchestration
- HTTP interceptors
- app-shell-wide services
- global configuration wiring
- global navigation if truly app-level

Do not use core as a miscellaneous dumping ground.

## 4. Greenfield fallback

If the repo is nearly empty, a pragmatic baseline is:

- `src/main.ts`
- `src/app/app.ts` or `src/app/app.component.ts` depending on repo style
- `src/app/app.routes.ts`
- `src/app/core/`
- `src/app/shared/`
- `src/app/features/<feature>/`

Inside each feature:
- route file
- page/shell component
- local components
- data-access service if needed
- local models/types
- colocated tests

## 5. File naming and locality

Prefer:
- hyphenated file names
- matching file names for TS/template/styles
- `.spec.ts` next to the code under test
- one main concept per file

Avoid:
- generic names like `helpers.ts`, `common.ts`, `utils.ts` unless truly shared and well-scoped
- giant cross-feature type buckets
- global `components/`, `services/`, `directives/` topologies in greenfield planning

## 6. Mixed legacy repos

If the repo mixes standalone and NgModules:
- identify the active pattern used by the nearest analogous feature;
- plan consistently with that area of the codebase;
- mention a modern alternative only as a note, not as the primary plan.

## 7. Forms guidance

Do not recommend signal forms by default for production planning because they are experimental.
Use existing form patterns in the repo first.

## 8. Performance-aware planning

When adding a routed feature, check whether it should be lazy loaded.
When adding reusable UI, keep imports narrow and colocated.
Avoid creating app-wide singletons for feature-local behavior.

## 9. What this skill should validate

Before finalizing a plan, verify:
- feature cohesion
- routing entrypoint clarity
- data-access boundary clarity
- absence of feature leakage into shared/core
- consistency with naming and folder patterns
- tests or validation points are identified