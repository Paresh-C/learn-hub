## 6. Project structure and architecture

- **Organize by feature/domain, not by file type.** Prefer `features/checkout/{components,hooks,api,types}` over giant top-level `components/`, `hooks/`, `utils/` folders.
- Separate **shared/UI primitives** (design system) from **feature code** from **app/routing code**.
- Enforce dependency direction: features may import shared code, but not each other's internals. Tools: `eslint-plugin-boundaries`, `dependency-cruiser`, or Nx module boundaries.
- Use **barrel files (`index.ts`) sparingly**; they can hurt tree-shaking and slow builds.
- Use **path aliases** (`@/features/...`) instead of `../../../`.
- Colocate tests, styles and stories with the component.
- For larger systems, consider a **monorepo** (pnpm workspaces, Turborepo, Nx) with shared packages.
- A sensible layout:

```
src/
  app/            store setup, providers, router
  features/
    auth/
      api/        RTK Query endpoints (injectEndpoints)
      components/
      hooks/
      slice.ts    only if real client state
      types.ts
  shared/
    ui/           Button, Input, Modal
    lib/          pure helpers
    hooks/
  pages/ or routes/
```
