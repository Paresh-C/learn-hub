## 23. Project management and agile

**Agile in one paragraph:** the Agile Manifesto values individuals and interactions, working software, customer collaboration, and responding to change, over (not instead of) processes, documentation, contracts and plans. In practice: short cycles, frequent delivery, fast feedback, and continuous improvement.

**Scrum (what you will likely see with GitLab sprints)**

- **Roles:** Product Owner (value and priorities), Scrum Master (process and obstacles), Developers (deliver the increment).
- **Events:** sprint (1-4 weeks), sprint planning, daily scrum, sprint review (demo), sprint retrospective, backlog refinement.
- **Artifacts:** product backlog, sprint backlog, increment, each with a commitment (product goal, sprint goal, Definition of Done).

**Kanban:** visualize work on a board, **limit work in progress (WIP)**, manage flow, measure **cycle time** and **throughput**. Good for support-heavy or continuous work. **Scrumban** mixes both.

**Stories, tasks and estimation**

- Hierarchy: epic, story, task. A story delivers user value; tasks are the steps.
- Story format: As a \[role\], I want \[capability\], so that \[benefit\].
- **INVEST:** a good story is Independent, Negotiable, Valuable, Estimable, Small, Testable.
- **Acceptance criteria**, ideally Given/When/Then, make done unambiguous. A **Definition of Ready** says when a story can enter a sprint.
- **Slice stories thin and vertically** (a usable end-to-end piece), not by technical layer.
- Estimation: story points or t-shirt sizes are relative; use **planning poker** to surface misunderstandings. Estimates are forecasts, not promises. Velocity is a planning aid; never a performance score.
- Use a **timeboxed spike** (e.g. 1 day) to reduce uncertainty before estimating a risky story.
- Be honest about uncertainty: give ranges, state assumptions, update early when reality changes.

**Prioritization:** MoSCoW (must, should, could, won't), RICE (reach, impact, confidence, effort), impact vs effort matrix, WSJF, and **Now/Next/Later** roadmaps. Always tie priority to a goal.

**GitLab features to use**

- **Epics** group issues (higher tiers), **issues** with weights, labels, assignees, due dates, **milestones** (releases) and **iterations** (sprints), **boards**, **time tracking** (`/estimate`, `/spend`), **burndown/burnup charts**, **roadmap view**, **MR approvals**, and **service desk** if needed.
- Keep issues current: status via scoped labels or board columns; close with MRs via closing keywords; move unfinished work explicitly at sprint end.

**Delivery health (DORA metrics):** deployment frequency, lead time for changes, change failure rate, time to restore service. Improve them with small batches, automation, and good tests.

**Working well inside the process**

- Raise blockers **early** and specifically: what is blocked, who can unblock, by when.
- Break work down; keep issues under a few days; update issues as you go.
- Manage dependencies (other teams, backend APIs) with explicit contracts and dates.
- Track **RAID:** risks, assumptions, issues, dependencies.
- Retrospective formats: Start/Stop/Continue, 4Ls (Liked, Learned, Lacked, Longed for), Mad/Sad/Glad. Turn findings into one or two owned actions, not a long list.
- **Incidents:** detect, mitigate first, communicate, then fix the root cause; hold a **blameless postmortem** (what happened, why, what we change).
- With your manager: agree on expectations in your first weeks, ask what success looks like at 30, 60, 90 days, and give short written progress updates.
