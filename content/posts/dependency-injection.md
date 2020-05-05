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

The goal of this blogpost is to teach myself how to answer the above question. Maybe others can use it as well.
If you see any mistakes, let me know, I'm mostly just trying to learn here.

## What is a code dependency

Let's say you have two classes: **X** and **Y**

Class X **uses** some functionality of class Y

In this case:
- X has a **dependency** on Y
- X needs an **instance** of Y to function

// Making it less abstract

Let's say we're building an app that lets you create motivational quotes and send them to users.

We have created a Class called QuotesHandler. It has a method for creating quotes, and a method for sending them.
```c#
public class QuotesHandler{
    public Quote CreateQuote(){}
    public void SendQuote(){}
}
```
To send the quotes, we've created a QuotesMailer class.
```c#
public class QuotesMailer{
    public Quote MailQuote(){
        // mails a quote to a list of users
    }
}
```
We want the SendQuote() method to use the QuotesMailer. We could do it like this:
```c#
public class QuotesHandler{
    public void SendQuote(){
        QuotesMailer quotesMailer = new QuotesMailer();
        quotesMailer.MailQuote();
    }
}
```
Alright, that works. We can now create and mail motivational quotes.

However, you recieve some feedback from users. They don't want to get the motivational quotes by mail. They would preffer to get them as a text message instead.

We're going to have to replace the QuotesMailer with a QuotesTexter. But on top of that, we have to make significant changes in the QuotesHandler. In this case, it's an easy swap. We create a new class, and make the QuotesHandler use this instead of the QuotesMailer class.
```c#
public class QuotesTexter{
    public Quote TextQuote(){
        // texts a quote to a list of users
    }
}
public class QuotesHandler{
    public void SendQuote(){
        QuotesTexter quotesTexter = new QuotesTexter();
        quotesTexter.TextQuote();
    }
}
```
However, as your code grows and you build more features into the project, it becomes harder to adapt. 
