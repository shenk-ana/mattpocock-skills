<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

# 面向真正工程师的 Skills

[English](./README.md) | **中文**

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

我每天都在用的 agent skills，用来做真正的工程，而不是 vibe coding。

开发真正的应用很难。GSD、BMAD、Spec-Kit 这类方法试图通过接管整个流程来帮忙。可一旦它们接手，你就失去了控制权，流程里的 bug 也更难排查。

这些 skills 被设计成小块、好改、可组合。它们能配合任何模型。背后是几十年的工程经验。尽管改。改成你自己的。享受这个过程。

如果想跟上这些 skills 的更新，以及我之后新写的内容，可以加入我的 newsletter，现在大约有 60,000 名开发者：

[订阅 Newsletter](https://www.aihero.dev/s/skills-newsletter)

## 安装（30 秒搞定）

两条入口，两种理念。**[Claude Code 插件](https://code.claude.com/docs/en/plugins)** 把整套 skills 装成受管、只读的包，我一发布就会跟着更新，所以你是在订阅，而不是 fork。**[skills.sh](https://skills.sh/mattpocock/skills)** 把可编辑的 skill 文件复制进你的项目，方便你自己改、变成自己的。选一条就好：两条都装，等于每份 skill 会出现两次。

### 1. 拿到 skills

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude plugins install mattpocock-skills
```

或者，在会话里运行：

```
/plugin install mattpocock-skills
```

它在 Claude Code 的官方 marketplace 里，所以不用先添加任何东西，更新也会自动到来。

</details>

<details>
<summary><strong>Codex 以及其他 agents</strong></summary>

```bash
npx skills@latest add mattpocock/skills
```

选择你想要的 skills，以及要安装到哪些编码 agents 上。**安装器会让你挑选要带走的 skills，请确保其中包含 `setup-matt-pocock-skills`。**

原生的 Codex 插件已在路线图上（见 [`.agents/adr/0002-ship-as-a-claude-code-plugin.md`](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)）。

</details>

<details>
<summary><strong>喜欢自己改的人</strong></summary>

在任意 agent 上用同一个安装器，包括 Claude Code：

```bash
npx skills@latest add mattpocock/skills
```

它会把 skills 写成你仓库里普通的、归你所有、可以编辑的文件。不会在你背后自动更新；想拉我的最新改动时，运行 `npx skills update`。

</details>

### 2. 运行 `/setup-matt-pocock-skills`

在你的 agent 里，每个仓库跑一次。它会：

- 问你想用哪种 issue tracker（GitHub、Linear，或本地文件）
- 问你分诊工单时用哪些 labels（`/triage` 会用到 labels）
- 问你要把我们创建的文档存到哪里

### 3. 搞定，可以开工了。

## 为什么要有这些 Skills

我写这些 skills，是为了修掉我在 Claude Code、Codex 和其他编码 agent 上反复看到的失败模式。

### #1：Agent 没按我想的做

> "没有人一开始就完全清楚自己想要什么"
>
> David Thomas 与 Andrew Hunt，《[The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)》

**问题**。软件开发里最常见的失败，是对齐失败。你以为对方知道你要什么。然后你看到做出来的东西，才发现它根本没理解你。

AI 时代也是同一件事。你和 agent 之间有沟通缺口。解决办法是开一场 **追问环节**：让 agent 就你要做的东西，向你提出细致的问题。

**解决办法** 是使用：

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md)：非代码场景
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md)：和 [`/grill-me`](./skills/productivity/grill-me/SKILL.md) 一样，但多了更多好处（见下文）

这是我最常用的 skills。它们帮你在动手之前先和 agent 对齐，并认真想清楚这次改动。每次要做改动时，都用它们。

### #2：Agent 话太多

> 有了通用语言，开发者之间的对话和代码中的表达都来自同一套领域模型。
>
> Eric Evans，《[Domain-Driven-Design](https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)》

**问题**：项目刚开始时，开发者和他们为之构建软件的人（领域专家）通常说的不是同一种语言。

我和我的 agents 也感到同样的张力。Agents 通常被丢进一个项目，再边走边猜行话。于是它们用 20 个词去说 1 个词就能说清的事。

**解决办法** 是一份共享语言。那是一份文档，帮 agents 解码项目里的行话。

<details>
<summary>
示例
</summary>

这是我 `course-video-manager` 仓库里的一份 [`CONTEXT.md`](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md)。哪一句更好读？

- **改前**："课程某个章节里的一节课被做成 'real' 时出了问题（也就是在文件系统里分到一个位置）"
- **改后**："物化级联出了问题"

这种简洁会在之后的每一次会话里回本。

</details>

这已经做进 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md)。它还是一场追问，但会帮你和 AI 建立共享语言，并把难讲清的决策写进 ADR。

这有多强，很难用一句话说清。它可能是这个仓库里最酷的手法。试试就知道。

> [!TIP]
> 共享语言除了少说话，还有很多好处：
>
> - **变量、函数和文件的命名一致**，都用这份共享语言
> - 因此，agent **更容易在代码库里找路**
> - agent **花在思考上的 token 也更少**，因为它手里有更短的语言

### #3：代码根本跑不起来

> "始终迈出小而审慎的步子。反馈的速度就是你的速度上限。永远不要接下过大的任务。"
>
> David Thomas 与 Andrew Hunt，《[The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)》

**问题**：假设你和 agent 已经对齐了要做什么。可 agent _还是_ 交出垃圾，怎么办？

该看你的反馈环了。如果没有关于代码实际怎么跑的反馈，agent 就是在盲飞。

**解决办法**：你需要那一套常见的反馈环：静态类型、浏览器访问，以及自动化测试。

对自动化测试来说，红-绿-重构循环至关重要。也就是 agent 先写一个失败的测试，再把测试修绿。这能给 agent 稳定的反馈，写出来的代码会好很多。

我做了一个 **[`/tdd`](./skills/engineering/tdd/SKILL.md) skill**，可以插进任何项目。它鼓励红-绿-重构，并给 agent 足够的指引，说明什么样的测试好、什么样的差。

调试方面，我还做了 **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)**。它把最佳调试实践收进一个有纪律的循环，按阶段把关。

### #4：我们堆出了一团泥球

> "每天都为系统设计投资。"
>
> Kent Beck，《[Extreme Programming Explained](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0321278658)》

> "最好的模块是深的。它们让大量功能可以通过一个简单的接口访问。"
>
> John Ousterhout，《[A Philosophy Of Software Design](https://www.amazon.co.uk/Philosophy-Software-Design-2nd/dp/173210221X)》

**问题**：大多数用 agents 做出来的应用又复杂又难改。Agents 能大幅加快写代码的速度，于是也加速了软件熵增。代码库变复杂的速度，前所未有。

**解决办法** 是一种对 AI 开发相当激进的新态度：认真对待代码的设计。

这一点写进了这些 skills 的每一层：

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md) 在写 spec 之前，会先问你要动哪些模块

更关键的是，[`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md) 会扫描代码库，找出可以加深的机会，再把候选交给你。我建议每隔几天就在你的代码库上跑一次。它是勘察，不是救援：在真正老的代码库上，它会找到真实的候选，但不会替你把泥球拆开。

### 小结

软件工程的基本功，比以往任何时候都更重要。这些 skills 是我尽力把这些基本功收成可重复实践的结果，帮你交出职业生涯里最好的应用。享受这个过程。

## 参考

它们按一个维度拆开：谁能调用它们。**用户触发（User-invoked）** 的 skills 只有你亲手输入时才能到达（例如 `/grill-me`），它们的工作是编排。**模型触发（Model-invoked）** 的 skills 可以由你调用，也可以在任务对得上时由 agent 自动伸手去拿；它们装着可复用的纪律。用户触发的 skill 可以调用模型触发的 skills，但绝不会再调用另一个用户触发的 skill。

### Engineering

我每天用来写代码的 skills。

**用户触发**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)**：问哪条 skill 或流程适合你现在的情况。本仓库用户触发 skills 的路由器。
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)**：追问环节，同时构建项目的领域模型，打磨术语，并当场更新 `CONTEXT.md` 和 ADR。
- **[triage](./skills/engineering/triage/SKILL.md)**：按分诊角色的状态机推动 issues。
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)**：扫描代码库里可以加深的机会，做成可视化 HTML 报告，再就你选中的那一条展开追问。
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)**：为工程类 skills 配置本仓库（issue tracker、分诊 labels、领域文档布局）。用其他工程 skills 之前，每个仓库跑一次。
- **[to-spec](./skills/engineering/to-spec/SKILL.md)**：把当前对话收成一份 spec，并发布到 issue tracker。不再追问，只综合你们已经讨论过的内容。
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)**：把任何计划、spec 或对话拆成一组示踪弹工单，每张都声明自己的阻塞边，写成本地文件里的文本，或写成真实 tracker 上的原生阻塞链接。
- **[implement](./skills/engineering/implement/SKILL.md)**：按 spec 或一组工单描述的工作来实现，在事先约好的接缝处驱动 `/tdd`，提交前用 `/code-review` 收尾。
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)**：规划一大块工作（超出一次 agent 会话装得下的量），在 issue tracker 上做成决策工单的共享地图，一次解开一张，直到通往目的地的路变清楚。

