## 5. CI/CD and linter

- **ESLint** (flat config) + **Prettier** + `typescript-eslint`, one shared config. Format on save.
- Useful ESLint plugins: `eslint-plugin-react-hooks`, `jsx-a11y`, `import` (or `eslint-plugin-boundaries`), `eslint-plugin-unicorn` (selectively), `eslint-plugin-testing-library` (when tests arrive), `@tanstack/eslint-plugin-query` (if used).
- Set `react-hooks/exhaustive-deps` to error. Ban `@ts-ignore` (use `@ts-expect-error` with a reason). Warn on `console.log`.
- **EditorConfig** and shared `.vscode/settings.json` and `extensions.json`.
- Pin Node via `.nvmrc` or `engines`; use one package manager and one lockfile (pnpm recommended).
- **Pipeline order** (fast checks first): install (cached), lint, type-check, test, build, bundle-size or performance check, optional E2E.
- Roll out strict lint rules gradually: introduce a rule as a warning, fix, then promote to error. Do not fail the whole team's builds with 2,000 new errors.
- Starter `.gitlab-ci.yml`:

```yaml
stages: [verify, build]

workflow:
  rules:
    - if: $CI_PIPELINE_SOURCE == 'merge_request_event'
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH

default:
  image: node:22
  cache:
    key:
      files: [pnpm-lock.yaml]
    paths: [.pnpm-store]
  before_script:
    - corepack enable
    - pnpm config set store-dir .pnpm-store
    - pnpm install --frozen-lockfile

lint:
  stage: verify
  script: pnpm lint

typecheck:
  stage: verify
  script: pnpm tsc --noEmit

test:
  stage: verify
  script: pnpm test --run
  allow_failure: true # remove once tests are stable

build:
  stage: build
  script: pnpm build
```

- Use **preview deployments** per MR (GitLab review apps) so reviewers can click through changes.
- Use **feature flags** (Unleash is built into GitLab, or GrowthBook/LaunchDarkly) to decouple deploy from release.
- Automate releases and changelogs (semantic-release, Changesets) once commits follow Conventional Commits.
- Make local setup one command (`pnpm install && pnpm dev`) and document it.
