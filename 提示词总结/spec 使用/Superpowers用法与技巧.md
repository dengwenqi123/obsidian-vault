---
title: Superpowers 基本用法与使用技巧
date: 2026-04-06
tags:
  - ai-generated
  - superpowers
  - coding-agent
  - 工作流
  - brainstorming
  - 提示词编写
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

## 🚀 开发功能时的实战流程

### 第一步：直接告诉 AI 你想做什么

不需要任何特殊命令，用自然语言描述需求即可。Superpowers 会自动接管，开始 brainstorming 流程。

### 第二步：回答 AI 的提问（头脑风暴阶段）

AI 不会直接写代码，而是会：
1. 先检查项目上下文（文件、文档、最近提交）
2. 逐个提问，理解真实需求
3. 提出 2-3 个方案，分析优劣，给出推荐
4. 分段展示设计方案，逐段确认

> [!tip] 不要急着说"赶紧开始写代码"。这个阶段越认真，后面返工越少。

### 第三步：确认设计文档

AI 会把设计写入 spec 文件，然后请你审核。满意就说"通过"，不满意就提修改。

### 第四步：自动创建隔离工作区

设计通过后，AI 自动创建 Git worktree（独立分支），主分支完全不受影响。

### 第五步：生成实现计划

AI 把设计拆分成一系列小任务（每个 2-5 分钟），保存到 `docs/superpowers/plans/` 目录。

### 第六步：说"开始执行"

AI 进入子代理驱动开发模式：为每个任务派遣独立子代理，严格 TDD，每个任务完成后两轮审查。AI 可自主工作数小时不偏离计划。

### 第七步：完成与集成

所有任务完成后：运行全量测试 → 提供 4 个选项（合并 / PR / 保留 / 丢弃）。

**你实际需要做的**：描述需求 → 回答提问 → 确认设计 → 说开始 → 选择合并方式。其余全部自动化。

---

## 🔌 Plugin vs Skills：选哪个？

**Plugin 是交付方式，Skills 是内容本身**，不是二选一的关系。

```
Plugin（插件）= 安装壳 + 自动发现 + 会话钩子
   └── Skills（技能）= 实际的工作流规则（SKILL.md 文件）
```

### 对比

| | 通过 Plugin 安装 | 手动使用 Skills |
|---|---|---|
| 安装 | 一条命令搞定 | 克隆仓库 + 手动配置 |
| 技能发现 | ✅ 自动 | ❌ 需手动引用 |
| 更新 | `/plugin update` | `git pull` |
| 自动触发 | ✅ AI 自动调用 | ⚠️ 需手动告诉 AI |
| 适用场景 | 完整工作流自动化 | 只用个别技能 |

**建议**：直接装 Plugin。只有平台不支持插件或只需个别技能时，才手动使用 Skills。

### 个人技能可覆盖插件技能

优先级：项目技能 > 个人技能 > Superpowers 插件技能

---

## 🧩 只使用部分 Skills

完全可以！在 `CLAUDE.md` 中声明即可：

```markdown
## Superpowers 使用偏好

### 启用的技能
- test-driven-development
- systematic-debugging

### 禁用的技能
- brainstorming（我自己做设计）
- writing-plans（我自己写计划）
- subagent-driven-development（不使用子代理）
```

### 推荐组合

| 组合 | 技能 | 适合 |
|------|------|------|
| **只要质量保障** | TDD + debugging + verification | 有自己的设计流程 |
| **只要设计+计划** | brainstorming + writing-plans | 自己写代码 |
| **跳过子代理** | 全部除了 subagent-driven-dev | 每步自己确认 |
| **全自动** | 全部（默认） | 信任 AI |

### 技能独立性

| 独立可用 ✅ | 有前置依赖 ⚠️ |
|---|---|
| test-driven-development | writing-plans（最好先有设计）|
| systematic-debugging | subagent-driven-development（需要计划）|
| verification-before-completion | executing-plans（需要计划）|
| brainstorming | finishing-a-development-branch（需要 worktree）|
| requesting-code-review | |

