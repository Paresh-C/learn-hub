## 14. Error handling, fallbacks and error boundaries

**Know the error types and where each is handled**

| Error | Example | Handle with |
| --- | --- | --- |
| Render error | `undefined.map` inside a component | Error boundary |
| Event handler error | Throw inside `onClick` | try/catch in the handler (boundaries do not catch these) |
| Async error | Rejected promise, failed fetch | try/catch, RTK Query error state, or `showBoundary` |
| Network/API error | 401, 403, 404, 500, timeout | RTK Query `error`, global middleware, user message |
| Validation error | Bad form input | Field-level messages (Zod + React Hook Form) |
| Programmer error | Wrong assumption or bug | Fail loudly in dev, log in prod, fix the cause |

**What error boundaries do and do not catch**

- They catch errors thrown while **rendering**, in lifecycle methods, and in constructors of components below them.
- They do **not** catch errors in event handlers, asynchronous code (timeouts, promises), server-side rendering, or errors thrown inside the boundary itself.
- Boundaries are class-based; use the `react-error-boundary` package so you get a function-friendly API.

```tsx
import { ErrorBoundary, type FallbackProps } from 'react-error-boundary';

function ErrorFallback({ error, resetErrorBoundary }: FallbackProps) {
  return (
    <div role='alert'>
      <h2>Something went wrong</h2>
      <p>Try again, or contact support if it keeps happening.</p>
      <button onClick={resetErrorBoundary}>Try again</button>
    </div>
  );
}

<ErrorBoundary
  FallbackComponent={ErrorFallback}
  onError={(error, info) => reportError(error, info.componentStack)}
  resetKeys={[userId]}   // auto-reset when these change
>
  <UserProfile userId={userId} />
</ErrorBoundary>
```

- To send an async error into the nearest boundary, use `useErrorBoundary()` and call `showBoundary(error)`.
- React 19 adds root options `onCaughtError`, `onUncaughtError` and `onRecoverableError` on `createRoot` for central logging.

**Where to place boundaries (layers)**

1. **Root:** last resort, shows a full-page fallback and a reload option.
2. **Route/page level:** a broken page does not take down navigation and layout.
3. **Widget level:** isolate risky or third-party parts (charts, editors, feeds) so one failure leaves the rest usable.
4. **Around lazy components:** combine with `Suspense` (loading) and `ErrorBoundary` (failure, such as a chunk that failed to load).

**Designing good fallbacks**

- Say what happened in plain language, what the user can do (retry, go back, contact support), and show a short error id or reference for support.
- Never show stack traces, raw server messages, or internal ids to users.
- Keep the fallback small, dependency-free, and unlikely to fail itself.
- Offer partial degradation: skeletons while loading, **stale data** when a refetch fails, an offline banner, and helpful empty states.
- Provide consistent 404, 403 and 500 pages.

**RTK Query specifics**

- Every query hook exposes `isLoading`, `isFetching`, `isError`, `error`, `data`. Render all states.
- The error type is `FetchBaseQueryError | SerializedError`; normalize it in a `baseQuery` wrapper into one app-level `ApiError` with a code, message and status.
- Global handling with middleware: `isRejectedWithValue(action)` to show a toast for failed mutations, redirect on 401, and so on.
- Use retry (`retry` utility) for flaky idempotent requests only; never auto-retry non-idempotent mutations blindly.
- Queries show inline errors near the content; mutations usually show toasts or form-level errors.

**General rules**

- Never swallow errors silently (`catch {}`). Handle, log, or rethrow.
- Validate external data with `safeParse` (Zod) at boundaries and handle the failure branch.
- Add global listeners for `window.onerror` and `unhandledrejection` and send them to your error tracker (Sentry or similar) with release and source maps.
- Map error codes to translated messages instead of showing backend strings.
- Log context (route, user id hash, action) but never PII or secrets.
- Next.js: `error.tsx` (segment) and `global-error.tsx` (root) are the framework's boundaries.
