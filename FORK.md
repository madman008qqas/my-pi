# my-pi — 个人 fork

[earendil-works/pi](https://github.com/earendil-works/pi) 的个人 fork。

源码构建，全局链接受理：`/usr/local/bin/pi` → `packages/coding-agent/dist/cli.js`

## 改动记录

### 2026-11-12 — 同步上游 1.5.2

从 `0.78.1` 合并上游至 `1.5.2`（3424 个 commit）。

**移除的自研功能（上游已内置且实现更好）**

- 鼠标点击定位光标：上游 `editor.ts` 的 `handleMouse(event: TuiMouseEvent)` 已支持点击定位、拖拽选中复制、自动补全列表鼠标操作、grapheme 级宽字符处理，本地实现已废弃。
- `/exit` 退出命令：上游 `interactive-mode.ts:3465` 已内置 `text === "/quit" || text === "/exit"`，无需本地改动。

### 2026-06-06

**鼠标点击定位光标**（已于 2026-11-12 废弃，改用上游实现）

iTerm2 终端中可以鼠标点击输入框任意位置移动光标，支持中文等宽字符。

- `packages/tui/src/terminal.ts` — 启动时开启 SGR 鼠标追踪模式（`?1002h` + `?1006h`），退出/挂起时关闭
- `packages/tui/src/tui.ts` — 解析 SGR 鼠标序列（`ESC[<B;X;YM`），递归搜索嵌套 Container 找到焦点组件的屏幕位置，分发点击事件
- `packages/tui/src/components/editor.ts` — 新增 `handleMouse()`，通过 `buildVisualLineMap()` 将屏幕坐标转换为编辑器光标位置，正确处理宽字符

**`/exit` 退出命令**（已于 2026-11-12 废弃，改用上游实现）

`/exit` 作为 `/quit` 的别名，输入即可退出 pi。

- `packages/coding-agent/src/modes/interactive/interactive-mode.ts` — 匹配 `/exit`

## 构建

```bash
cd /Users/madman/studywork/code/my-pi
npm install --ignore-scripts
npm run build
# /usr/local/bin/pi 已软链到 dist/cli.js，build 后直接生效
```

## 同步上游

```bash
git fetch upstream
git merge upstream/main
npm install --ignore-scripts
npm run build
```

冲突处理约定：`README.md` 与 `packages/tui/**` 一律取上游（`git checkout --theirs`）。
