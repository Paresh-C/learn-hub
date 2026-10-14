## 28. Reasoning and fallacies

**Reasoning tools**

- **Separate facts, assumptions and opinions.** Write them down; test assumptions.
- **Deductive, inductive, abductive reasoning:** certain from rules, probable from patterns, best explanation from evidence. Most debugging is abductive.
- **Hypothesis-driven debugging:** observe, form a hypothesis, make a prediction, test it, change one thing at a time. Make the bug reproducible first.
- **5 Whys / root cause analysis:** keep asking why until you reach something you can fix. Fix causes, not symptoms.
- **First principles:** break a problem into facts you know are true, then rebuild.
- **Occam's razor:** prefer the simplest explanation that fits. **Hanlon's razor:** do not assume malice where carelessness explains it.
- **Inversion:** ask what would make this fail, then avoid that. Run a **pre-mortem** (imagine the project failed; why?).
- **Second-order thinking:** and then what? Consider consequences of consequences.
- **Reversible vs irreversible decisions (two-way doors):** decide fast on reversible ones, slowly on irreversible ones.
- **Base rates and probability:** how often does this usually happen? Update beliefs when evidence arrives (Bayesian thinking).
- **Falsifiability:** what evidence would prove me wrong? If nothing could, be suspicious.
- **Steelman:** state the opposing view in its strongest form before replying.
- **Calibrated confidence:** say how sure you are (I'm about 70 percent sure) and what would change your mind. Strong opinions, weakly held.
- **Write down decisions and reasoning** (ADRs) so later you can learn from them rather than rewrite history.

**Common fallacies and biases, with developer examples**

| Name | What it is | Example | Better move |
| --- | --- | --- | --- |
| Ad hominem | Attacking the person, not the argument | That dev always writes bad code, ignore the idea | Evaluate the idea on its merits |
| Straw man | Misrepresenting a position to defeat it | You want no tests at all? (when they said not everything needs tests) | Restate their view and confirm it first |
| Appeal to authority | It is true because an important source says so | Google uses it, so we should | Ask what problem it solves for us |
| Bandwagon / hype | Popular means right | Everyone is moving to X | Compare against our constraints |
| Appeal to tradition | It is right because we always did it | We have always done it this way | Ask what it costs and what alternatives exist |
| Appeal to novelty | New means better | A new framework will fix this | Prove the benefit with a pilot |
| False dilemma | Only two options are offered | Rewrite everything or live with it | List more options (incremental migration) |
| Slippery slope | One step inevitably leads to disaster | If we allow one any, types are doomed | Argue the actual likelihood |
| Hasty generalization | Broad claim from few cases | Two bugs from the library, so it is unreliable | Look for more data |
| Post hoc / false cause | Because it followed, it was caused by | Bug appeared after the deploy, so the deploy caused it | Check timelines, diffs and logs |
| Correlation is not causation | Two things move together | More tests, more bugs found | Look for a confounder |
| Circular reasoning | The conclusion is in the premise | It is best practice because it is the right way | Give independent reasons |
| Red herring | Distracting from the point | Changing topic mid-review | Return to the question |
| Appeal to ignorance | No evidence against means true | Nobody reported a bug, so it works | Look for evidence actively |
| Anecdotal evidence | One story as proof | It works on my machine | Reproduce in a clean environment |
| Burden of proof shifting | Asking others to disprove your claim | Prove that this will not scale | The claimant supplies evidence |
| False authority by title (HiPPO) | The highest-paid person's opinion wins | The CTO likes it | Ask for data and the reasoning |
| Sunk cost | Continuing because of past investment | We already spent months on this design | Decide from future cost and benefit |
| Confirmation bias | Favoring evidence that fits what you believe | Reading only benchmarks that favor your choice | Actively look for disconfirming evidence |
| Survivorship bias | Looking only at successes | Successful startups use microservices | Ask about the ones that failed |
| Anchoring | First number dominates | The first estimate becomes the plan | Re-estimate independently |
| Planning fallacy | Underestimating time and risk | It is a two-day task | Use past data, add buffer, slice small |
| Availability heuristic | Judging by what is easy to recall | The last outage shapes all priorities | Check frequencies |
| Bikeshedding | Debating trivial things at length | Hours on a variable name, minutes on architecture | Time-box small decisions; automate style |
| IKEA effect | Overvaluing what you built | My component cannot be improved | Welcome reviews |
| Not invented here | Rejecting outside solutions | We should build our own table library | Evaluate buy vs build honestly |
| Golden hammer | Using one tool for everything | Redux for every piece of state | Match tool to problem |
| Resume-driven development | Choosing tech to pad a resume | Kubernetes for a small site | Choose for the problem and the team |
| Cargo cult | Copying practices without understanding | Memoizing every component | Know why a practice works |
| Middle ground fallacy | Truth must be halfway | One says 1 s, the other 10 s, so 5 s | Measure it |
| No true Scotsman | Redefining terms to dodge counterexamples | A real senior would never do that | Accept the counterexample |
| Cherry-picking | Using only supporting data | Showing only the best benchmark run | Show the full data |
| Texas sharpshooter | Finding patterns after seeing the data | Declaring the cause after the fact | Set hypotheses before testing |

**Using this in practice**

- Name the *pattern* quietly, not the label. Saying that is a fallacy escalates conflict; asking what evidence supports it or what else could explain it keeps the discussion productive.
- Define terms (what do we mean by fast or scalable?) and ask for numbers.
- Aim to be less wrong, not to win. Change your mind visibly when the evidence changes; it builds trust.
- Notice your own biases first; most bugs in reasoning live there.
