---
title: Find and Terminate Active Resources on AWS Using Tag Editor in Resource Groups
date: 2023-08-22 20:30:32
tags:
---

You must have the same headache as me when AWS sends you an email saying this month you get yet another bill for all the unknown active resources on AWS.

But wait, where are they? How can I find them?

I have been asking myself these questions time and time again. Now I finally find a simple way to deal with it.

- Open AWS Resource Groups: https://console.aws.amazon.com/resource-groups/
- In the navigation pane, on the left side of the screen, choose Tag Editor.
- For Regions, choose All regions.
- For Resource types, choose All supported resource types.
- Choose Search resources.

Then, you will see all the resources that are still active in your account.

You need to terminate them one by one.

Good luck!
