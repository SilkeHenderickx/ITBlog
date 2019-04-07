---
title: "How I Translated a Mathematical Algorithm into Code: TF-IDF to Python"
date: 2019-03-08T12:02:22+01:00
draft: false
tags: ["Machine Learning", "Algorithm", "Python", "TF-IDF"]
series: ["Internship"]
categories: ["Internship"]
toc: true
aliases:
    - /blog/2019-03/how-i-translated-a-mathematical-algorithm-into-code-tf-idf-to-python/
summary: Does your brain short-circuit when you see a mathematical algorithm? Don't worry, you're not alone.
         In this post I will show you how I worked my way through an algorithm, namely TF-IDF, and got it up and running in Python.
---

Does your brain short-circuit when you see a mathematical algorithm? Don't worry, you're not alone.

In this post I will show you how I worked my way through an algorithm, namely TF-IDF, and got it up and running in Python.
The code examples that I will be using come from a Proof of Concept that I worked on for my internship at [JIDOKA](https://www.jidoka.be).

After finishing the PoC, I realized that I had actually used a system while working on it. Here's what I did.

</br></br>

___

<font size=+2>
**The <b style="color:DodgerBlue;">FOUR</b> Steps of Translating a Mathematical Algorithm into Code:**
</font>

</br><font size=+1>
<b style="color:DodgerBlue;">
<ol>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">Translate the algorithm into human terms</b></li>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">Split the algorithm into bite-sized chunks</b></li>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">Translate each chunk into code</b></li>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">Combine the chunks to form the complete algorithm</b></li>
</ol>
</b>
</font></br>


___

</br>

# <b style="color:DodgerBlue;">Translate the Algorithm into Human Terms</b>

The algorithm that I will be using here is **TF-IDF**, which stands for **Term Frequency - Inverse Document Frequency**, and it looks like this:

<center><img src="/images/TFIDF/TFIDF.PNG" width="300px" alt="TFIDF Algorithm""></img></center>

*But what does it actually mean?*

Unless you're a math wizard and are creating your own algorithms, you can find explanations for whichever one you're using with a quick google search. Here's what I found.

<b>To summarize:</b>

The goal of TF-IDF is to calculate the importance of a word in a document.

**TF calculates how many times a word appears in a document.**

However, many words like *and*, *or*, and *the* are used so frequently in the English language, that their score would skew the rest of the words' scores.
That's where the IDF part comes in.

**IDF gives each word a score based on how many documents contain it. The more documents contain it, the lower the score.**

*Now let's translate the algorithm into human terms.*

<img src="/images/TFIDF/TFIDF.PNG" width="200px" alt="TFIDF Algorithm""></img>

The first thing we can do is split the algorithm into two parts because: 
**TF-IDF = TF x IDF**

**<font style="color:DodgerBlue;">TF = tf<sub>i,j</sub></font>**

OR: How many times each word i is in each document j, and calculate that for each document.
 
 We can rewrite TF as:
 
> TF = number of times word i appears in document j / number of words in document j



**<font style="color:DodgerBlue;">IDF = log ( N / df<sub>i</sub>)</font>**

OR: How many times word i is one of the words in a document, and compare it to the total number of documents.

We can rewrite IDF as:

> IDF = log ( number of documents / number of documents containing word i)


# <b style="color:DodgerBlue;">Split the Algorithm into Bite-sized Chunks</b>

Now that our algorithm has been translated into human terms, it's time to split it into bite-sized chunks.

*What does this mean?*

We are going to create small tasks that we can turn into separate functions in our code.

*We're refactoring, before we've even written any code!*

**TF = number of times word i appears in document j / number of words in document j**

AND

**IDF = log ( number of documents / number of documents containing word i)**

can be split into four parts:

<b style="color:DodgerBlue;">
<ul>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">number of times word i appears in document j</b></li>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">number of words in document j</b></li>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">number of documents</b></li>
<li style="padding-left:1em"><b style="color:rgb(60, 60, 60);">number of documents containing word i</b></li>
</ul>
</b>

# <b style="color:DodgerBlue;">Translate Each Chunk into Code</b>

For my PoC I worked with [Pluralsight course data](https://www.pluralsight.com/product/professional-services/white-paper/api). I then cleaned and molded it into the shape that I needed.
Ending up with a list of courses, containing an Id followed by the document itself:

**['course1', 'course description']**

Within the code, this is called 'clean_docs'

### Imports

For my PoC I worked with a Jupyter Notebook and used the following imports:

```python
import csv
import string
import math
from collections import defaultdict
```

### Number of times word i appears in document j

For this part, we want to end up with a list. 
Each line in the list will contain 1 document Id, and a dictionary containing each word in the document as a key, followed by how many times the word occurs in that document.

```python
def term_frequency_word_i_doc_j(clean_docs):
    term_frequency_word_i_doc_j_list = []   # list setup
    for doc in clean_docs:
        term_frequency_word_i_doc_j = {} # dictionary setup
        
        # the next two lines create a list of all words in the document
        # all leading and trailing punctuation is removed
        # so that e.g. asp.net doesn't become two words: asp and net
        words = doc[1].split()
        words = list(map(lambda x: x.strip(string.punctuation), words))
        
        for word in words:
        
            # if the word is already in the dictionary, amount + 1
            if word in term_frequency_word_i_doc_j:
                term_frequency_word_i_doc_j[word] += 1
                
            # else add it to the dictionary
            else:
                term_frequency_word_i_doc_j[word] = 1
                
        # create the dictionary and append it to the list        
            temp = {'doc_id' : doc[0], 'term_frequency_word_i_doc_j' : term_frequency_word_i_doc_j}
        term_frequency_word_i_doc_j_list.append(temp)
        
    return term_frequency_word_i_doc_j_list
```

### Number of words in document j

I split this segment into two parts: a function that takes a document and counts the amount of words, and a function that uses the first function to create a dictionary of each document and the word count.

```python
# cleaning the data is not necessary here
# if you use a different dataset you might need to clean the data anyway

# count words in a document
def count_words(doc):
    doc_words = doc.split()
    return len(doc_words)
    
# create list of word counts
def docs_word_count(clean_docs):
    docs_word_count = []
    for doc in clean_docs:
        count = count_words(doc[1])
        temp = {'doc_id' : doc[0], 'doc_length' : count}
        docs_word_count.append(temp)
    return docs_word_count
```

### Number of documents

This one did not need a seperate function.

```python
len(clean_docs)
```

### Number of documents containing word i

This section only needs one key value pair, so I opted to use a defaultdict instead of a regular dictionary.

```python
def count_docs_containing_word(clean_docs):
    count_docs_containing_word = defaultdict(int) # dictionary setup with int values
    for doc in clean_docs:
    
        # same as the first section
        # the next two lines create a list of all words in the document
        # all leading and trailing punctuation is removed
        # so that e.g. asp.net doesn't become two words: asp and net 
        words = doc[1].split()
        stripped_words = list(map(lambda x: x.strip(string.punctuation), words))
        
        # removing duplicates because we only want to count each word in a document once
        words_no_duplicates = list(set(stripped_words))
        
        for word in stripped_words:
            if word in count_docs_containing_word:
                count_docs_containing_word[word] += 1
            else:
                count_docs_containing_word[word] = 1
    
    return dict(count_docs_containing_word)

```

# <b style="color:DodgerBlue;">Combine the Chunks to Form the Complete Algorithm</b>

Now that we have each separate section prepared, it's time to combine them.
Let's start by running each function and saving it into a variable.
Underneath each function I've put a print() of the first row in the list, to show what it looks like.
As stated above, this is using the Pluralsight course data.

```python
tf_word_i_doc_j = term_frequency_word_i_doc_j(clean_docs)
# {'doc_id': 'abts-advanced-topics', 'word_frequency_dict': {'biztalk': 2, '2006': 2, 'business': 2, 'process': 2, 'management': 2, 'this': 1, 'course': 1, 'covers': 1, 'features': 2, 'in': 1, 'server': 1, 'including': 1, 'web': 1, 'services': 1, 'bam': 1, 'hosting': 1, 'and': 1, 'bts': 1, '2009': 1}}

tf_docs_word_count = docs_word_count(clean_docs)
# {'doc_id': 'abts-advanced-topics', 'doc_length': 25}

idf_count_docs_containing_word = count_docs_containing_word(clean_docs)
# the first line in this list is for the key 'biztalk'
# 17

idf_num_docs = len(clean_docs)
# 7975
```

### Term Frequency

**TF = number of times word i appears in document j / number of words in document j**

```python
# insert both parts of the equation into the function
def computeTF(tf_word_i_doc_j, tf_docs_word_count): 
    TF_scores = []
    
    # tf_docs_word_count is a list, so we can only access each line by index number
    i = 0
    
    # each line in tf_word_i_doc_j represents one document
    for document in tf_word_i_doc_j:
        doc_id = document['doc_id']
        
        # we will create one list entry per term in the document
        for term in document['word_frequency_dict']:
        
            temp = {'doc_id' : doc_id,
            
                    # TF = number of times word i appears in document j / number of words in document j
                   'TF_score' : document['word_frequency_dict'][term]/tf_docs_word_count[i]['doc_length'],
                   
                   'term' : term}
            TF_scores.append(temp)
        i += 1
    return TF_scores
    
# this function returns something that looks like this:
# {'doc_id': 'abts-advanced-topics', 'TF_score': 0.08, 'term': 'biztalk'}
```

### Inverse Document Frequency

**IDF = log ( number of documents / number of documents containing word i)**

For this part, I did something that might seem a bit weird at first. Bear with me, all will be explained later. 

```python
# insert both parts of the equation AND a stowaway tf_word_i_doc_j into the function
def computeIDF(idf_num_docs, idf_count_docs_containing_word, tf_word_i_doc_j): 
    IDF_scores = []
    
    # same iteration as in TF except with a for loop instead of a foreach
    for x in range(len(tf_word_i_doc_j)):
        doc_id = tf_word_i_doc_j[x]['doc_id']
        for term in tf_word_i_doc_j[x]['word_frequency_dict']:

            temp = {'doc_id' : doc_id, 
                    
                    # IDF = log ( number of documents / number of documents containing word i)
                    'IDF_score' : math.log(idf_num_docs/idf_count_docs_containing_word[term]), 
                    
                    'term' : term}
            IDF_scores.append(temp)
    return IDF_scores
    
# this function returns something that looks like this:
# {'doc_id': 'abts-advanced-topics', 'IDF_score': 6.150853583596829, 'term': 'biztalk'}
```

### TF-IDF

**TF-IDF = TF * IDF**

Now for our final step! Combining TF and IDF to complete my first ever mathematical algorithm in Python! Woo!

```python
def computeTFIDF(TF, IDF):
    TFIDF_scores = []
    
    # loop over the IDF and TF lists
    for i in IDF:
        for j in TF:
        
            # if it's the same document and the same term, compute its TF-IDF
            if i['doc_id'] == j['doc_id'] and i['term'] == j['term']:
            
                temp = {'doc_id' : i['doc_id'],
                
                        # TF-IDF = TF * IDF
                       'TFIDF_score' : i['IDF_score']*j['TF_score'],
                       
                       'term' : i['term']}
        TFIDF_scores.append(temp)
    return TFIDF_scores
    
# this function returns something that looks like this:
# {'doc_id': 'abts-advanced-topics', 'TFIDF_score': 0.4920682866877463, 'term': 'biztalk'}
```

Positive that I had done it, I ran the code.

And waited...

And waited some more...

And got myself a coffee...

**1h 23min 15s later, it worked!**

But it took way too long.

Panicking about the runtime, I started searching for ways to speed up my algorithm. 
Maybe **multithreading** could do the trick? I knew nothing of multithreading, and so I went down the rabbithole.
Luckily a stray comment residing deep in some forum was able to help me out. I don't remember the exact words, but it went something like this:

> <i style="color:DodgerBlue;">Multithreading is cool and all, but make sure your code isn't doing unnecessary loops and checks first. You'd be surprised how much time is wasted that way. </i>

So I went through my code again, putting timers on different sections to check how long it took.

I had found the guilty party.

```python
if i['doc_id'] == j['doc_id'] and i['term'] == j['term']:
```


In order to get rid of it, I placed the stowaway tf_word_i_doc_j into the IDF function.

By making sure that the **length AND order** of both the TF and IDF list were the same, I could simply remove the line of code causing the bottleneck.


```python
def computeTFIDF(TF, IDF):
    TFIDF_scores = []
    for i in range(len(TF)):
        temp = {'doc_id' : TF[i]['doc_id'],
        
                # TF-IDF = TF * IDF
                'TFIDF_score' : IDF[i]['IDF_score']*TF[i]['TF_score'],
                'term' : TF[i]['term']}
        TFIDF_scores.append(temp)
    return TFIDF_scores
```

I ran the code again, and the run time changed from roughly an hour to 996 ms for that function, resulting in a total run time of about 10 seconds.

> <font size=+1 style="color:DodgerBlue;">Note</font>

> When having blocks of code that are dependent on each other to function in a certain way, it is important to document it.

> Someone else, or myself at a later point in time, might look at the IDF code and think "This looks weird and can be done much simpler, let's refactor it!"

> The best documentation in this case would be a test that checks whether the TF and IDF lists are the same length and are in the same order. This way, if someone refactors it, it will break the test.

> However, as tests were not part of this PoC that I was doing, I opted to add written documentation above each of the code blocks.

# <font style="color:DodgerBlue;">Conclusion </font>

Safe to say, I learned a lot from working out this Proof of Concept, and even more from making this blog post about it.

I hope this might help you, if you're working on something similar.

Let me know what you think, and if there are any tricks of the trade and/or improvements that you'd like to share with me on this topic, I'd love to hear them!



And with that, dear reader, I leave you. 
See you soon!

Silke