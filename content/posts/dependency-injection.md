---
title: "Dependency Injection"
date: 2020-04-20T21:03:04+02:00
draft: true
tags: ["SOLID", "Dependency Injection"]
toc: true
aliases:
    - /blog/2020-03/dependency-injection/
summary: 
---

Last week I had a technical interview. One of the questions I was asked was: 

<font size=+1>
<b style="color:DodgerBlue;">
What is Dependency Injection?
</b>
</font>

Have I been using dependency injection on the job for the past few months? <b style="color:DodgerBlue;">YES</b>

Did I fumble and fail to explain it properly and concisely? <b style="color:DodgerBlue;">ALSO YES</b>

The goal of this blogpost is to teach myself how to answer the above question. Maybe others can use this as well.
If you see any mistakes, let me know, I'm mostly just trying to learn here.

## What is a code dependency

You have two classes: **A** and **B**

Class A **uses** some functionality of class B

In this case:
- A has a **dependency** on B
- A needs an **instance** of B to function