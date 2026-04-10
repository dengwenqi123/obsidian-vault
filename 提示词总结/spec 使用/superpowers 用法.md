需求没问清就写！

边界没拆清就写！

用例没先写就写！

改完没检查就发！

这是当前AI编程经常遇到的问题。最近很火的Superpowers又是什么？能不能解决这个问题呢？

## 是什么

![[../../attachment/Pasted image 20260410101202.png]]
**Superpowers 是一套完整的软件开发工作流，建立在一组可组合的 skills 之上，并通过初始化指令确保 agent 真正去使用这些 skills。**

最后看起来很快，实际上返工更多。

Superpowers 解决的，就是这类问题。

它不是靠一句更强的 prompt 去赌模型状态，而是把整套流程拆成一批可调用的技能：

**核心工作流（7 个）：**

-   • `brainstorming`：先把需求问清楚，再给方案和设计
    
-   • `writing-plans`：把实现计划拆成可执行的小任务
    
-   • `test-driven-development`：严格走 RED-GREEN-REFACTOR
    
-   • `subagent-driven-development`：把任务派给独立子代理执行
    
-   • `requesting-code-review`：每个阶段都做复核
    
-   • `using-git-worktrees`：隔离分支和工作区，避免互相踩
    
-   • `finishing-a-development-branch`：最后决定合并、发 PR 还是保留分支

**容易被忽略但同样重要的另外 7 个：**

-   • `systematic-debugging`：4 阶段根因分析（观察 → 模式识别 → 假设验证 → 实施修复），铁律是"没有完成根因调查，不允许提出修复方案"。官方数据称系统化调试 15-30 分钟解决问题，随机修复要 2-3 小时
    
-   • `verification-before-completion`：在宣布"完成"之前，必须证明修复确实生效，防止"我觉得修好了"的自欺欺人
    
-   • `dispatching-parallel-agents`：面对 3 个以上独立故障时，每个问题域派一个 agent 并行调查，比串行快一个数量级
    
-   • `executing-plans`：按批次推进计划，保留人工检查点，和 `subagent-driven-development` 是两种不同的执行策略
    
-   • `receiving-code-review`：不只是发起 review，还规范了如何接收和响应 review 反馈
    
-   • `using-superpowers`：元技能，教 agent 如何发现和使用其他 skill，是整个框架的引导入口
    
-   • `writing-skills`：把 TDD 应用到 skill 本身的编写上——先写压力测试场景，观察 agent 失败，再写最小化的 SKILL.md，然后堵住 agent 可能的"合理化借口"
    

说白了，Superpowers 想做的不是“让 AI 一口气写完代码”。而是让 AI 像一个流程严格、习惯良好的工程团队那样工作。

## 它和普通提示词最大的区别

普通提示词，通常只解决一件事：“这一次，怎么让模型表现好一点。”

Superpowers 解决的是另一件事：“以后每一次，怎么让 agent 按同一套规则工作。”

它的核心结构，其实只有两层。

第一层是 **skills**。

这些 skill 本质上是仓库里的 `SKILL.md` 文件，是一份份面向 agent 的操作手册。

有的强调流程，有的强调测试，有的强调 review，有的强调并行协作。

第二层是 **bootstrap / discovery**。

也就是让宿主 agent 在任务开始前，先检查有没有相关 skill，再决定怎么做，而不是先凭直觉行动。

这件事看上去简单，意义却非常大。因为只要 agent 先“查 skill，再行动”，它的行为风格就会稳定下来。

`using-superpowers` 这个核心 skill 甚至把规则写得非常硬：

**如果有哪怕 1% 的概率某个 skill 适用，就必须先调用 skill。**

但它也没有越界。同一个 skill 里写得很清楚：**用户显式指令始终优先。**

也就是说，Superpowers 很强，但不夺权。

## 工作流程

先看官方 README 里的基本工作流。

**第一步是 `brainstorming`。**

在你要做新功能、改行为、做设计时，它要求 agent 先理解项目上下文，再一个问题一个问题把需求问清楚，然后给出 2 到 3 种方案与 trade-off，最后形成设计稿并让你确认。

这一步的价值非常高。很多 AI 编程翻车，不是实现差，而是一开始就做错题。

**第二步是 `writing-plans`。**

这个 skill 非常强调“计划必须细到一个没有上下文、品味一般、还不太爱测试的工程师也能执行”。

所以它要求每个任务都写清楚文件路径、测试方法、命令、预期输出，甚至要求任务粒度缩到 2 到 5 分钟。

**第三步是 `test-driven-development`。**

它的口径极其强硬：

`NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST`

换句话说，没有先看到失败测试，就不允许写生产代码。如果先写了代码，再补测试，按它的规则是要删掉重来。

**第四步是 `subagent-driven-development` 或 `executing-plans`。**

前者更像“分任务给子代理逐个实现，再逐个复核”。后者更像“按批次推进，保留人工检查点”。

**第五步是 `requesting-code-review`。**

它不是等到最后才 review，而是鼓励阶段性 review。每完成一个任务，就先做规格符合性检查，再做代码质量检查，防止问题一路滚到最后。

**最后一步是 `finishing-a-development-branch`。**

把测试、分支处理、PR 或 merge 决策都纳入流程。

这说明它追求的不是“写出代码”，而是“把开发闭环走完”。

如果你以前觉得 agent 经常像一个“聪明但毛躁的实习生”，那 Superpowers 干的事，其实就是给这个实习生配上一套非常严格的团队 SOP。

## 怎么安装

**Superpowers 没有单一安装方式，必须按宿主平台来。**

如果你用的是 `Claude Code`，当前 README 给出的做法是先添加 marketplace，再安装插件：

```
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace
```

装完以后，README 还建议直接用 `/help` 检查是否已经出现这些命令：

```
/help

# 应该能看到：
# /superpowers:brainstorm
# /superpowers:write-plan
# /superpowers:execute-plan
```



## 最佳实践

Superpowers 最好的用法，不是背一堆命令。而是学会把任务交给它的方式，改成“目标 + 约束 + 边界”，而不是“立刻给我代码”。

比如你要做一个新功能，不要一上来就说：“把退款功能写出来。” 更好的说法是：

```
先不要写代码。
请用 superpowers 的 brainstorming 流程帮我把需求问清楚，
给出 2-3 种方案和推荐方案。

目标：给现有支付模块增加退款能力
约束：不能改数据库结构；必须兼容旧接口；一周内上线
成功标准：支持全额退款、部分退款、重复请求幂等
```

这样一来，agent 会先进入需求澄清和设计阶段。后面的计划、TDD、子代理执行和 review，才有可靠基础。

如果你是在修 bug，也不要直接说“修一下”。更适合的姿势是：

```
先不要改代码。
请用 systematic-debugging 找 root cause，再给我最小修复方案。

现象：支付回调偶发重复入账
线索：只在重试场景出现
要求：必须给出验证修复是否生效的步骤
```

这才是 Superpowers 的强项。它更像一个“把 agent 拉回正确工程流程”的框架，而不是一个帮你偷懒的捷径。
![[../../attachment/Pasted image 20260410101251.png]]