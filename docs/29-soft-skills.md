## 29. Soft skills for engineers

Technical skill gets you hired; soft skills decide how far you go. They are learnable habits, not personality traits. Related material: sections 1, 4, 23, 24, 26 and 28.

### 29.1 Building trust as a new hire

- **Do what you say, when you say it.** Small promises kept (I'll send that today) build more trust than big promises.
- **Be visible and predictable:** update issues, post short progress notes, and flag risks early. Surprises destroy trust faster than bad news.
- **Learn before you judge.** Ask why things are the way they are; avoid phrases like this is a mess in public.
- **Give credit generously** and in public; take responsibility for mistakes quickly.
- **Early wins:** pick small, real tasks, finish them well, and document what you learned.
- **Understand people, not only code:** learn who owns what, how each person likes to communicate, and what the team cares about.

### 29.2 Giving and receiving feedback

- **Giving:** be specific, timely, kind and actionable. A useful structure is **SBI:** Situation (when and where), Behavior (what you observed, not your interpretation), Impact (the effect). Example: In yesterday's review (S), the MR had no description (B), so it took me 20 minutes to understand the goal (I). Could you add the why next time?
- Give feedback privately when it is critical and publicly when it is praise. Ask permission when appropriate: Can I share a thought on the demo?
- **Receiving:** listen fully, do not defend immediately, ask a clarifying question, say thanks, then decide what to do. Feedback is information about how you were received, not a verdict on your worth.
- Separate **the idea from the person**, and **intent from impact.**
- Ask for feedback regularly: What is one thing I could do better in reviews?

### 29.3 Handling conflict and disagreement

- **Start from shared goals** (the product, the deadline, quality), then discuss the options.
- **Understand first:** restate the other view (steelman) and ask what concerns or constraints lie behind it.
- Argue with **evidence and trade-offs** (data, examples, a small prototype), not with rank or repetition.
- Move heated written threads to a **call**; follow up in writing with the decision.
- If you stay stuck, **escalate the decision, not the conflict:** ask the owner or lead to decide, then **disagree and commit.**
- Assume good intent. Text hides tone; read messages in the kindest plausible way and ask when unsure.
- After a disagreement, repair the relationship quickly: a short, warm message goes a long way.

### 29.4 Asking for help and admitting mistakes

- **Timebox your struggle** (for example 30-60 minutes on a bounded problem), then ask. Do not wait days.
- A good question includes: the goal, what you tried, what you expected, what happened (with exact error text), and what you need.
- Ask in public channels when others may benefit; ask directly when it is sensitive. Say thank you and share the answer afterwards (add it to the docs).
- **Mistakes:** say it early and plainly: I broke X, here is the impact, here is my plan to fix it, here is how I will prevent it. Do not hide, blame or over-apologize.
- A blameless culture (focus on systems and process) makes everyone safer; model it.

### 29.5 Saying no, scope, deadlines and estimates

- Prefer **not yet** and **yes, if** over a flat no: I can do that if we move X, or in two days instead of one.
- Make **trade-offs visible:** time, scope, quality and cost are linked. Ask which one can change.
- **Estimates are forecasts.** Give ranges, state assumptions, and slice work. Update immediately when facts change.
- Protect quality: the usual lever is scope, not skipping tests or review.
- Push back on unclear requirements by asking for acceptance criteria rather than guessing.
- Handle scope creep with a simple rule: new requests become new issues, then get prioritized.

### 29.6 Time management and focus

- Plan **three priorities** each morning; protect one or two blocks of **deep work** (no chat, no notifications).
- **Batch** shallow work: messages, small reviews, admin. Review pending MRs early in the day so others are unblocked.
- Use **timeboxes** (Pomodoro-style 25-50 minute blocks) and short breaks; sleep and rest are productivity tools.
- **Finish before starting** (limit work in progress). Write down parked ideas so your mind lets go.
- Use the **Eisenhower matrix** (urgent vs important) and the 80/20 rule to choose.
- Reduce context switching; set status messages when focusing; agree on response-time expectations with the team.
- Say no to low-value work politely and propose a time to revisit.
- Keep a simple end-of-day note: what is done, what is next, what is blocked (this also feeds your time report, section 25).

### 29.7 Working with non-developers

- **Designers:** ask about intent, states (loading, empty, error), responsive and RTL behavior; show early builds; use shared tokens and components.
- **Product owners and managers:** translate technical terms into impact (time, risk, user value); propose options with trade-offs; confirm acceptance criteria.
- **QA:** share how to test, edge cases and known limits; treat bug reports as gifts, reproduce before arguing.
- **Backend:** agree on API contracts early (OpenAPI), error formats and pagination; do not guess; document mismatches in the issue.
- **Support and stakeholders:** listen to the real problem behind the request; give honest timelines; close the loop when it ships.
- Avoid jargon, use pictures and examples, and check understanding: Does that match what you expected?

### 29.8 Mentoring and being mentored

- **Being mentored:** come with specific questions and goals, take notes, try things before asking, and report back on what you did with the advice.
- **Mentoring (even as a junior):** explain the why, pair on problems, share resources, and let others struggle a little before helping. Teaching is the fastest way to learn.
- Write down what you learn (docs, short posts); it helps the next new hire and cements your knowledge.
- Seek multiple perspectives; no single person has all the answers.

### 29.9 Stress, burnout and impostor syndrome

- **Impostor feelings are common**, especially in a new job. Counter them with evidence: keep a **wins log** of tasks done, problems solved, and feedback received.
- Remember that nobody knows the whole system; asking questions is a sign of engagement.
- Set **boundaries:** regular hours, offline time, and breaks. Sustainable pace beats heroics.
- Watch early signs of burnout (constant exhaustion, cynicism, falling quality) and talk to your manager or a trusted person early. Seek professional support if stress feels heavy.
- Separate **what you control** (effort, communication, learning) from what you do not (deadlines set above you, other teams).
- Take care of basics: sleep, movement, food, and social contact.

### 29.10 Career growth, visibility and 1:1s

- **Ask for expectations:** What does good look like at 30, 60 and 90 days? How is performance evaluated?
- **1:1s are yours:** prepare an agenda (progress, blockers, feedback, growth, questions), take notes, follow up on actions.
- **Make your impact visible** without bragging: short demos, written updates, and a running list of achievements with results (numbers where possible). This helps at review time.
- Pick growth areas on purpose (testing, architecture, performance, accessibility, leadership) and ask for work that stretches you.
- **Share knowledge:** docs, lunch-and-learns, helping others in reviews. Seniority is mostly about increasing the effectiveness of the people around you.
- Build a network inside and outside the company (communities, open source, conferences).
- Review your own growth every quarter: what did I learn, what would I do differently, what is next?

### 29.11 A short daily checklist

1. Greet, check blockers and pending reviews, and set three priorities.
2. Communicate early when something changes (estimate, scope, blocker).
3. Write clearly: descriptions, commit messages, summaries.
4. Give one piece of specific, kind feedback or thanks.
5. Ask one good question or share one thing you learned.
6. Close the day with notes and a time report.
