## 7. TypeScript practices

- Turn on `strict: true`. If the codebase is not strict yet, migrate incrementally (`strictNullChecks` first, then `noImplicitAny`), or use a per-folder tsconfig.
- Avoid `any`. Use `unknown` plus narrowing. Prefer `@ts-expect-error` with an explanation over `@ts-ignore`.
- Prefer `type` for unions and compositions, `interface` for extendable object contracts. Be consistent.
- Use **discriminated unions** for state: `{status: 'loading'} | {status: 'success', data: T} | {status: 'error', error: Error}`. Impossible states become unrepresentable.
- **Validate at runtime boundaries** (API responses, forms, URL params, `localStorage`) with Zod or Valibot, and infer types from schemas. TypeScript types are erased at runtime.
- Use `satisfies`, `as const`, and utility types (`Pick`, `Omit`, `Partial`, `Required`, `Record`, `ReturnType`, `Awaited`) instead of duplicating types.
- Avoid type assertions (`as Foo`) unless justified; never `as unknown as Foo` to silence errors.
- Use **branded types** for ids that must not be mixed (`UserId` vs `OrderId`) when mix-ups are likely.
- Prefer `readonly` and immutable shapes. Use exhaustive `switch` with a `never` check on unions.
- Share types with the backend via generated clients (OpenAPI codegen, GraphQL Codegen, tRPC).
- Type component props explicitly; export prop types when reused. Avoid `React.FC` unless the team prefers it.
