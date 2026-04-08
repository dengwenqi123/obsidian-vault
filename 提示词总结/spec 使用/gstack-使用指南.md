# gstack 使用指南

## 简介

gstack 是一套给 AI agent 用的结构化工作流技能集，由 Y Combinator CEO Garry Tan 开源。每个技能对应一个专业角色（CEO 审查、工程经理、设计师、QA 等），通过 SKILL.md 文件定义。核心理念是把 Claude Code 变成一个虚拟工程团队。

## 安装

### 前置条件

- [Git](https://git-scm.com/)
- [Bun](https://bun.sh/) v1.0+
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code)

### 全局安装（推荐）

```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack
cd ~/.claude/skills/gstack && bun install && ./setup
```

### 团队模式

```bash
cd ~/.claude/skills/gstack && ./setup --team

# 在项目中初始化
cd <你的项目>
~/.claude/skills/gstack/bin/gstack-team-init required
git add .claude/ CLAUDE.md && git commit -m "require gstack"
```

### 指定其他 AI Agent

```bash
./setup --host kiro      # Kiro
./setup --host codex     # OpenAI Codex CLI
./setup --host cursor    # Cursor
./setup --host factory   # Factory Droid
```

### 卸载

```bash
~/.claude/skills/gstack/bin/gstack-uninstall
```

## 工作流总览

gstack 的技能按 sprint 流程排列：

**想清楚 → 做计划 → 写代码 → 审查 → 测试 → 发布 → 回顾**

每个技能的输出会自动喂给下一个技能，形成完整链条。

## 命令速查

### 一、规划阶段（写代码之前）

| 命令 | 角色 | 用途 |
|------|------|------|
| `/office-hours` | YC Office Hours | 起点。把模糊想法变成清晰需求，会追问你 6 个关键问题 |
| `/plan-ceo-review` | CEO | 从产品角度审视方案，找到"10 星体验" |
| `/plan-eng-review` | 工程经理 | 锁定架构、数据流、边界情况、测试计划 |
| `/plan-design-review` | 高级设计师 | 设计维度打分（0-10），说明 10 分长什么样 |
| `/plan-devex-review` | DX 负责人 | 开发者体验审查，追踪 TTHW（Time To Hello World） |
| `/autoplan` | 审查流水线 | 一条命令自动跑 CEO → 设计 → 工程审查 |


### 二、编码阶段（安全护栏）

| 命令 | 角色 | 用途 |
|------|------|------|
| `/careful` | 安全守卫 | 破坏性命令警告（rm -rf、DROP TABLE、force-push） |
| `/freeze <目录>` | 编辑锁 | 锁定只能改指定目录，防止误改其他模块 |
| `/guard` | 全面保护 | `/careful` + `/freeze` 同时激活 |
| `/unfreeze` | 解锁 | 移除目录锁定 |

### 三、审查阶段（写完代码后）

| 命令 | 角色 | 用途 |
|------|------|------|
| `/review` | Staff Engineer | 代码审查，找 CI 过了但生产会挂的 bug |
| `/cso` | 首席安全官 | OWASP Top 10 + STRIDE 威胁模型审计 |
| `/codex` | 第二意见 | 用 OpenAI Codex 做独立代码审查（跨模型对比） |
| `/design-review` | 设计工程师 | 设计审计 + 修复循环，atomic commit |
| `/devex-review` | DX 测试员 | 实际测试你的开发者上手体验 |

### 四、调试阶段

| 命令 | 角色 | 用途 |
|------|------|------|
| `/investigate` | 调试专家 | 系统化根因排查，不查清原因不动手修 |

### 五、测试阶段

| 命令 | 角色 | 用途 |
|------|------|------|
| `/qa <URL>` | QA 负责人 | 真实浏览器测试，发现 bug 就修，自动生成回归测试 |
| `/qa-only <URL>` | QA 报告员 | 只报告 bug，不改代码 |
| `/benchmark` | 性能工程师 | 页面加载时间、Core Web Vitals、资源大小基线 |

### 六、发布阶段

| 命令 | 角色 | 用途 |
|------|------|------|
| `/ship` | 发布工程师 | 跑测试 → 审查 → 推送 → 开 PR，一条命令 |
| `/land-and-deploy` | 发布工程师 | 合并 PR → 等 CI → 部署 → 验证生产健康 |
| `/canary` | SRE | 部署后监控，盯控制台错误和性能回退 |
| `/document-release` | 技术写作 | 自动更新 README、CHANGELOG 等文档 |

### 七、浏览器相关

| 命令 | 角色 | 用途 |
|------|------|------|
| `/browse` | QA 工程师 | 真实 Chromium 浏览器，~100ms/命令 |
| `/setup-browser-cookies` | 会话管理 | 从 Chrome/Arc/Brave/Edge 导入 cookies |
| `/open-gstack-browser` | GStack 浏览器 | 带侧边栏、反检测、自动模型路由的浏览器 |
| `/pair-agent` | 多 Agent 协调 | 让多个 AI agent 共享同一个浏览器 |

### 八、设计相关

| 命令 | 角色 | 用途 |
|------|------|------|
| `/design-consultation` | 设计伙伴 | 从零构建完整设计系统 |
| `/design-shotgun` | 设计探索 | 生成 4-6 个 AI 设计变体，对比选择 |
| `/design-html` | 设计工程师 | 把设计稿变成可发布的 HTML/CSS |

### 九、回顾与维护

| 命令 | 角色 | 用途 |
|------|------|------|
| `/retro` | 工程经理 | 周回顾，统计提交数、代码行数、测试覆盖率 |
| `/retro global` | 工程经理 | 跨所有项目和 AI 工具的全局回顾 |
| `/learn` | 记忆 | 管理 gstack 跨会话学到的项目知识 |
| `/gstack-upgrade` | 自更新 | 升级 gstack 到最新版本 |
| `/health` | 健康检查 | 技能健康看板 |

## 实战场景

### 场景一：从零开发新功能

```
/office-hours          → 梳理需求
/plan-ceo-review       → 产品视角审视
/plan-eng-review       → 锁定技术方案
（写代码）
/review                → 代码审查
/qa https://staging... → 浏览器测试
/ship                  → 发布
```

### 场景二：线上 bug 排查

```
/investigate           → 系统化排查根因
（修复）
/qa https://staging... → 验证修复
/review + /ship        → 审查并上线
```

### 场景三：重构高风险模块

```
/guard                 → 开启保护（careful + freeze）
（重构代码）
/review                → 审查改动
/qa                    → 浏览器验证
/unfreeze              → 解除限制
/ship                  → 发布
```

### 场景四：安全审计

```
/cso                   → OWASP + STRIDE 审计
/codex                 → 跨模型第二意见
（修复安全问题）
/review + /ship        → 审查并上线
```

### 场景五：周五发版

```
/review                → 最后审查
/qa-only               → 只报告不改
/ship                  → 发布
/document-release      → 更新文档
/retro                 → 周回顾
```

## 研发工程师推荐入门顺序

1. `/review` — 每次提交前跑一下，最常用
2. `/ship` — 替代手动 git push + 开 PR
3. `/investigate` — 下次遇到 bug 试试
4. `/careful` — 操作生产环境时开着
5. `/office-hours` — 做新功能前先聊聊

用熟以上 5 个后，再逐步加入 `/qa`、`/autoplan`、`/cso`。

## 构建命令

```bash
bun install              # 安装依赖
bun test                 # 跑测试（免费，<5s）
bun run build            # 生成文档 + 编译二进制
bun run gen:skill-docs   # 从模板重新生成 SKILL.md
bun run skill:check      # 所有技能的健康看板
```

## 注意事项

- SKILL.md 是从 `.tmpl` 模板生成的，要改内容得改模板文件
- `/ship` 会自动调用 `/document-release` 更新文档
- `/qa` 每修一个 bug 都会自动生成回归测试
- gstack 会跨会话学习你的项目模式（通过 `/learn` 管理）
- 遥测默认关闭，需要手动 opt-in
