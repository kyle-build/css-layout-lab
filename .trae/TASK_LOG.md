## 2026-04-22T11:58:10.477Z - Add HTML prettier rules
- Goal: Introduce Prettier HTML formatting rules (tabs)
- Summary: Added .prettierrc.json with HTML overrides (useTabs/tabWidth/printWidth); added package.json scripts; added scripts/task-log.mjs for task logging
- Repro: pnpm run format:html (after pnpm i)

## 2026-04-22T12:03:00.468Z - Enable format on save
- Goal: Ctrl+S auto-format HTML in VSCode
- Summary: Added .vscode/settings.json enabling formatOnSave and using Prettier as HTML formatter
- Repro: Open src/cascade/cascade.html, press Ctrl+S; file formats via Prettier
