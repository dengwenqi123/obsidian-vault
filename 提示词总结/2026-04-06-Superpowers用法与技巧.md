---
title: Superpowers 基本用法与使用技巧
date: 2026-04-06
tags:
  - ai-generated
  - superpowers
  - coding-agent
  - 工作流
source: ai-generated
created: 2026-04-06T00:00:00
---

# Superpowers 基本用法与使用技巧

## 📦 Superpowers 是什么

Superpowers 是一套**完整的 AI 编程代理工作流系统**，由一系列可组合的 "skills"（技能）构成。它让你的编程 AI 代理（如 Claude Code、Cursor、Codex、Gemini CLI 等）不再盲目写代码，而是遵循结构化的软件工程流程。

核心理念：**先理解、再设计、后实现**，而非上来就写代码。

---

## 🔧 安装方式

| 平台 | 命令 |
|------|------|
| **Claude Code**（官方市场） | `/plugin install superpowers@claude-plugins-official` |
| **Claude Code**（社区市场） | `/plugin marketplace add obra/superpowers-marketplace` → `/plugin install superpowers@superpowers-marketplace` |
| **Cursor** | `/add-plugin superpowers` |
| **Gemini CLI** | `gemini extensions install https://github.com/obra/superpowers` |
| **Codex / OpenCode** | 让 AI 读取安装文档 URL 自动安装 |

---

## 🔄 核心工作流（7 步流水线）

Superpowers 的技能会**自动触发**，你不需要手动调用：

### 1️⃣ Brainstorming（头脑风暴）

- **触发时机**：任何创建功能、构建组件的请求
- **作用**：不直接写代码，先通过苏格拉底式提问理清需求，探索 2-3 种方案，生成设计文档
- **关键规则**：必须得到用户批准后才能开始实现

### 2️⃣ Using Git Worktrees（Git 工作树）

- 设计通过后自动创建**隔离的 Git 分支和工作区**
- 确保干净的测试基线

### 3️⃣ Writing Plans（编写计划）

- 把设计拆分成**2-5 分钟的小任务**
- 每个任务包含：精确的文件路径、完整代码、验证步骤
- 强调 TDD、YAGNI、DRY 原则

### 4️⃣ Subagent-Driven Development（子代理驱动开发）

- 为每个任务派遣**独立的子代理**执行
- 执行后进行**两阶段审查**：规格合规性 → 代码质量
- AI 可以自主工作数小时而不偏离计划

### 5️⃣ Test-Driven Development（测试驱动开发）

- 铁律：**没有失败的测试就不能写生产代码**
- 严格的 RED → GREEN → REFACTOR 循环
- 如果先写了代码再写测试？**删除代码，从头来过**

### 6️⃣ Requesting Code Review（代码审查）

- 任务之间自动发起审查
- 关键问题会**阻断进度**

### 7️⃣ Finishing a Development Branch（完成分支）

- 所有任务完成后：验证测试 → 提供 4 个选项（合并 / PR / 保留 / 丢弃）→ 清理工作树

---

## 🛠 技能库一览

| 类别 | 技能 | 用途 |
|------|------|------|
| **测试** | `test-driven-development` | RED-GREEN-REFACTOR 循环 |
| **调试** | `systematic-debugging` | 4 阶段根因分析，禁止盲猜修复 |
| | `verification-before-completion` | 确保问题真的修好了 |
| **协作** | `brainstorming` | 设计精炼 |
| | `writing-plans` | 实现计划编写 |
| | `executing-plans` | 批量执行 + 人工检查点 |
| | `dispatching-parallel-agents` | 并发子代理工作流 |
| | `subagent-driven-development` | 快速迭代 + 两阶段审查 |
| **Git** | `using-git-worktrees` | 并行开发分支 |
| | `finishing-a-development-branch` | 合并/PR 决策流程 |
| **元技能** | `writing-skills` | 创建新技能 |
| | `using-superpowers` | 技能系统入门 |

---

## 💡 使用技巧

### 1. 你不需要记住任何技能名称

技能会**自动触发**。当你说"帮我构建 X 功能"时，brainstorming 技能自动启动；说"修复这个 bug"时，debugging 技能自动介入。

### 2. 理解优先级

- **你的指令** > Superpowers 技能 > 系统默认行为
- 如果你在 `CLAUDE.md` 中说"不用 TDD"，技能会尊重你的选择

### 3. 对简单任务也不要跳过设计

Superpowers 的哲学：**即便是 todo list 这样简单的项目也需要走设计流程**（设计可以很简短，但不能省略）

### 4. 调试时遵循铁律

- **先找根因，再修复**
- 禁止"先试试这个修复看看行不行"的做法
- 越紧急越要冷静、系统化排查

### 5. 更新插件保持最新

```bash
/plugin update superpowers
```

### 6. 验证安装成功

开启新会话，问 AI"帮我规划这个功能"或"帮我调试这个问题"，如果 AI 自动调用了相关技能，说明安装成功。

---

## 🎯 核心哲学

- **测试先行** — 永远先写测试
- **系统化 > 随意** — 流程胜过猜测
- **降低复杂度** — 简洁为王
- **证据 > 声明** — 验证后再宣布成功

---

> [!info] 来源
> 基于 [superpowers](https://github.com/obra/superpowers) v5.0.7 文档整理，作者 Jesse Vincent。