---

## ✍️ 如何写高质量的 Brainstorming 提示词

### 核心原则

你提供"什么"和"为什么"，AI 来问"怎么做"：

```
❌  "用 React + Redux 搭一个带 WebSocket 的通知系统"
✅  "我需要一个通知系统，用户要能实时收到消息"
```

技术选型是 brainstorming 阶段 AI 该帮你探索的，不是你预先定死的。

### 高质量提示词的四要素

#### 1. 明确目的（Purpose）

```markdown
✅ "我的 SaaS 产品需要一个账单系统，用户能看到历史消费、下载发票"
❌ "做一个账单页面"  ← 太模糊
```

#### 2. 说明约束（Constraints）

```markdown
✅ "后端必须用 Python/FastAPI，数据库用现有的 PostgreSQL，不能用付费服务"
❌ "随便用什么技术都行"  ← 浪费时间探索你用不了的方案
```

#### 3. 定义成功标准（Success Criteria）

```markdown
✅ "成功标准：3 秒内加载通知列表，支持已读/未读筛选，移动端桌面端都可用"
❌ "做得好看一点"  ← 不可衡量
```

#### 4. 提供现有上下文（Context）

```markdown
✅ "项目在 /src 下，已有用户认证模块。数据模型在 /src/models/"
❌ "你自己看代码吧"  ← AI 需要方向
```

### 提示词模板

```markdown
## 我想做什么
[1-2 句话描述功能目的]

## 背景
- 功能给 [谁] 用
- 当前痛点是 [什么问题]
- 现有系统已有 [哪些相关模块]

## 约束条件
- 技术栈：[语言/框架/数据库]
- 性能要求：[如有]
- 不能做的事：[如有]

## 成功标准
- [ ] [可验证的条件 1]
- [ ] [可验证的条件 2]
- [ ] [可验证的条件 3]

## 我的倾向（可选）
[有偏好可以说，但不要限死]
```

### 实战示例

#### ❌ 差的提示词

> "帮我做一个聊天功能"

#### ✅ 好的提示词

> "我在做一个项目管理工具，需要给团队成员添加项目内聊天功能。
>
> **背景**：目前讨论在微信群，上下文容易丢失。希望讨论能和项目任务关联。
>
> **约束**：后端 Node.js + MongoDB，前端 Vue 3。用户数不超过 50 人/项目。
>
> **成功标准**：任务详情页能发消息、支持 @提及、消息关联任务、离线回来能看未读数。
>
> **不确定的地方**：该用 WebSocket 还是轮询，请帮我分析。"

### 进阶技巧

| 技巧 | 说明 | 示例 |
|------|------|------|
| **说出不确定的地方** | AI 最擅长帮你分析犹豫不决的部分 | "我不确定要不要支持离线同步" |
| **大项目先整体后展开** | 主动引导拆分 | "先从用户管理开始设计，其他后面再来" |
| **提供反例** | 说"不想要什么"比"想要什么"更精确 | "不要像 Notion 那样太复杂" |
| **预先给选项** | 加速 AI 的提问过程 | "方案 A 存 MongoDB，方案 B 加 Redis 层" |
| **声明经验水平** | AI 调整问题深度 | "前端不太熟，需要更详细的指导" |

### 常见反模式

| 反模式 | 问题 | 改进 |
|--------|------|------|
| 一次提太多需求 | AI 和你都会迷失 | 拆成子项目，一次一个 |
| 预定义技术方案 | 跳过方案探索 | 说约束，不说具体方案 |
| 只说"做个 XX" | 太模糊，问答轮次多 | 至少加目的+约束+标准 |
| 催促写代码 | 破坏设计流程 | 信任过程 |
| 追求完美设计 | 过度设计 | YAGNI，够用就行 |

---

> [!info] 来源
> 基于 [superpowers](https://github.com/obra/superpowers) v5.0.7 文档整理，作者 Jesse Vincent。
