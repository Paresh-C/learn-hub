## 1. Joining a codebase: the first month

Most improvement efforts fail socially, not technically.

- **Spend 2-4 weeks learning.** Read the code, merge request (MR) history and old issues. Many bad-looking decisions had a reason: deadlines, legacy constraints, a past incident.
- **Chesterton's Fence:** do not remove something until you know why it was put there. Ask first, then change.
- **Keep an improvement backlog** with evidence (bundle size, bug counts, screenshots, build times). Evidence beats opinion.
- **Fix things in the area you are already touching** (Boy Scout Rule) instead of opening giant refactor MRs.
- **Propose, do not impose.** Bring data and a small pilot, then let the team decide.
- **Automate agreement.** A rule enforced by a linter or CI is a rule nobody argues about in review.
- **Ask good questions.** Try first for a bounded time (e.g. 30-60 min), then ask with context: what you tried, what you expected, what happened.
- **Find the owners.** Know who owns auth, payments, the design system, CI, and the API. Most delays are waiting for the right person.
