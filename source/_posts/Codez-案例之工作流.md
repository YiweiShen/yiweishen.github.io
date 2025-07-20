---
title: Codez 使用案例之工作流
date: 2025-07-20 16:36:20
tags:
---

最近被 Agentic Coding 这套思路迷住了，于是搞了个小项目 [Codez](https://github.com/YiweiShen/codez)，直接嵌在 GitHub Actions 里运行 Codex，效果还不错的。比如这样的工作流：

**先讨论，然后拆解成 tickets，最后各个击破**

像是这个代码重构的需求：[Parent Ticket](https://github.com/YiweiShen/codez/issues/304)

![Parent Ticket](/img/codez001.jpg)

---

## 第一步：先抛出需求

我在 issue 里写清楚了想做的事，包括要探讨的点、相关的背景资料。这个 issue 的标题和内容，agent 会当成初始 prompt 的一部分。

然后我直接在评论里触发 agent：

```bash
/codex             # 用关键词唤醒 agent
--no-pr            # 加个 flag，不要直接生成 PR
--fetch            # 把链接里的内容先抓下来，方便 agent 离线使用
https://google.github.io/styleguide/tsguide.html  # 提供相关文档，有助于 agent 做判断
```

![](/img/codez002.jpg)

Agent 就开始工作啦。即便它在运行时是断网的，但通过 context（比如我们的代码、给的链接、issue 内容），它还是给出了几条挺靠谱的初步思路。

## 第二步：自动拆解成 actionable 的 tickets

接着我又触发了一次 agent，这次是让它生成一系列 issue：

![](/img/codez003.jpg)

```bash
/codex
--create-issues    # 生成 JSON，再用 GitHub API 创建 issues
--full-history     # 把整个 issue 的所有评论都作为上下文
```

注意一下：这些 flag 是对“当前这条评论”生效的，之前的那些不会继承。所以得按需组合。Agent 就把之前的讨论内容整合，拆成了几个明确的小 ticket。每一个都可以独立地推进。比如这样一个：

![](/img/codez004.jpg)

这些新建好的 ticket 就可以一个一个单独的处理啦。比如下面这样。

## 最后一步：Agent 干活

![](/img/codez005.jpg)

整个过程跟团队协作时的节奏几乎一模一样：先讨论，再拆解，最后分头干活。不同的是，人换成了 Agent，效率还挺高，重点是它不会摆烂（除非 prompt 写的太糟糕）。

有点上头。
