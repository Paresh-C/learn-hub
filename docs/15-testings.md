## 15. Testing strategy

If you have no tests yet, aim for **high-value logic first**, not coverage numbers.

**The testing trophy (priority)**

1. **Static:** TypeScript and ESLint catch a huge class of bugs for free.
2. **Unit:** pure utilities, reducers, selectors, validators, permission and pricing logic.
3. **Integration/component:** React Testing Library with a real store and mocked network; test behavior as the user sees it.
4. **E2E:** Playwright (or Cypress) for 2-3 critical flows only (login, checkout, core CRUD).
5. **Visual regression:** optional, if UI consistency matters.

**Getting started**

- Tooling: Vitest, React Testing Library, `@testing-library/user-event`, MSW (Mock Service Worker). Add the `test` job to CI first as allowed-to-fail, then make it blocking.
- Start with pure logic: utilities, formatters, validators, slices and selectors.
- Test RTK Query with MSW: mock the network, render with a real store, assert on UI states (loading, success, error, refetch after invalidation).
- **Bug-driven rule:** every bug fix ships with a test that fails before the fix.
- **Before refactoring** risky legacy code, write characterization tests that pin current behavior.
- Skip snapshot spam and implementation details (internal state, private functions, exact class names).

```tsx
// test/renderWithStore.tsx
export function renderWithStore(ui: ReactElement, preloadedState?: Partial<RootState>) {
  const store = setupStore(preloadedState);
  return { store, ...render(<Provider store={store}>{ui}</Provider>) };
}
```

**Good test habits**

- Structure: Arrange, Act, Assert. One behavior per test; name it as a sentence (`shows an error when login fails`).
- Query by role, label and text. Use `findBy` for async, `getBy` for present, `queryBy` for absent.
- Keep tests deterministic: control time, randomness and network.
- Coverage is a signal, not a target. Gate on no regression instead of an arbitrary percentage.
- TDD is optional but excellent for pure logic: write the failing test, make it pass, refactor.
