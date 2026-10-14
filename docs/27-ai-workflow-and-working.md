## 27. AI workflow and working with agents

**Mindset:** treat an AI agent like a very fast, tireless, sometimes overconfident junior pair. It speeds up work, but **you own every line you commit**. If you cannot explain a change in review, it should not be merged.

**First: company policy**

- Ask what tools, models and data are allowed. Check rules on source code, customer data, secrets and licensing.
- Do not send secrets, credentials, customer data or proprietary code to tools or providers that are not approved.

**The tools (as far as I know; verify against each project's current docs)**

- **Claude Code:** a terminal-based coding agent. Reads your repo, edits files, runs commands. Supports a project memory file (`CLAUDE.md`), plan mode, custom slash commands, subagents, hooks, permission settings and MCP connections.
- **Codex (OpenAI):** a coding agent with CLI and cloud variants; reads project instructions from `AGENTS.md`.
- **Cline:** an open-source VS Code agent with Plan and Act modes and per-step approvals; you can bring your own model or API key; project rules go in `.clinerules`.
- **9router:** as far as I know, a router/proxy that sits between coding tools and several model providers, offering one endpoint and fallback between providers or plans. I could not verify details, so read its README. Routing work code through a third-party proxy or free tier is a data-handling decision; get approval before pointing a company repo at it.

**A reliable workflow**

1. **Define the task:** goal, constraints, files involved, acceptance criteria, what not to touch.
2. **Explore and plan first** (plan mode or ask for a plan). Read the plan; fix wrong assumptions before any code is written.
3. **Work in small steps** on a feature branch; commit before each agent run so you can diff and revert.
4. **Make it verify itself:** tell it the commands (`pnpm lint`, `pnpm tsc --noEmit`, `pnpm test`) and to run them.
5. **Review the diff line by line** like an MR from a stranger: correctness, scope, types, security, style, unnecessary changes.
6. **Write the MR description yourself** (or edit the draft) so it states the real why. Link the issue with a closing keyword.
7. **Start fresh sessions** for unrelated tasks; long, noisy contexts degrade results.

**Context engineering (the biggest lever)**

- Keep a short rules file in the repo (`CLAUDE.md`, `AGENTS.md`, `.clinerules`): stack and versions, how to run build/lint/test, folder map, conventions (naming, RTK Query patterns, error handling), do/do-not rules, and known gotchas.
- Point the agent to a good existing example: follow the pattern in `features/orders` for this new feature.
- Update the rules file whenever you correct the same mistake twice. Commit it through an MR so the team shares it.
- Reference specific files and paste full error messages and logs.

**Prompting well**

- Provide **goal, context, constraints, output format.** Ask for questions if requirements are unclear.
- Ask for **options with trade-offs** before decisions; you decide.
- Say what to avoid: new dependencies, changing public APIs, touching unrelated files, disabling tests or lint rules.
- One task per prompt or session; split big work into steps.

**Safe use**

- Review permissions. Do not auto-approve destructive actions (`rm -rf`, force push, database migrations, deploys, package installs).
- Work on a branch or in a git worktree/container; keep `.env` and secrets out of the agent's reach.
- Be careful with new dependencies it adds: check they exist, are maintained and are what you expect (models sometimes invent package names, and attackers register those names).
- Give MCP connections (GitLab, databases, docs) the **least privilege**, read-only where possible.

**Common failure modes**

- Hallucinated APIs or props, or code for an outdated library version; verify against the docs and your installed version.
- Over-engineering, duplicated helpers, ignoring project conventions.
- Making tests pass by weakening them; silently widening scope; huge diffs.
- Confident but wrong explanations; subtle bugs and security holes (XSS, unsafe URLs, secrets).
- Mitigations: types, lint, tests, small diffs, careful review, and asking it to justify choices.

**Good uses:** explaining unfamiliar code during onboarding, mapping a codebase, drafting tests for pure logic (you review), boilerplate, codemods and migrations (JS to TS), debugging with logs, regex, TypeScript types, MR and commit message drafts, a first-pass code review, documentation drafts, rubber-duck thinking.

**Poor uses:** unreviewed large changes, security-critical code without expert review, architecture decisions you cannot evaluate, or anything where you skip understanding.

**Keep learning:** ask for the why, write some code yourself, and quiz yourself on what the agent produced. Skills you never practice fade.

**Parallel work:** git worktrees let several agents work on separate branches at once; use one agent to write and another session to review. Choose cheaper models for simple tasks and stronger ones for planning and hard debugging.

**Team norms:** agree on an AI usage policy, share the rules file, and review AI-assisted code exactly like any other. A good test: would I be comfortable defending every line in review?
