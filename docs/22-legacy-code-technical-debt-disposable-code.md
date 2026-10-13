## 22. Legacy code, technical debt and disposable code

**Definitions**

- **Legacy code** (Michael Feathers): code without tests, so you cannot change it with confidence. It is also simply code that is old, poorly understood, or whose authors left.
- **Technical debt** (Ward Cunningham): shortcuts that speed delivery now and cost interest later, in slower changes and more bugs. Not all debt is bad; unmanaged debt is.
- **Fowler's debt quadrant:** deliberate vs inadvertent, reckless vs prudent. Prudent and deliberate (we ship now and fix soon) is acceptable; reckless and inadvertent (we did not know better) is solved by learning and review.
- Kinds of debt: code, design/architecture, test, documentation, dependency, infrastructure, and knowledge (bus factor).

**Working safely in legacy code**

1. **Understand before changing:** read `git log` and `git blame`, find the entry points and the data flow, ask the people who know.
2. **Chesterton's Fence:** find out why something exists first.
3. **Pin behavior** with characterization tests (or at least manual test notes) before risky changes.
4. **Find seams** (Feathers): places where you can change behavior without editing the surrounding code, such as props, context, or module boundaries.
5. **Make small, reversible steps.** Commit often; one refactor per commit.
6. **Sprout instead of rewrite:** write the new behavior as a new, clean, tested component or function and call it from the old code. Or **wrap** the old code behind a clean interface.
7. **Strangler Fig:** route new features to the new pattern and migrate old screens opportunistically. Avoid big-bang rewrites; they stall and reproduce old bugs.
8. Use **codemods** (jscodeshift, ts-morph) for repetitive large-scale changes, reviewed in their own MR.
9. Migrate JavaScript to TypeScript incrementally (allowJs, convert files as they are touched, tighten `strict` per folder).

**Managing technical debt as a team**

- **Make it visible:** create issues with a `tech-debt` label and a short template: what, where, the pain it causes, the cost of leaving it, a rough size, and a proposed fix.
- **Prioritize by pain times frequency of change:** debt in code that changes weekly hurts more than debt in a stable corner. Look at **hotspots** (high churn plus high complexity).
- **Speak business language:** slower delivery, more bugs, onboarding time, risk, cost. Not that the code is ugly.
- **Budget for it:** reserve a steady share of each sprint (commonly 10-20 percent) or one debt item per sprint, instead of a one-off cleanup sprint that never happens.
- **Attach debt to features:** when a feature touches debt, include the preparatory refactor in the estimate.
- **Do not create new debt silently.** If you take a shortcut, record it (issue and a TODO with ticket) and say it in the MR.
- **Deprecation process:** mark it (`@deprecated`), warn, provide the migration path, set a removal date, remove.
- Track a few signals (build time, flaky tests, bug rate in hotspots, dependency age) but do not turn them into targets (Goodhart's Law).

**Disposable code**

Disposable code is code you expect to delete: prototypes, spikes, migration shims, temporary workarounds, experiments, one-off scripts. The goal is to **make it easy to find and remove, and hard to keep by accident.**

| Type | Treatment |
| --- | --- |
| Spike or prototype | Throwaway branch or `experiments/`; record findings in the issue or an ADR; rewrite properly instead of merging it |
| Migration shim or adapter | Isolate in one folder or file (`legacy/`, `*.compat.ts`) |
| Temporary workaround | Comment the reason, ticket and removal condition |
| Feature-flagged experiment | Delete the flag and the losing branch after the decision |
| One-off script or codemod | Keep in `scripts/` with a short header, or delete after use |

```ts
// TODO(PROJ-482, remove-by 2026-12-01): backend returns user_name until the v2 API ships.
// Delete this adapter and read username directly once the API is migrated.
export const adaptLegacyUser = (u: LegacyUser): User => ({ ...u, username: u.user_name });
```

- Always include a **ticket plus a removal condition or date**.
- Create the **cleanup issue at the same time** as the shim and put it in a future milestone or iteration.
- **Isolate behind a boundary** so deleting it is a one-file change. Do not let it leak into shared types and components.
- Prefer code that is easy to delete over code that is easy to extend.
- Search for `remove-by` in CI or a periodic job; review expired items at sprint planning.
- Do not write tests for throwaway code, but do test the permanent logic around it.
- **Disposable does not mean sloppy.** It still needs to be correct, typed and readable, because it often outlives its plan.
