# Planning Output Rubric

Use this rubric internally when preparing the final answer.

## Pass conditions

A strong plan should satisfy all of these:

1. **Repo awareness**
   - The answer describes the current repo shape.
   - It identifies whether the repo is standalone-first, module-based, or mixed.

2. **Feature interpretation**
   - The answer explains what the feature likely requires.
   - It distinguishes routed/UI/data/state/infrastructure concerns.

3. **Concrete file plan**
   - Proposed paths are explicit and plausible.
   - Each path has a responsibility and a reason.
   - New vs modified is clear.

4. **Architectural fit**
   - The plan follows existing conventions where possible.
   - Shared/core are used sparingly and intentionally.
   - Feature cohesion is preserved.

5. **Execution quality**
   - There is a practical implementation sequence.
   - Risks and assumptions are explicit.
   - The answer does not drift into code generation.

## Warning signs

These weaken the output:
- global `components/services/models` advice with no repo mapping
- recommending NgModule-heavy structure for clearly standalone-first code
- using `effect()` for derived state
- proposing experimental forms APIs as default production advice
- moving feature-local code into shared too early
- giving only generic Angular best practices without file placement

## Scoring guide

- 90–100: concrete, repo-specific, low ambiguity
- 75–89: mostly strong, minor ambiguity
- 60–74: useful but generic in places
- below 60: weak mapping to the repo or modern Angular conventions