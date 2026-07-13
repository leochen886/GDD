# GDD Generator Skill — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 创建一个双模式 GDD（游戏设计文档）生成 Skill，支持逆向反推已有游戏和正向三阶段对话写 GDD。

**Architecture:** 3 个 Markdown 文件组成——SKILL.md（主流程指令）、mvp-gdd.md（输出模板）、sample-gdd.md（写作范例）。纯对话驱动，无外部依赖。

**Tech Stack:** Markdown（Skill 文件格式）

---

## 文件规划

| 文件 | 路径 | 职责 |
|------|------|------|
| SKILL.md | `.claude/skills/gdd-generator/SKILL.md` | Skill 入口，含元信息、模式路由、三阶段流程指令、设计原则 |
| mvp-gdd.md | `.claude/skills/gdd-generator/templates/mvp-gdd.md` | GDD 输出模板，正逆向共用，定义 8 章结构 |
| sample-gdd.md | `.claude/skills/gdd-generator/examples/sample-gdd.md` | 范例 GDD（以《杀戮尖塔》为例），给 AI 做写作参考 |

---

### Task 1: 创建目录结构

**Files:**
- Create: `.claude/skills/gdd-generator/` (directory)
- Create: `.claude/skills/gdd-generator/templates/` (directory)
- Create: `.claude/skills/gdd-generator/examples/` (directory)

- [ ] **Step 1: 创建目录**

```bash
mkdir -p .claude/skills/gdd-generator/templates
mkdir -p .claude/skills/gdd-generator/examples
```

- [ ] **Step 2: 验证目录结构**

```bash
ls -la .claude/skills/gdd-generator/
```
Expected: templates/ 和 examples/ 两个子目录存在

---

### Task 2: 创建 GDD 输出模板

**Files:**
- Create: `.claude/skills/gdd-generator/templates/mvp-gdd.md`

- [ ] **Step 1: 编写 MVP GDD 模板**

模板内容包括：
- 8 章的固定结构
- 每章的子项占位符
- 末尾的 MVP 范围清单（✅ ❌ 🔮）格式

- [ ] **Step 2: 验证文件已创建且内容完整**

```bash
wc -l .claude/skills/gdd-generator/templates/mvp-gdd.md
```
Expected: 文件存在，行数合理

---

### Task 3: 创建范例 GDD

**Files:**
- Create: `.claude/skills/gdd-generator/examples/sample-gdd.md`

- [ ] **Step 1: 以《杀戮尖塔》为例编写完整 MVP GDD**

用逆向模式的方法论，按模板填入：
- 8 章完整内容
- 标注 🔵 已知事实 / 🟡 推测设计
- 展示一份高质量 GDD 应该长什么样

- [ ] **Step 2: 验证文件已创建且内容完整**

```bash
wc -l .claude/skills/gdd-generator/examples/sample-gdd.md
```
Expected: 文件存在，内容覆盖全部 8 章

---

### Task 4: 创建 SKILL.md 主文件

**Files:**
- Create: `.claude/skills/gdd-generator/SKILL.md`

- [ ] **Step 1: 编写 SKILL.md**

包含以下模块：

**元信息（YAML frontmatter）：**
- name: gdd-generator
- description: 双模式游戏设计文档生成器

**模式路由逻辑：**
- 如何判断用户意图（关键词检测：逆向/反推/已有游戏名 → 逆向模式）
- 默认正向模式

**模式 1 · 逆向指令：**
- 流程步骤
- 标注规范（🔵🟡）
- 阅读指南模板
- 输出后引导用户尝试正向模式

**模式 2 · 正向指令（三阶段）：**
- Phase 1 速描：6 项提取 + 速描卡模板
- Phase 2 搭骨架：大纲展示 → 逐章对话引导
  - 每章的引导问题集
  - 对话节奏规则（一问一答、关键决策给选项）
  - 跳过/深度控制机制
- Phase 3 打磨：一致性检查清单 + 输出规范

**MVP 铁律 & 设计原则：**
- "够 MVP 就停"的提醒时机
- 翻译而非创作
- 一问一答
- 全中文

**参考引用：**
- 引用 templates/mvp-gdd.md 作为输出模板
- 引用 examples/sample-gdd.md 作为写作范例

- [ ] **Step 2: 验证文件已创建且内容完整**

```bash
head -5 .claude/skills/gdd-generator/SKILL.md
```
Expected: 文件以 YAML frontmatter 开头

---

### Task 5: 验证 Skill 可用

- [ ] **Step 1: 在 Claude Code 中触发 Skill**

在对话中输入 `/gdd` 或 "帮我写GDD"，验证 Skill 被正确加载

- [ ] **Step 2: 测试逆向模式**

输入 "逆向一下《吸血鬼幸存者》"，验证：
- Skill 正确识别逆向意图
- 按模板输出 GDD
- 标注 🔵🟡
- 附阅读指南

- [ ] **Step 3: 测试正向模式**

输入 "帮我写个GDD，我想做一个XX游戏"，验证：
- Skill 正确进入正向模式
- Phase 1 输出速描卡
- Phase 2 展示大纲并逐章引导
- MV 铁律被执行

- [ ] **Step 4: 根据测试结果修调 SKILL.md**

如果对话节奏、模板、引导问题有问题，调整 SKILL.md 的指令
