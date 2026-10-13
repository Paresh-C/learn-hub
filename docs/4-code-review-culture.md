## 4. Code review culture

- Review for: correctness, readability, edge cases, tests, accessibility, performance, security. Leave style to the linter.
- Distinguish blocking comments from suggestions with prefixes: `nit:`, `optional:`, `question:`, `blocking:`.
- Critique the code, not the person. Ask questions (What happens if this is null?) rather than issuing orders.
- Authors self-review the diff before requesting review, and explain the why in the MR description.
- Aim for a review turnaround of about one business day. Do not let MRs go stale.
- Review in layers: design first (does the approach make sense?), then logic, then details.
- Say what is good too. Specific praise teaches the team what to repeat.
- Resolve threads yourself only when you addressed them; let the commenter resolve questions.
- When you disagree, state the trade-off and ask for the reasoning. If stuck, move to a call or chat; escalate decisions to the owner, then write the outcome down.
- Receiving review: assume good intent, do not take it personally, reply to every comment (Done, or why not), and keep MRs small to make review easier.
