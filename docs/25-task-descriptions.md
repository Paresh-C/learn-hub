## 25. Task descriptions and end-of-day time reports

There are two related writing jobs: the **task (issue) description** that defines work, and the **time-report entry** that records what you did. Both exist so another person can understand the work without asking you.

**A. Writing a good task/issue description**

```md
## Context / problem
Why this exists, who is affected, link to design or discussion.

## Goal
The outcome in one or two sentences.

## Acceptance criteria
- [ ] Given ..., when ..., then ...
- [ ] Works on mobile and in RTL
- [ ] Loading, error and empty states handled

## Out of scope
What this issue deliberately does not cover.

## Technical notes
API endpoints, affected modules, risks, links.

## Test plan
How to verify, including edge cases.

## Dependencies
Other issues, backend work, approvals.
```

**B. Writing time-report entries (end of the working day)**

**Formula:** `[Action verb] + [what] + [where or why] + [result or status]`, plus the ticket id.

| Weak | Strong |
| --- | --- |
| Worked on login | Implemented token refresh handling in the auth baseQuery (PROJ-123); MR open for review |
| Fixed bugs | Fixed double-submit on the checkout form (PROJ-456); added a guard and verified manually |
| Meetings | Sprint planning and backlog refinement for the orders epic |
| Debugging | Investigated the 500 on the invoice list; root cause is a null date field; reported to backend (PROJ-478), waiting for fix |
| Code review | Reviewed MR !212 (user profile form): 6 comments, approved with suggestions |

**What is important to include**

- **What you actually did** (verb first): implemented, fixed, investigated, reviewed, refactored, documented, tested, deployed, paired.
- **The thing it concerned:** feature, component, endpoint, or MR/issue number.
- **The status or result:** done, in review, blocked, partially done, needs input.
- **Blockers and who you are waiting for**, with the ticket or person.
- **Category of work** if your report separates them: development, bug fix, code review, meeting, investigation, testing, documentation, support, deployment.
- **Outcomes over activity:** what changed or was learned, not just that time passed.
- **Surprises and estimate overruns**, briefly, so planning improves.

**What is not important (leave out)**

- Micro-steps (opened the editor, ran the dev server, searched Google).
- Vague filler (worked on stuff, did tasks, misc).
- A long retelling of the whole ticket or your debugging journey; link to the ticket instead.
- Emotions, complaints, or blame (frustrating, X broke it).
- Secrets, tokens, customer data or private details.
- Padding or inventing hours. Report real time; if a task took longer than planned, say why in one line.
- Duplicating the same sentence across days; show progress instead (Day 2: finished validation, Day 3: added tests).

**Daily summary template**

```md
Done: ...
In progress: ... (status, % or next step)
Blocked: ... (waiting on whom, ticket)
Next: ...
```

**Habits that make this easy**

- Jot a one-line note at the end of each work block instead of reconstructing the day at 6 pm.
- Log time in the tool the team uses; in GitLab use `/spend 1h30m` on the issue or MR.
- Round sensibly (15-minute steps) and be consistent.
- Keep entries short: one line per task, one extra line only for blockers or results.
- Match the team's wording and ticket conventions. Ask your lead what level of detail they expect.
