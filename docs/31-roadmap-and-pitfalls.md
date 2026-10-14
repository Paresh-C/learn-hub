## 30. Roadmap and pitfalls

**Weeks 1-4: learn and low-risk wins**

1. Get the app running; note setup pain and fix the README.
2. Run lint, type-check and build; see what is broken or ignored.
3. Learn the GitLab conventions of your team (closing keywords, labels, milestones, iterations, MR template) and follow them exactly.
4. Read MR history; ask why things are the way they are.
5. Start the improvement backlog with evidence. Apply the Boy Scout Rule in files you touch.
6. Set up your editor (section 29) and, if allowed, your AI workflow with a rules file (section 27).

**Months 1-2: guardrails and automation**

1. Propose and add MR and issue templates, CODEOWNERS, lint rules (warnings first), commit hooks, and basic CI.
2. Add error tracking and error boundaries at root, route, and risky-widget level.
3. Add Vitest and MSW; test pure logic and selectors first; add a test to every bug fix.
4. Write down first ADRs and a short onboarding or conventions doc.

**Months 2-6: incremental improvement**

 1. Standardize RTK Query (tags, error handling, `injectEndpoints`); pilot on one feature, then spread.
 2. Adopt strict TypeScript gradually; validate API responses at the boundary.
 3. Build or consolidate the shared UI layer and document it (Storybook).
 4. Reduce top technical-debt hotspots using strangler-style migrations and a steady debt budget.
 5. Improve performance and accessibility by measured impact.
 6. Share what you learn: short demos, written notes, brown-bag talks.

**Daily and weekly habits**

- Daily: plan three priorities, log notes through the day, write the end-of-day report, review pending MRs first thing.
- Weekly: review your backlog, update issues and milestones, spend an hour learning, and reflect on what slowed you down.
- Always: small MRs, clear descriptions, kind reviews, early communication about blockers.

**Pitfalls to avoid**

- Big-bang rewrites or refactors with no tests; use the strangler pattern instead.
- Introducing a new library, pattern, or tool without team buy-in.
- Perfectionism: consistent and decent beats ideal but half-migrated. Two competing patterns are worse than one mediocre one.
- Mixing refactors with feature changes in one MR, or formatting-only changes with logic.
- Optimizing without measuring; abstracting without three examples.
- Staying silent when blocked, or hiding estimate overruns.
- Shipping AI-generated code you do not understand.
- Judging the existing code harshly in public; the people who wrote it solved real problems with the information they had.
