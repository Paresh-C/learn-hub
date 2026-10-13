## 17. Accessibility (a11y)

- Use **semantic HTML** first (`button`, `nav`, `main`, `label`, `ul`); ARIA is a last resort. Do not use `div onClick` as a button.
- Everything must work with the keyboard: visible focus, logical tab order, no focus traps (except in modals, which must trap and restore focus). Manage focus on route changes.
- Labels for inputs, alt text for images, sufficient color contrast (WCAG AA), do not convey meaning by color alone, respect `prefers-reduced-motion`.
- Announce dynamic changes with `aria-live` or `role='alert'` (errors, toasts).
- Tooling: `eslint-plugin-jsx-a11y`, axe DevTools, `jest-axe` or Playwright axe, and manual checks with a screen reader (NVDA, VoiceOver).
- If your product supports RTL languages (such as Persian), test layout direction with logical CSS properties (`margin-inline-start`, `padding-inline`), `dir` attributes, and mirrored icons.
