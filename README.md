# GDD Generator

游戏设计文档（GDD）生成器 —— Claude Code Skill。

## 两种模式

| 模式 | 说明 | 触发 |
|------|------|------|
| **逆向 GDD** | 反推已有游戏的设计文档，学 GDD 怎么写 | "逆向 xx 游戏"、"拆解 xx" |
| **正向 GDD** | 三阶段对话，从大白话到可执行 MVP GDD | "/gdd"、"帮我写游戏设计" |

## 示例

`examples/sample-gdd.md` — 《杀戮尖塔》逆向 GDD 范例，按 8 章模板完整拆解。

## 安装

全局 skill，放在 `~/.claude/skills/gdd-generator/` 即可在所有项目中调用。
