---
name: modern-angular-architect
description: Analyze modern Angular repositories and produce an implementation plan for new features, validating architecture, file placement, and fit with current Angular conventions before any code changes.
---

# Modern Angular Architect

Use this skill when:
- the user wants to add a feature to an Angular repo;
- the user asks where files should go in a modern Angular codebase;
- the user wants an Angular architectural review before implementation;
- the user explicitly mentions `modern-angular-architect`.

This is a **plan-first, no-write** skill.

## Core behavior

1. Inspect the repository and identify the Angular shape actually in use.
2. Interpret the requested feature.
3. Map the feature onto the existing repo structure.
4. Produce a concrete file-by-file implementation plan.
5. Explain architectural fit, assumptions, and risks.
6. Do not edit files.

## First-pass repo inspection

Look for:
- `package.json`
- `angular.json`
- `tsconfig*.json`
- `src/main.ts`
- `src/app/`
- route definitions
- bootstrap/config files
- existing feature folders
- standalone components, route definitions, services, guards, interceptors, stores, facades, models, API clients, tests

Do not assume Nx, NgRx, Angular Material, SSR, or any specific stack unless the repo proves it.

## Angular reference material

Before planning, use these references as needed:

- Architecture guide: `references/angular-modern-architecture.md`
- Feature planning guide: `references/angular-modern-feature-planning.md`
- Output quality rubric: `references/planning-output-rubric.md`

Prefer the repo’s current conventions first. Use the references to resolve ambiguity, not to force a rewrite.

## Required output format

Always structure the response as:

### A. Architecture snapshot
How the repo is organized today.

### B. Feature interpretation
What the requested feature appears to require.

### C. Proposed file plan
For each proposed file or folder:
- relative path
- new or modified
- responsibility
- why it belongs there

### D. Implementation sequence
A practical order of work.

### E. Risks and assumptions
Explicit unknowns, dependencies, or architectural tensions.

### F. Next action
One concrete next step.

## Planning rules

- Be repository-specific.
- Prefer concrete paths over generic advice.
- Preserve current conventions where reasonable.
- Recommend broad re-architecture only if the user explicitly asks for it.
- If the repo is sparse or greenfield, use the fallback guidance in `references/angular-modern-architecture.md`.
- Do not write files.

## Quality bar

A strong answer:
- reflects the actual repo;
- recognizes whether the repo is standalone-first, module-legacy, or mixed;
- places files by feature boundaries;
- keeps shared/core code limited to real cross-cutting concerns;
- calls out risks and missing information;
- reduces implementation ambiguity.