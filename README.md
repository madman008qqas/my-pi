# my-pi

[earendil-works/pi](https://github.com/earendil-works/pi) 的个人 fork，加入自定义增强功能。

源码构建，全局链接：`~/code/SelfBuild` → `npm link`

## 改动记录

### 2026-06-06

**鼠标点击定位光标**

iTerm2 终端中可以鼠标点击输入框任意位置移动光标，支持中文等宽字符。

- `packages/tui/src/terminal.ts` — 启动时开启 SGR 鼠标追踪模式（`?1002h` + `?1006h`），退出/挂起时关闭
- `packages/tui/src/tui.ts` — 解析 SGR 鼠标序列（`ESC[<B;X;YM`），递归搜索嵌套 Container 找到焦点组件的屏幕位置，分发点击事件
- `packages/tui/src/components/editor.ts` — 新增 `handleMouse()`，通过 `buildVisualLineMap()` 将屏幕坐标转换为编辑器光标位置，正确处理宽字符

**`/exit` 退出命令**

`/exit` 作为 `/quit` 的别名，输入即可退出 pi。

- `packages/coding-agent/src/modes/interactive/interactive-mode.ts` — 匹配 `/exit`

## 构建

```bash
cd ~/code/SelfBuild
npm run build
# 已通过 npm link 全局链接，build 后直接生效
```

## 同步上游

```bash
git remote add upstream https://github.com/earendil-works/pi.git  # 首次
git fetch upstream
git merge upstream/main
npm run build
```
