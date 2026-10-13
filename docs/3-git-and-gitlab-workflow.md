## 3. Git and GitLab workflow

Issues → branches → MRs

**Branching**

- Pick one strategy and write it down: trunk-based (short-lived branches off `main`, preferred for most web teams) or GitHub/GitLab Flow. Avoid long-lived feature branches; they cause painful merges.
- Create the branch from the issue so GitLab links them: `123-add-login-form`. Or use a naming convention such as `feat/PROJ-123-user-avatar`, `fix/PROJ-456-login-redirect`, `chore/upgrade-eslint`.
- Rebase or merge `main` into your branch often. Small, frequent syncs avoid conflict pain.

**Commits**

- Use [Conventional Commits](https://www.conventionalcommits.org/): `feat:`, `fix:`, `refactor:`, `docs:`, `test:`, `chore:`, `perf:`, `ci:`, `build:`, `style:`, `revert:`. This enables automatic changelogs and semantic versioning.
- Include a scope and issue reference: `fix(auth): handle expired refresh token (#123)`.
- Make commits atomic: one logical change each, and the project builds after each one.
- Subject in imperative mood, at most 72 chars (Add retry logic to token refresh). Use the body for the why.
- Enforce with **commitlint + Husky**.
- Useful commands: `git commit --fixup`, `git rebase -i --autosquash`, `git stash -u`, `git reflog` (undo almost anything), `git bisect` (find the commit that broke something), `git restore`, `git switch`, `git cherry-pick`, `git commit --amend` (only on unpushed work), and `git push --force-with-lease` (never plain `--force`).

**Merge requests (MRs)**

- Keep them small (ideally under 400 changed lines). Small MRs get reviewed faster and better.
- Open as **Draft** early (`/draft` quick action or a `Draft:` title prefix) for feedback. Use `/ready` when done.
- Add an **MR template** (`.gitlab/merge_request_templates/Default.md`): what and why, `Closes #123`, screenshots or video for UI changes, how to test, checklist (types, a11y, docs, tests).
- Prefer **squash merge** for a clean history (or rebase/fast-forward if the team writes good atomic commits). Enable Delete source branch.
- Require: pipeline must succeed, all threads resolved, required approvals.
- Consider **merge trains** when `main` is busy, so each MR is tested against the latest `main`.

**Closing keywords (GitLab)**

Put these in the MR description or a commit message. The issue closes automatically when the change reaches the default branch.

```
Closes #123
Fixes #45, #46
Resolves group/other-project#9
Implements #77
```

- Accepted verbs: Close/Closes/Closed/Closing, Fix/Fixes/Fixed/Fixing, Resolve/Resolves/Resolved/Resolving, Implement/Implements/Implemented/Implementing.
- Use `Related to #12` or `/relate #12` when you do not want auto-closing.
- Each closing keyword needs its own issue reference; a keyword placed in a comment on the issue will not close it.

**Milestones, iterations and labels**

- **Milestone** = a release or goal (`v2.4`, `Q4 Checkout`). **Iteration** = the sprint (a Premium/Ultimate feature). Without iterations, use one milestone per sprint or a scoped label such as `sprint::14`.
- Assign **both issues and MRs** to the milestone so progress and burndown stay accurate.
- **Scoped labels** (`type::bug`, `priority::high`, `workflow::in-review`) are mutually exclusive inside a scope; boards can use them as columns.
- **Quick actions** (type them in descriptions or comments):

```
/milestone %v2.4
/label ~type::feature ~workflow::in-review
/assign @me
/reviewer @teammate
/estimate 3h
/spend 1h
/due 2026-11-01
/relate #200
/draft
/ready
```

- Use an **Issue Board** with columns like Backlog, In Dev, In Review, QA, Done.

**Templates and protections**

- Issue templates: `.gitlab/issue_templates/Bug.md` and `Feature.md` with acceptance criteria and definition of done.
- `CODEOWNERS` plus approval rules; protect `main` (no direct pushes, no force push).
- Dependency updates: Renovate (works well with GitLab) or scheduled update MRs.
- Good `.gitignore`; never commit `.env` or secrets. Use secret detection (GitLab Secret Detection, `gitleaks`).
- **Hooks:** Husky + lint-staged run ESLint, Prettier and type-check on staged files pre-commit. Keep hooks fast; CI is the real gate.
