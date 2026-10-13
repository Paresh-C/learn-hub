## 11. Naming: class names, ids, CSS and Tailwind

**Ids**

- Avoid ids for styling. Ids have high specificity and must be unique per page, which breaks reusable components.
- Valid uses: `<label htmlFor>` and `aria-*` relationships, in-page anchors (`#section`), form controls. In React generate them with `useId()` so they stay unique and SSR-safe.
- Do not hardcode an id inside a component that may render twice.

**Class names**

- Name by **purpose, not appearance:** `.alert`, `.card-header`, not `.red-box` or `.left-30`.
- Use **kebab-case** in CSS. Pick one methodology and stay consistent: **BEM** (`block__element--modifier`, e.g. `card__title--large`), CSS Modules, or utility-first (Tailwind).
- State classes: `is-active`, `is-open`, `has-error`. Prefer `data-state` or `aria-*` attributes (`aria-expanded`, `aria-current`) because they double as accessibility and are easy to style.
- Avoid global CSS leaking between components; scope with CSS Modules, a component prefix, or utilities.
- Do not use classes as JavaScript hooks in new code. For tests, prefer accessible queries (role, label, text) and use `data-testid` only as a fallback.
- Keep specificity low and flat. Avoid `!important` and deep selectors (`.a .b .c .d`).

**Tailwind specifics**

- Never build class names dynamically (`bg-${color}-500`); the compiler cannot see them. Use a lookup map of complete class strings.
- Repeated class strings belong in a component or a `cva`/`tailwind-variants` variant, not an `@apply` pile.
- Use `cn()` (`clsx` + `tailwind-merge`) for conditionals and overrides.
- Define tokens (colors, spacing, fonts) in the theme config; avoid arbitrary values like `w-[137px]` unless justified.
- Use the Prettier Tailwind plugin for class ordering. Mobile-first breakpoints. Dark mode via tokens or CSS variables.

**Code naming conventions**

- `PascalCase` for components, types, interfaces and classes. `camelCase` for variables, functions and hooks (`useUserProfile`). `SCREAMING_SNAKE_CASE` for true constants.
- Props that take handlers are `onX` (`onSubmit`); the internal functions are `handleX`.
- Files: match the main export (`UserCard.tsx`) or use kebab-case consistently. Pick one in the team and let ESLint enforce it.
- Booleans: `isLoading`, `hasPermission`, `canEdit`. Collections are plural (`users`), single items singular (`user`).
- Avoid encodings and abbreviations (`btn`, `usrMgr`) unless they are universal (`id`, `url`, `i18n`).
