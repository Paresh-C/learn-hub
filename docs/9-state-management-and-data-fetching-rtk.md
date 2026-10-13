## 9. State management and data fetching (RTK + RTK Query)

**Classify state first**

| Kind | Tool |
| --- | --- |
| Server state (API data) | RTK Query (caching, dedupe, retries, invalidation) |
| URL state (filters, pagination, tabs) | Search params (shareable, back-button friendly) |
| Form state | React Hook Form + Zod |
| Local UI state | `useState` / `useReducer` |
| Shared client state | Redux slice, only if truly needed |

**RTK Query practices**

- **One `createApi` (or a few), many endpoints via `injectEndpoints`**, split per feature.
- **Tags:** `providesTags` on queries, `invalidatesTags` on mutations. Use `{ type: 'Post', id }` plus a `'LIST'` id rather than blanket invalidation.
- Use `transformResponse` to normalize backend shapes at the edge so components never see raw quirks.
- Use `selectFromResult` to avoid re-renders when you need only part of a result. Use `skip` or `skipToken` for conditional queries.
- Centralize error handling in a `baseQuery` wrapper: refresh on 401, normalize errors to one `ApiError` type.
- Export **typed hooks** (`useAppDispatch`, `useAppSelector`) once; never use the raw hooks.
- Use `createSlice` only for true client state. Do not copy server data into slices.
- Use `createEntityAdapter` for normalized collections, `createListenerMiddleware` for side effects, and `createSelector` for memoized derived data.
- If the backend has an OpenAPI spec, use `@rtk-query/codegen-openapi` for typed endpoints.
- **Optimistic updates:** `onQueryStarted` with `updateQueryData`, and `patchResult.undo()` on failure.
- Use `refetchOnFocus`/`refetchOnReconnect` and `pollingInterval` deliberately, and tune `keepUnusedDataFor`.
- Components should not build URLs or parse raw responses; all of that lives in the API layer.
- Always render all four states: loading, error, empty, success.
- Handle race conditions and cancellation (RTK Query does this for you).
