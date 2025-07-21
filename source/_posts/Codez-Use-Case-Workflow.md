---
title: Codez Use Case Workflow
date: 2025-07-21 01:37:50
tags:
---

Lately, I’ve been obsessed with Agentic Coding and built a small project called [Codez](https://github.com/YiweiShen/codez), which runs the Codex CLI directly inside GitHub Actions. It's been working quite well. Here's an example of a workflow it supports:

**Discuss with AI first → break down the problem → tackle each part one by one**

Take this code refactoring request as an example: [Issue #304](https://github.com/YiweiShen/codez/issues/304)

---

![](/img/codez001.jpg)

---

## Step 1: Raise the Requirement

In the issue, I clearly described what I wanted to do, including points to discuss and related background info. The title and content of the issue become part of the initial prompt for the agent.

Then, I triggered the agent directly in the comments:

```bash
/codex             # Keyword to wake up the agent
--no-pr            # Add this flag to prevent it from directly creating a PR. I want to clarify the problem first
--fetch            # This flag lets the agent fetch the content from the link for offline use
https://google.github.io/styleguide/tsguide.html  # Relevant documentation to help the agent make informed decisions
```

---

![](/img/codez002.jpg)

---

With that, the agent gets to work. Even though it doesn’t have network access during runtime, it can still give some solid initial ideas using the context (codebase, content cached from the provided links, and the issue itself).

## Step 2: Automatically Break Down into Actionable Tickets

Next, I triggered the agent again. This time to generate a series of issues:

---

![](/img/codez003.jpg)

---

```bash
/codex
--create-issues    # The model generates a JSON of titles and descriptions, then uses GitHub API to create issues
--full-history     # Includes all previous comments in this thread into the context window
```

Note: Only flags in the current comment are recognized. The agent then organizes the discussion into multiple issues. Each issue can be worked on independently.

---

![](/img/codez004.jpg)

---

These newly created tickets can now be handled one by one. Like this:

## Final Step: Let the Agent Do the Work

---

![](/img/codez005.jpg)

---

The entire workflow feels like genuine team collaboration: discuss first, break down the problem, then work in parallel. The difference is that humans are replaced by agents.

Some say Agentic Coding is like catnip for programmers, totally addictive. It's true.
