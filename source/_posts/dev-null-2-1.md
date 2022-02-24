title: '> /dev/null 2>&1'
date: 2021-03-19 18:25:34
tags:
---
I saw something in the shell code as follows.
```bash
cat /dev/random > /dev/null 2>&1
```
Or something similar.
```bash
export lang="en_us.utf-8" >/dev/null 2>&1
```
They all have this part.
```bash
>/dev/null 2>&1
```
I did some research to find out what it means. Basically, the number 1 is standard output, the number 2 is the standard error, the char > is to redirect the flow of information, and 2>&1 means to treat the 2 the same way as the 1, and /dev/null, you know, is in the middle of nowhere.

So, to put them all together, this piece of code means that throw the standard output and standard error away as garbage. You will never see anything stdout or stderr on the screen or anywhere on disk. No, just say goodbye to them. They are gone for good.