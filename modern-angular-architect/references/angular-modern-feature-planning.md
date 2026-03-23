# Angular Modern Feature Planning Guide

Use this file to convert a user request into a concrete file plan.

## 1. Classify the request

First classify the requested change.

Common classes:

### Routed feature
Examples:
- orders page
- admin dashboard
- settings area
- notifications center

Usually implies:
- route config
- page or shell component
- feature-local UI
- data-access service(s)
- model/types
- tests

### Reusable UI component
Examples:
- table, modal, badge, filter bar

Usually implies:
- component file(s)
- template/styles if separate
- spec file
- possible location in feature or shared depending on reuse

### API integration
Examples:
- fetch orders
- integrate billing endpoint

Usually implies:
- data-access service
- request/response mapping
- model or DTO boundary
- error/loading handling
- tests

### Stateful workflow
Examples:
- multi-step wizard
- cart flow
- optimistic updates

Usually implies:
- page/container
- several components
- orchestration state
- data-access
- route guards or resolvers if needed
- integration tests or stronger validation

### Auth/permissions concern
Examples:
- role-based route protection
- login session feature

Usually implies:
- route guard or access logic
- auth service or session boundary
- interceptors or provider config if app-wide
- careful core vs feature placement analysis

## 2. Decide where the code belongs

Use this decision order:

1. Is there an existing analogous feature? Mirror it.
2. Is the code only used by one feature? Keep it inside that feature.
3. Is the code reused by several features? Consider shared.
4. Is it app-wide infrastructure? Consider core.
5. Is it a route entry concern? Keep it near routing.

## 3. Typical planning shapes

### New routed feature in a modern standalone repo

Possible plan:
- `src/app/features/orders/orders.routes.ts`
- `src/app/features/orders/pages/orders-page/orders-page.ts`
- `src/app/features/orders/components/order-list/order-list.ts`
- `src/app/features/orders/data-access/orders-api.service.ts`
- `src/app/features/orders/models/order.ts`
- colocated spec files

### Add a feature-local reusable component
Keep it in the feature until real cross-feature reuse exists:
- `src/app/features/orders/components/order-status-badge/order-status-badge.ts`

Only promote later if reuse becomes real.

### Add a cross-cutting interceptor or app-wide auth concern
Potential location:
- `src/app/core/http/...`
- `src/app/core/auth/...`

But only if the concern truly spans the app.

## 4. Plan output expectations

For each path, specify:
- `path`
- `status`: new or modify
- `responsibility`
- `reason`

Example:

- `src/app/features/orders/orders.routes.ts` — new — route entry for the orders feature — belongs with the feature boundary and keeps routing local to the feature.
- `src/app/features/orders/pages/orders-page/orders-page.ts` — new — shell/page component — owns orchestration for the routed screen.
- `src/app/features/orders/data-access/orders-api.service.ts` — new — backend communication — isolates transport details from UI code.

## 5. Risks the skill should call out

Always look for:
- duplicate services or models already present
- another feature already solving the same use case
- feature-specific code drifting into shared/core
- route conflicts
- backend contract uncertainty
- required environment/config changes
- missing tests
- missing loading/error/empty states in the UI plan

## 6. Good planning behavior

Prefer:
- file-by-file placement
- explicit responsibility boundaries
- practical order of work
- repository-specific language

Avoid:
- hand-wavy “create a component and a service”
- inventing folders not justified by the feature
- prescribing unrequested migration work
- forcing a state library unless the repo already uses one