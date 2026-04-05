# OpenSpec 基本用法

## OpenSpec 是什么

一个轻量级的 AI 辅助开发规范框架，核心思路是：**先对齐需求，再写代码**。每个功能变更都有独立的文件夹，包含提案、规格、设计和任务清单。

---
## 安装与初始化

```bash
npm install -g @fission-ai/openspec@latest
cd your-project
openspec init
```

---

## 核心工作流（默认 `core` 模式）

```
/opsx:propose → /opsx:apply → /opsx:archive
```

1. `/opsx:propose <change-name>` — 创建变更，自动生成 `proposal.md`、`specs/`、`design.md`、`tasks.md`
2. `/opsx:apply` — 按 `tasks.md` 逐步实现代码
3. `/opsx:archive` — 归档变更，将 delta specs 合并到主 `specs/` 目录

---

## 目录结构

```
openspec/
├── specs/          # 系统当前行为的"真相来源"
└── changes/        # 每个变更一个文件夹
    └── add-dark-mode/
        ├── proposal.md   # 为什么做、做什么
        ├── design.md     # 技术方案
        ├── tasks.md      # 实现清单（带 checkbox）
        └── specs/        # Delta specs（增/改/删）
```

---

## Delta Specs 格式

```markdown
## ADDED Requirements    # 新增行为 → 归档时追加到主 spec
## MODIFIED Requirements # 修改行为 → 替换主 spec 中对应内容
## REMOVED Requirements  # 删除行为 → 从主 spec 中移除
```

---

## 常用 CLI 命令

```bash
openspec list              # 查看当前活跃变更
openspec show <name>       # 查看变更详情
openspec validate <name>   # 验证 spec 格式
openspec view              # 打开交互式 dashboard
openspec update            # 刷新 AI 指令文件
```

---

## 扩展工作流（可选）

通过 `openspec config profile` 启用，增加更细粒度的控制：

| 命令 | 用途 |
|------|------|
| `/opsx:new` | 创建变更脚手架 |
| `/opsx:continue` | 逐步生成下一个 artifact |
| `/opsx:ff` | 一次性生成所有 artifacts |
| `/opsx:verify` | 验证实现是否符合规格 |
| `/opsx:bulk-archive` | 批量归档多个变更 |

---

## 核心理念

每次变更都有清晰的"为什么、做什么、怎么做、做哪些步骤"，让 AI 和人类在写代码前先对齐。

```
fluid not rigid       — 无阶段门控，灵活迭代
iterative not waterfall — 边学边改，随时更新 artifacts
easy not complex      — 轻量初始化，最小化仪式感
brownfield-first      — 适用于已有项目，不只是新项目
```
