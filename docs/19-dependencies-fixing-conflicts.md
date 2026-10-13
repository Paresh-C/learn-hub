## 19. Dependencies and fixing conflicts

**Common conflict types**

- **Peer dependency errors** (npm `ERESOLVE`): a package requires a different version of React, TypeScript, or another peer than you installed.
- **Duplicate versions:** two copies of React or `@types/react` cause hook errors or type mismatches.
- **Lockfile merge conflicts** after two branches change dependencies.
- **Version drift:** developers on different Node or package-manager versions get different installs.
- **Transitive vulnerabilities** in packages you do not directly control.
- **ESM vs CJS** incompatibilities, and tooling mismatches (e.g. TypeScript version newer than `typescript-eslint` supports).

**Diagnosis workflow**

1. Read the error fully; it names the package, the required range, and what was found.
2. Find who requires what: `npm ls <pkg>`, `pnpm why <pkg>`, or `yarn why <pkg>`.
3. Check the offending package's `peerDependencies` and release notes. Is there a newer version that supports your setup?
4. Pick the least risky fix (below), apply it, run lint, type-check, tests, and the app.
5. Document anything unusual (why an override exists, and when it can be removed).

**Fix options (best to worst)**

1. **Upgrade** the package (or the thing it depends on) to a compatible version.
2. **Align versions** across the project so only one copy exists (`npm dedupe`, `pnpm dedupe`).
3. **Replace** an unmaintained package with a maintained alternative.
4. **Overrides:** `overrides` (npm), `pnpm.overrides` (pnpm), `resolutions` (Yarn) to force a version of a transitive dependency. Add a comment and a ticket to remove it later.
5. **Patch** a package temporarily (`pnpm patch`, `patch-package`) and open an upstream issue or PR.
6. **`--legacy-peer-deps` / `--force`:** last resort; record the reason, because it hides real incompatibilities.

**Lockfile conflicts**

- Never hand-edit a lockfile. Resolve conflicts in `package.json` first.
- Then take the target branch's lockfile (`git checkout origin/main -- pnpm-lock.yaml`) and run the install to regenerate it with your changes.
- Commit the regenerated lockfile.

**Prevention**

- One package manager, declared via the `packageManager` field (with Corepack) and `engines`; pin Node with `.nvmrc`.
- Commit the lockfile; use `pnpm install --frozen-lockfile` (or `npm ci`) in CI.
- Understand semver: major = breaking, minor = features, patch = fixes. Decide on a range policy (caret, tilde, exact) and apply it consistently.
- Update often in small batches (Renovate groups), read changelogs and migration guides, and upgrade one major at a time.
- Remove unused packages (`knip`, `depcheck`). Check size and license before adding a dependency.
- Do not delete `node_modules` and the lockfile as the first move; it can hide the problem and change many versions at once.
- In monorepos, watch hoisting and workspace version ranges.
