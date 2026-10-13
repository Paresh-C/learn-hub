## 10. Clean code: modern, fast, agile

**Core principles**

- **Naming:** reveal intent. `isUserEligibleForDiscount` beats `check`. Booleans start with `is/has/should/can`. Avoid abbreviations and noise words like `data`, `info`, `handleStuff`.
- **Functions:** do one thing, stay short, at most 3 parameters (use an options object beyond that), avoid boolean flag arguments, prefer pure functions.
- **Early returns** over deep nesting; avoid nested ternaries.
- **DRY, but do not over-abstract:** duplication is cheaper than the wrong abstraction. Abstract on the third occurrence and only when the duplicated things change for the same reason.
- **KISS and YAGNI:** do not build for hypothetical requirements.
- **No magic values:** extract constants, `as const` objects, or enums.
- **SOLID adapted to the frontend:** single responsibility for components and hooks; open/closed via composition and props; dependency inversion via props, context and injected services (makes testing easy).
- Delete dead and commented-out code. Git remembers.
- Prefer **immutability** and declarative array methods over mutation and manual loops.
- Make illegal states unrepresentable (discriminated unions).
- **Functional core, imperative shell:** keep business logic in pure functions; push side effects (network, storage, DOM) to the edges.
- **Composition over inheritance.** **Explicit over clever.** **Colocate** things that change together.
- **Optimize for deletion:** small, decoupled modules are easy to remove, and removing code is the best refactor.

**Kent Beck's four rules of simple design (in priority order)**

1. Passes the tests.
2. Reveals intent.
3. No duplication.
4. Fewest elements.

**Modern language features worth using**

- Optional chaining `?.`, nullish coalescing `??`, destructuring, spread, template literals.
- `Array.prototype.at`, `toSorted`, `toReversed`, `findLast`, `Object.groupBy` (check your browser targets), `structuredClone`.
- `async/await` with `AbortController` for cancellation; `Promise.allSettled` when failures are independent.
- `Intl.DateTimeFormat`, `Intl.NumberFormat`, `Intl.RelativeTimeFormat` instead of heavy date and number libraries when possible.
- `satisfies`, `as const`, template literal types, and `using` declarations where supported.

**Modern and fast = agile engineering habits**

- **Small batches:** small issues, small MRs, frequent merges. Big batches hide risk.
- **Fast feedback:** quick local dev server, fast lint and tests, fast CI, quick review turnaround.
- **Thin vertical slices:** deliver a working end-to-end slice (UI + API + state) rather than finishing all layers separately. Start with a walking skeleton.
- **Definition of Done:** merged, tested where agreed, documented, accessible, no new lint errors, deployed behind a flag if needed.
- **Continuous refactoring** in small steps instead of a refactor sprint that never comes.
- **Pair or mob** on hard problems; it replaces some review latency.
- **Quality is not the lever, scope is.** Cut scope before cutting quality; the only way to go fast in the long run is to go well.
- **Limit work in progress.** Finish before starting. Context switching is the hidden tax.
- **Make decisions reversible when cheap** (flags, adapters) and spend care on the irreversible ones (data models, public APIs).

**Code smells to recognize**

- God component (does fetching, state, layout and logic), long parameter lists, flag arguments, primitive obsession, shotgun surgery (one change touches 10 files), feature envy, speculative generality, comments that excuse bad code, dumping-ground `utils` files, deep prop drilling, copy-pasted blocks with tiny differences.
