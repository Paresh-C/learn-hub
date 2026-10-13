## 21. Documentation and comments

**Principles**

- **Docs-as-code:** docs live in the repo, are reviewed in MRs, and change with the code. A behavior change updates the docs in the same MR (add it to the MR checklist).
- Organize by reader need (the Diataxis framework): **tutorials** (learn by doing), **how-to guides** (solve a task), **reference** (facts), **explanation** (why).
- Short beats long. Link to code instead of copying it. Put an owner and last-reviewed date on important docs.
- Write for someone who joined yesterday; that person is you in six months.

**What goes where**

| Need | Where |
| --- | --- |
| Setup, scripts, env vars, folder map, how to run tests | `README.md` |
| Branching, commits, MR rules, review expectations, closing keywords | `CONTRIBUTING.md` |
| Why a decision was made | ADRs in `docs/adr/0001-use-rtk-query.md` |
| Component and hook usage | TSDoc on exports, Storybook for shared UI |
| Diagrams (data flow, auth, architecture) | Mermaid in markdown (GitLab renders it) |
| Guides, onboarding, glossary | `docs/` folder, or the GitLab Wiki if non-developers edit |
| Operations and incidents | Runbooks and blameless postmortems |
| API contracts | OpenAPI spec or generated types |
| Version history | Changelog generated from Conventional Commits |

**ADR template**

```
# 0007. Use RTK Query for server state
Status: Accepted (2026-10-13)
Context: We hand-roll fetch calls and duplicate caching logic...
Decision: Use RTK Query for all new API calls.
Consequences: Less boilerplate, cache invalidation via tags; team must learn tags.
Alternatives considered: TanStack Query, SWR.
```

**Comment standards**

- Comment the **why**, not the **what**. The code shows what; comments explain intent, trade-offs, workarounds and non-obvious constraints.
- Bad: `// increment counter`. Good: `// Safari fires blur before click, so delay closing by one tick`.
- Before writing a comment to explain confusing code, try renaming or extracting a function.
- Use `TODO(name, TICKET-123): ...` and `FIXME(...)` with an owner or ticket so they do not rot.
- Never leave commented-out code. Git remembers.
- Use **TSDoc** on public utilities, hooks and shared components:

```ts
/**
 * Formats an amount for display in the user's locale.
 * @param amount - Value in minor units (e.g. cents).
 * @param currency - ISO 4217 code, e.g. 'USD'.
 * @returns A localized string such as '$12.50'.
 * @example formatMoney(1250, 'USD') // '$12.50'
 * @deprecated Use formatPrice from shared/lib/price instead.
 */
```

- Write comments, identifiers, commit messages and docs in the language the whole team shares (English, see section 26).
- Document **decisions and gotchas** more than obvious facts. Keep a glossary of domain words.
