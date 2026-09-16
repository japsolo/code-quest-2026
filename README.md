# Code Quest - Frontend App

Single-page React 19 + TypeScript + Vite site.

## Prerequisites

- [Node.js](https://nodejs.org) 20 or newer
- [pnpm](https://pnpm.io) (install with `corepack enable` or `npm install -g pnpm`)

## Getting started

1. Clone the repo and move into it:
   ```bash
   git clone https://github.com/japsolo/code-quest-2026.git
   cd code-quest-2026
   ```
2. Install dependencies:
   ```bash
   pnpm install
   ```
   This also runs the `prepare` script, which installs the Git hooks so `.husky/pre-commit` runs on every commit (see [Git hooks with Husky](#git-hooks-with-husky) below).
3. Start the dev server:
   ```bash
   pnpm dev
   ```
   The app will be available at `http://localhost:5173`.

## Other scripts

```bash
pnpm build     # typecheck (tsc -b) then build for production into dist/
pnpm preview   # serve the production build locally to sanity-check it
```

## Linting and formatting with Biome

This project uses [Biome](https://biomejs.dev) for linting and formatting, configured in `biome.json`.

```bash
pnpm check       # lint + format check, no writes
pnpm check:fix   # lint + format, writing fixes
```

Also, you will need `.vscode/settings.json` in your local, to allow *auto-format* on *save-file*. `settings.json` looks like this:

```json
{
  "editor.defaultFormatter": "biomejs.biome",
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.biome": "always",
    "source.organizeImports.biome": "always"
  },
  "[typescript]": {
    "editor.defaultFormatter": "biomejs.biome"
  },
  "[typescriptreact]": {
    "editor.defaultFormatter": "biomejs.biome"
  },
  "[javascript]": {
    "editor.defaultFormatter": "biomejs.biome"
  },
  "[javascriptreact]": {
    "editor.defaultFormatter": "biomejs.biome"
  },
  "[json]": {
    "editor.defaultFormatter": "biomejs.biome"
  },
  "js/ts.preferences.importModuleSpecifier": "non-relative"
}
```

Feel free to add any rules you need. Take care provided they don't drastically alter the codebase!

## Git hooks with Husky

This project uses [Husky](https://typicode.github.io/husky) to run checks automatically before each commit.

- Husky is installed as a dev dependency and wired up via the `prepare` script (`"prepare": "husky"` in `package.json`), which runs automatically after `pnpm install` and creates the Git hooks.
- The hook itself lives at `.husky/pre-commit` and currently runs:
  ```bash
  pnpm run check
  pnpm run typecheck
  ```
  These correspond to the `check` (`biome check .`) and `typecheck` (`tsc -b`) scripts in `package.json`.
- If a commit is rejected, run `pnpm check:fix` to auto-fix lint/format issues, resolve any remaining TypeScript errors reported by `pnpm build`, then commit again.