**模型触发**

- **[prototype](./skills/engineering/prototype/SKILL.md)**：做一个用完即弃的原型，用来回答设计问题：状态/逻辑问题用一份可分享的 HTML 文件，或在同一条路由上做几套风格迥异、可切换的 UI 变体。
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)**：针对难解 bug 和性能回退的有纪律诊断循环：先搭一个会在这个 bug 上变红的反馈环 → 最小化 → 假设 → 埋点 → 修复 → 回归测试。
- **[research](./skills/engineering/research/SKILL.md)**：对照高可信的一手来源调查一个问题，把发现写成带引用的 Markdown 文件放进仓库，作为后台 agent 运行。
- **[tdd](./skills/engineering/tdd/SKILL.md)**：带红-绿-重构循环的测试驱动开发。一次做一个垂直切片，用来做功能或修 bug。
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)**：主动构建并打磨项目的领域模型：用术语表检验用词，用边界场景做压力测试，并当场更新 `CONTEXT.md` 和 ADR。
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)**：设计深模块的共享纪律和词汇：大量行为藏在小接口后面，放在干净的接缝上，并通过该接口可测。
- **[code-review](./skills/engineering/code-review/SKILL.md)**：从某个固定点起，对 diff 做双轴审查：**Standards**（是否遵循仓库的编码标准，外加 Fowler 坏味道基线？）和 **Spec**（是否忠实实现了源 issue/spec？），作为并行 sub-agents 运行，互不污染。
- **[resolving-merge-conflicts](./skills/engineering/resolving-merge-conflicts/SKILL.md)**：逐块处理进行中的 git merge 或 rebase 冲突，按追溯到各方一手来源的意图来解决，然后把操作做完（绝不 `--abort`）。
- **[wizard](./skills/engineering/wizard/SKILL.md)**：生成一个交互式 bash 向导，带人走完只有人能做的步骤：开通基础设施、配置凭证或 CI secrets、走过不熟的第三方控制台，或跑一次性迁移/切换。

