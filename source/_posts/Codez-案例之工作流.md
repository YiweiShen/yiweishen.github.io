---
title: Codez 使用案例之工作流
date: 2025-07-20 16:36:20
tags:
---

最近沉迷于 Agentic Coding，搞了个小项目 [Codez](https://github.com/YiweiShen/codez)，直接嵌在 GitHub Actions 里运行 Codex CLI，效果还不错。可以做这样的工作流：

**先和 AI 讨论，然后问题拆解，最后各个击破**

比如这个代码重构的需求：[Issue #304](https://github.com/YiweiShen/codez/issues/304)

---

![](/img/codez001.jpg)

---

## 第一步：先抛出需求

我在 issue 里写清楚了想做的事，包括要探讨的点、相关的背景资料。这个 issue 的标题和内容，agent 会当成初始 prompt 的一部分。

然后我直接在评论里触发 agent：

```bash
/codex             # 用关键词唤醒 agent
--no-pr            # 加个 flag，不要直接生成 PR，因为我想要把问题先探讨清楚
--fetch            # 这 flag 会让 agent 把链接里的内容先抓下来，方便离线使用
https://google.github.io/styleguide/tsguide.html  # 提供相关文档，有助于 agent 做判断
```

---

![](/img/codez002.jpg)

---

这样 agent 就开始工作啦。即便它在运行时没有网络权限，但通过 context（包括 codebase、给的链接、issue 内容），它还是给出了几条挺靠谱的初步思路。

## 第二步：自动拆解成可执行的 tickets

接着我又触发了一次 agent，这次是让它生成一系列 issues：

---

![](/img/codez003.jpg)

---

```bash
/codex
--create-issues    # 原理是让模型生成标题加内容的 JSON，然后用 GitHub API 创建 issue
--full-history     # 把当前对话前面的所有评论都加入 prompt 进入 context window
```

注意一下：所谓的 flag 只有当前评论内的 flag 才会生效。现在 agent 把讨论内容整合，分别创建了 issues。每一个 issue 都可以独立地推进。

---

![](/img/codez004.jpg)

---

这些新建好的 ticket 就可以一个一个单独的处理啦。比如下面这样。

## 最后一步：Agent 干活

---

![](/img/codez005.jpg)

---

整个工作流就像真正的团队协作一样：先讨论，再问题拆解，最后分头干活。不同的是，把人换成了 agent。

有人说，Agentic Coding 就像是程序员的猫薄荷。特别上头。
