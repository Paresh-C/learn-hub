## 2. Refactor vs Boy Scout Rule in legacy code (and other rules worth knowing)

**Boy Scout Rule:** leave the code a little cleaner than you found it (popularized by Robert C. Martin). Small, safe, local improvements in files you are already changing.

**Refactoring:** a deliberate, planned, structural change that does not alter behavior. It has its own issue, MR and (ideally) tests.

| | Boy Scout Rule | Planned refactor |
| --- | --- | --- |
| Size | Minutes, a few lines | Hours to weeks |
| Trigger | You are already in the file | Pain, bugs, a blocked feature, a tech-debt issue |
| Examples | Rename a vague variable, delete dead code, extract a constant, add a type, fix a typo, add a missing key | Replace hand-rolled fetch with RTK Query, split a 900-line component, change folder structure |
| MR | Same MR, separate small commit (`refactor:`) | Own issue, milestone and MR |
| Risk | Very low | Needs tests or characterization tests first |

**Decision guide**

1. Can you do it in under \~10 minutes, in code you are already editing, with no behavior change? Boy Scout it.
2. Does it touch many files, shared behavior, or need a design decision? Create an issue, estimate it, plan it.
3. Is it blocking your feature? Use **preparatory refactoring**: make the change easy, then make the easy change (Kent Beck). Do the refactor as a separate commit or MR first.
4. Not covered by tests and risky? Write characterization tests (pin current behavior) before changing.

**Limits of the Boy Scout Rule**

- Do not bury cleanups in a feature diff so large that reviewers cannot see the real change. Keep cleanups in their own commits.
- Do not clean files you do not understand. Ask or read the history.
- Never mix a formatting-only change across a whole file with logic changes. Run formatters in a separate MR.

**Other rules and laws useful for you**

- **Two Hats (Fowler):** either add behavior or refactor, never both in the same step or commit.
- **Make it work, make it right, make it fast** (Beck). In that order.
- **Rule of Three:** duplicate once, tolerate twice, abstract on the third time.
- **YAGNI / KISS:** build what is needed now, in the simplest way that works.
- **Strangler Fig:** grow the new system around the old one and replace it piece by piece, instead of a rewrite.
- **Gall's Law:** complex systems that work evolved from simple systems that worked. Start simple.
- **Hyrum's Law:** with enough users, every observable behavior of your API will be depended on by someone. Be careful changing outputs.
- **Conway's Law:** system structure mirrors the communication structure of the organization. Architecture problems are often team problems.
- **Hofstadter's Law:** it always takes longer than you expect, even when you account for that. Pad estimates and slice work small.
- **Parkinson's Law:** work expands to fill the time available. Timebox.
- **Brooks's Law:** adding people to a late project makes it later.
- **Pareto (80/20):** most value or most bugs come from a small part of the system. Focus there.
- **Goodhart's Law:** when a measure becomes a target, it stops being a good measure (coverage %, story points, lines of code).
- **Kernighan's Law:** debugging is twice as hard as writing code, so do not write code as cleverly as you can.
- **Postel's Law (use carefully):** be conservative in what you send, liberal in what you accept. Validate input anyway.
- **Law of Demeter:** talk to your neighbors, not strangers (`a.b.c.d()` chains are a smell).
- **Principle of Least Astonishment:** code should do what a reader expects.
- **Fail fast:** surface errors early and loudly rather than hiding them.
- **Premature optimization is the root of much evil (Knuth):** measure first.
- **Bus factor:** if only one person understands something, that is a risk. Share knowledge via docs and pairing.
