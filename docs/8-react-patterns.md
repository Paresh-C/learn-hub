## 8. React patterns: components and hooks

**Components**

- Keep components small and single-purpose. If you cannot name it simply, it does too much.
- Separate **logic from presentation**: extract custom hooks (`useCheckoutForm`); keep components mostly declarative.
- Prefer **composition over configuration**: use `children` and compound components instead of a dozen boolean props.
- Avoid prop drilling beyond 2-3 levels; use composition, context (low-frequency data), or a state library.
- Do not define components inside other components (they remount every render).
- Use stable, meaningful `key`s, never array indexes for dynamic lists.
- Make components controlled or uncontrolled deliberately, and support both only when needed.

**Hooks**

- Treat `react-hooks/exhaustive-deps` as an error and fix the cause rather than disabling it.
- **You might not need `useEffect`:** derive values during render, handle events in handlers, fetch with a data library. Effects are for syncing with external systems.
- Avoid derived state stored in `useState`; compute it.
- Use `useMemo`/`useCallback` only when profiling or referential equality requires it. With React 19 and the React Compiler much manual memoization is unnecessary.
- Custom hooks start with `use`, return a stable, minimal API, and do one job.
- Clean up subscriptions, timers and listeners in effect cleanup; handle StrictMode double-invocation.
- Use `useReducer` when state transitions are complex; `useRef` for values that must not trigger renders; `useId` for accessible ids.

**Next.js**

- Default to Server Components; add `"use client"` only at the leaves that need interactivity.
- Use `next/image`, `next/font`, `next/link`, and `loading.tsx`, `error.tsx`, `not-found.tsx` boundaries.
- Anything prefixed `NEXT_PUBLIC_` ships to the browser; keep secrets server-side.
