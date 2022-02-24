---
title: Superclass Typo in Servlet Template of Eclipse
date: 2021-05-23 20:52:39
tags:
---

Update: The typo has been fixed if you are using Dynamic web module version 5.0

When you are using the Servlet Template in Eclipse, you may encounter the error saying "The import javax.servlet cannot be resolved."

For example, I am using Eclipse for Mac (Version 4.19.0). First, create a Dynamic Web Project, target runtime: Apache Tomcat v10.0, Dynamic web module version 4.0. And inside this project, create a new servlet file using the Create Servlet Wizard. Soon you will see the errors pop up in the servlet file you just created.

```java
// BEFORE
import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
```

How to fix it? All you have to do is changing the superclass name from javax into jakarta. Why does this happen? I think it is because, as mentioned on Wikipedia page, that from 12 Jun 2020 and on, API moved from package javax.servlet to jakarta.servlet. Let's hope Eclipse will update the template someday in future. For the exising codes out there, I guess they are doing well.

```java
// AFTER
import java.io.IOException;
import jakarta.servlet.ServletException;
import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
```

Of course, you can create an empty class file to build servlet from scratch, to avoid such issues. Just in case you do face the similar errors in Eclipse when coding Java, I hope the simple fix would help you.

Wikipedia page of Jakarta Servlet:
https://en.wikipedia.org/wiki/Jakarta_Servlet