## 29. VS Code extensions and shortcuts

**Extensions worth installing** (fewer is better; extensions run with your permissions, so check the publisher and install counts)

| Area | Extension |
| --- | --- |
| Code quality | ESLint, Prettier - Code formatter, EditorConfig for VS Code |
| Errors | Error Lens (inline errors), Pretty TypeScript Errors |
| Git and GitLab | GitLens, GitLab Workflow (official; MRs, issues, pipelines in the editor), Git Graph |
| React and TS | ES7+ React/Redux/React-Native snippets, Auto Rename Tag, Path Intellisense, Import Cost |
| Styling | Tailwind CSS IntelliSense, CSS Peek |
| API | Thunder Client or REST Client |
| Notes and docs | Markdown All in One, Markdown Preview Mermaid Support, Code Spell Checker, Todo Tree, Better Comments |
| Testing (later) | Vitest, Playwright Test for VS Code |
| Collaboration | Live Share |
| Misc | DotENV, indent-rainbow, Bookmarks |
| AI agents | Claude Code and Cline extensions, if your company allows them |

Browser extensions: React Developer Tools, Redux DevTools (RTK integrates with it), axe DevTools, Lighthouse.

**Recommended settings**

- `editor.formatOnSave: true` and `editor.codeActionsOnSave` with `source.fixAll.eslint`.
- `files.autoSave: afterDelay`, `editor.linkedEditing: true`, `editor.stickyScroll.enabled: true`.
- `typescript.preferences.importModuleSpecifier: non-relative` (use path aliases) and use the workspace TypeScript version.
- Commit `.vscode/settings.json` and `.vscode/extensions.json` (recommendations) so the team shares them.
- Emmet in JSX: `div.card>h2+p` then Tab. Snippet `rafce` creates an arrow-function component with an export.

**Essential shortcuts** (Windows/Linux; on Mac use Cmd for Ctrl and Option for Alt; a few differ)

| Action | Shortcut |
| --- | --- |
| Command palette | Ctrl+Shift+P |
| Quick open file | Ctrl+P |
| Go to line / symbol in file / symbol in workspace | Ctrl+G / Ctrl+Shift+O / Ctrl+T |
| Search in files / replace in files | Ctrl+Shift+F / Ctrl+Shift+H |
| Find / replace in file | Ctrl+F / Ctrl+H |
| Toggle sidebar / terminal / explorer | Ctrl+B / Ctrl+\` / Ctrl+Shift+E |
| Split editor | Ctrl+\\ |
| Switch editor tabs | Ctrl+Tab, or Ctrl+PageUp/PageDown |
| Close tab / reopen closed tab | Ctrl+W / Ctrl+Shift+T |
| Go to definition / peek definition | F12 / Alt+F12 |
| Find all references | Shift+F12 |
| Rename symbol (all usages) | F2 |
| Quick fix and refactor actions | Ctrl+. |
| Navigate back / forward | Alt+Left / Alt+Right |
| Select next occurrence / all occurrences | Ctrl+D / Ctrl+Shift+L |
| Add cursor | Alt+Click, or Ctrl+Alt+Up/Down |
| Move line up/down | Alt+Up / Alt+Down |
| Copy line up/down | Shift+Alt+Up / Shift+Alt+Down |
| Delete line | Ctrl+Shift+K |
| Toggle line comment / block comment | Ctrl+/ / Shift+Alt+A |
| Insert line below / above | Ctrl+Enter / Ctrl+Shift+Enter |
| Select line | Ctrl+L |
| Format document | Shift+Alt+F |
| Trigger suggestion / parameter hints | Ctrl+Space / Ctrl+Shift+Space |
| Fold / unfold all | Ctrl+K Ctrl+0 / Ctrl+K Ctrl+J |
| Jump to matching bracket | Ctrl+Shift+\\ |
| Problems panel / next problem | Ctrl+Shift+M / F8 |
| Source control / extensions / debug | Ctrl+Shift+G / Ctrl+Shift+X / Ctrl+Shift+D |
| Debug: start, breakpoint, step over, step into | F5, F9, F10, F11 |
| Zen mode | Ctrl+K Z |
| Keyboard shortcuts editor | Ctrl+K Ctrl+S |

**Terminal tools that pair well:** `ripgrep` (`rg`) for fast search, `fzf` for fuzzy finding, `jq` for JSON, `lazygit` for a git TUI, plus git aliases for your common commands.
