# Frontend Code Quality Changes

## Summary

Added frontend code quality tooling (Prettier for formatting, ESLint for linting) and applied consistent formatting across all frontend files.

---

## New Files

### `frontend/package.json`
Declares the frontend as a Node project and wires up quality check scripts:
- `npm run format` — formats all JS/CSS/HTML with Prettier (write mode)
- `npm run format:check` — checks formatting without modifying files (CI-safe)
- `npm run lint` — lints `script.js` with ESLint
- `npm run lint:fix` — auto-fixes ESLint issues
- `npm run quality` — runs both `format:check` and `lint` (full check)
- `npm run quality:fix` — runs both `format` and `lint:fix` (full auto-fix)

Dev dependencies: `prettier@^3.3.3`, `eslint@^8.57.0`

### `frontend/.prettierrc`
Prettier configuration:
- 4-space indentation, 100-char print width
- Single quotes, trailing commas (ES5), LF line endings

### `frontend/.prettierignore`
Excludes `node_modules/` from Prettier.

### `frontend/.eslintrc.json`
ESLint configuration targeting browser ES2021:
- Errors on `no-undef`, `eqeqeq` (strict equality), `no-var`, `curly`
- Warns on `no-unused-vars`, `prefer-const`
- Registers `marked` as a known read-only global (loaded via CDN)

### `scripts/check-frontend.sh`
Shell script to run all frontend quality checks from the repo root:
```bash
# Check only (exits non-zero if anything fails):
./scripts/check-frontend.sh

# Auto-fix formatting and lint issues:
./scripts/check-frontend.sh --fix
```

---

## Modified Files

### `frontend/script.js`
Applied Prettier-consistent formatting:
- Single quotes throughout
- Trailing commas on multi-line function arguments and object literals
- Explicit `curly` braces on all `if` bodies
- Arrow function parentheses around single parameters
- Consistent blank lines between logical sections

### `frontend/style.css`
Applied Prettier-consistent formatting:
- Each CSS selector on its own line (e.g. `*,\n*::before,\n*::after`)
- `h1`, `h2`, `h3` font-size rules expanded to separate blocks
- `@keyframes bounce` selector list expanded (`0%,\n80%,\n100%`)
- `.no-courses, .loading, .error` selector list expanded
- Removed stale inline comment on `.course-titles` block
- Consistent blank lines between rule blocks

### `frontend/index.html`
Applied Prettier-consistent formatting:
- `<!doctype html>` lowercased
- Self-closing void elements (`<meta ... />`, `<link ... />`, `<input ... />`)
- 4-space indentation throughout
- Long `<button>` attributes broken onto separate lines
- `<script>` tags moved inside `<body>` closing tag for consistency
