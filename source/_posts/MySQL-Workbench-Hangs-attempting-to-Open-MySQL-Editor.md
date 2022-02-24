---
title: MySQL Workbench Hangs attempting to Open MySQL Editor
date: 2021-06-12 22:20:54
tags:
---

When this bug happens, it shows that it takes time to open the MySQL Editor, but the fact is that it will never open. So you will wait forever.

I am on MacOS Catalina and the MySQL Workbench version is 8.0.22, just in case you want to know.

## Why this error happens (My guess):

You changed the password to the MySQL database user, but it somehow failed to sync the password in the keychain.

## The solution:

Go to the /Applicaiton/Utilities/ to find the Keychain Access App and run it. Search and delete the password to the database user. Try search 'MySQL'. Reopen the MySQL Workbench and you should be fine now.