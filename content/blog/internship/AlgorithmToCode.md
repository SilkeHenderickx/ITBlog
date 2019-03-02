---
title: "How to Translate a Mathematical Algorithm into Code"
date: 2019-03-02T12:02:22+01:00
draft: true
tags: ["Machine Learning", "Algorithm", "Python", "TF-IDF"]
series: ["Internship"]
categories: ["Internship"]
toc: true
summary: 
---

Does your brain short-circuit when you see a mathematical algorithm? Don't worry, you're not alone.

In this post I will show you how you can work your way through an algorithm and get it up and running in code.
The examples that I will be using come from a Proof of Concept that I worked on for my internship at [JIDOKA](https://www.jidoka.be).

</br></br>

---

### **The <b style="color:DodgerBlue;">FOUR</b> Steps of Translating a Mathematical Algorithm into Code:**

</br><font size=+1>
<b style="color:DodgerBlue;">
<ol>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">Translate the algorithm into human terms</b></li>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">Split the algorithm into bite-sized chunks</b></li>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">Translate each chunk into code</b></li>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">Combine the chunks to form the complete algorithm</b></li>
</ol>
</b>
<font></br>


---

</br>

## <b style="color:DodgerBlue;">Translate the Algorithm into Human Terms</b>

The algorithm that I will be using here is **TF-IDF**, which stands for **Term Frequency - Inverse Document Frequency**, and it looks like this:

<center><img src="/images/TFIDF/TFIDF.PNG" width="300px" alt="TFIDF Algorithm""></img></center>

*But what does it actually mean?*

Unless you're a math wizard and are creating your own algorithms, you can find explanations for the one you're using with a quick google search.

<b>To summarize:</b>

The goal of TF-IDF is to calculate the importance of a word in a document.

**TF calculates how many times a word appears in a document.**

However, many words like *and*, *or*, and *the* are used so frequently in the English language, that their score would skew the rest of the words' scores.
That's where the IDF part comes in.

**IDF gives each word a score based on how many documents contain it. The more documents contain it, the lower the score.**

*Now let's apply this to the algorithm.*

<img src="/images/TFIDF/TFIDF.PNG" width="200px" alt="TFIDF Algorithm""></img>

The first thing we can do is split the algorithm into two parts because: 
**TF-IDF = TF x IDF**

**TF = tf<sub>i,j</sub>**

OR: How many times each word i is in each document j, and calculate that for each document.
 
 We can the rewrite TF as:
 
 TF = number of times word i appears in j / number of words in j



**IDF = log ( N / df<sub>i</sub>)**

OR: How many times word i is one of the words in a document, and compare it to the total number of documents.

We can rewrite IDF as:

IDF = log ( number of documents / number of documents containing i)


## <b style="color:DodgerBlue;">Split the Algorithm into Bite-sized Chunks</b>

Now that our algorithm has been translated into human terms, it's time to split it into bite-sized chunks.

*What does this mean?*

We are going to create small tasks that we can turn into separate functions in our code.

*We're refactoring, before we've even written any code!*

**TF = number of times word i appears in j / number of words in j**

AND

**IDF = log ( number of documents / number of documents containing i)**

can be split into four parts:

<b style="color:DodgerBlue;">
<ul>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">number of times word i appears in j</b></li>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">number of words in j</b></li>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">number of documents</b></li>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">number of documents containing i</b></li>
</ul>
</b>

## <b style="color:DodgerBlue;">Translate Each Chunk into Code</b>

## <b style="color:DodgerBlue;">Combine the Chunks to Form the Complete Algorithm</b>