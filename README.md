# my-pi

Personal fork of [earendil-works/pi](https://github.com/earendil-works/pi) with custom enhancements.

Built from source at `~/code/SelfBuild`, linked globally via `npm link`.

## Changelog

### 2026-06-06

**Mouse click cursor positioning**
- `packages/tui/src/terminal.ts` — Enable SGR mouse mode (`?1002h` + `?1006h`) on start, disable on stop/drain
- `packages/tui/src/tui.ts` — Parse SGR mouse sequences (`ESC[<B;X;YM`), dispatch to focused component; recursive search for nested containers to find focused component's screen position
- `packages/tui/src/components/editor.ts` — `handleMouse()` converts screen coordinates to editor cursor position via `buildVisualLineMap()`, supports wide characters (CJK/emoji)

**`/exit` command**
- `packages/coding-agent/src/modes/interactive/interactive-mode.ts` — `/exit` as alias for `/quit`

## Build & Install

```bash
cd ~/code/SelfBuild
npm run build              # Build all packages
# If linked globally, changes take effect immediately
```

## Sync with Upstream

```bash
git remote add upstream https://github.com/earendil-works/pi.git  # once
git fetch upstream
git merge upstream/main
npm run build
```