### Productivity

通用工作流工具，不限定写代码。

**用户触发**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)**：就一份计划或设计被不停追问，直到设计树的每个分支都被解开。
- **[handoff](./skills/productivity/handoff/SKILL.md)**：把当前对话压成一份交接文档，好让另一个 agent 接着做。
- **[teach](./skills/productivity/teach/SKILL.md)**：分多轮会话教用户一项新 skill 或概念，把当前目录当作有状态的教学工作区。
- **[to-questionnaire](./skills/productivity/to-questionnaire/SKILL.md)**：把一个你自己答不了的决策，收成一份给那个能答的人的 Markdown 问卷，可以异步填，也可以开会一起填。它追问的是发送本身（给谁、你要拿回什么），不是主题。
- **[wait-what](./skills/productivity/wait-what/SKILL.md)**：消息没听懂的那一刻就开火。agent 用你缺的上下文，按你 `CONTEXT.md` 里的词汇，用白话重新讲一遍。

**模型触发**

- **[grilling](./skills/productivity/grilling/SKILL.md)**：就一份计划、决策或想法不停追问用户，直到设计树的每个分支都被解开。这是 `grill-me`、`grill-with-docs`、`triage`、`wayfinder` 和 `improve-codebase-architecture` 背后可复用的访谈原语。
- **[writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md)**：给 agents 写文档：skills、AGENTS.md/CLAUDE.md，以及任何 agent 会通过指针找到的文档。
