---
title: "The MoSCoW Method"
date: 2019-02-14T09:54:42+01:00
draft: false
tags: ["Agile", "Software Development", "Project Management", "MoSCoW", "Iron Cross of Software Engineering"]
series: ["Internship"]
categories: ["Internship"]
aliases:
    - /blog/2019-02/the-moscow-method/
toc: true
summary: "The MoSCoW Method, what does it stand for, what does it mean, why would you use it, and does it have anything to do with that one city in Russia..."
---

This week I went to my first ever Tech Meetup!
Thanks to Rabobank & Utrecht JUG I got to see Robert C. Martin, also known as Uncle Bob, in action! 
If you don't know who he is, I highly recommend his book "Clean Code". 

School can only teach you so much. 
That's not to say school isn't worthwhile, absolutely not! 
Thanks to my (still ongoing) formal education I learned how to quickly learn the basics of new programming languages, and went a bit deeper into one or two of them. 
So now, when I see a new language, I have a base to fall back on.
That being said, Clean Code was an eye-opener for me. 
The first thing JIDOKA, my internship company, did, was give me a two-day [course](https://www.jidoka.be/clean-code/) on the subject, taught by my mentor Geert Guldentops.

Now, you might be thinking, the title of this post is "The MoSCoW Method", why are you even mentioning Robert Martin and Clean Code?
Because his book isn't only about coding practices, but also about Agile Software Practices.
This was pervasive throughout the Utrecht JUG Meetup as well.

During his last session, Uncle Bob talked about the importance of managing software development projects and communicating well with your client.
And as chance would have it, the day before I left for Utrecht, I was stuck. Where do I even begin to define the scope of a project?

To test out whether my internship project was even feasible, I had been tasked with coming up with a Proof of Concept.
This would then become a tool to help set the scope of the project as a whole.
It was supposed to be a very small test, where I would focus on just one part of the bigger puzzle.
Lo and behold, it was way too elaborate. To nudge me in the right direction, Geert drew something on some scrap paper. I've drawn it out for you here.

<img src="/images/scope/IronCrossSoftwareEngineering.jpg" width="500px" alt="The Iron Cross of Software Engineering"></img>

A project's deadline is usually an immutable object, frozen in place. In my case, there is absolutely no wiggle room.
The deadline for my Bachelor Thesis is June 2nd, no ifs or buts about it.
According to the iron cross of software engineering, there are three other things we could change, apart from the deadline: the quality, the scope, and the budget.
You might know the iron cross under a different name: the project management triangle.
Right off the bat, something both my mentor Geert and uncle Bob stressed was: do not, under any circumstances, mess with the quality. 
Even telling your client that quality is something you can lower is not a good idea. 
So what's left? The budget. Well, in a regular development project, we could double the development staff. 
As we all know, doubling the staff effectively doubles the speed at which code can be written.
*Sarcasm is very hard to convey through text, so I'll just put a nice little disclaimer here: the previous statement was practically drowning in sarcasm.*
Adding extra staff adds extra overhead, and the later these new developers are added, the more time it will take for them to be productive members of the team.
My internship is a one-woman show. Yes, I can count on my colleagues, both at JIDOKA and at school, but at the end of the day, it's just me.

So that leaves just one more option: the scope. 

<img src="/images/scope/ScopeUncleBob.jpg" width="500px" alt="Sketchnotes of Uncle Bob's session 'Agility & Architecture'"></img>

Telling your client that the scope needs to be smaller is not easy. 
Often they will hang on to their initial requirements for as long as possible. 
And here, we finally come to the MoSCoW Method.

There are several methods that can be used to make it easier for your client to choose which requirements can be dropped, and which cannot.
The MoSCoW method is one of them. 
Only the consonants are important in this abbreviation, the vowels are purely there for pronunciation's sake. It stands for:

Must have

Should have

Could have

Won't/Would have

The Must Haves are those things that the project cannot go without. If you don't get one of those done, you can just as well scrap the entire project.
The Should Haves are still pretty crucial. However, if you don't get one of these done, it's not the end of the world.
It might take some creative thinking to find a workaround for the issue, or it might cause part of the functionality to be non-viable, but these are often features that can be added in a second live phase.
The Could Haves can be viewed as optional. 
We'd very much like them to be in the end product, but if the deadline of the project is at risk, these are the first things to be scrapped.
Lastly, we have the Won't/Would Haves. 
These are the optional items that are so low-priority that we simply won't do them, at least during the current time frame.
When Geert explained the MoSCoW method to me, he used the term Would instead of Won't. 
Originally the term was Won't. However, from what I can tell, the term shifted to Would because when discussing these points with a client, Won't sounds very final and has a bit of a bad connotation.
Which one you want to use is of course entirely up to you.

During my research on MoSCoW, I came across a [list of tips by Zied Zaier](http://ziedzaier.com/wp-content/uploads/2015/10/MOSCOW) on how to put the MoSCoW method into practice.
One in particular stuck out at me, and really helped me to put this method into practice.

<br>
<center><font size=+2>
"Start all requirements as Won’t Haves and then justify why they need to be given a higher priority."
</font></center>
<br>


If you have used MoSCoW during a project with a client, I would love to hear from you! 
How did it influence the decisions made in terms of scope?
Did it aid or hinder you during the project?
Did it make communicating with your client and other stakeholders easier or tougher?

And with that, dear reader, I leave you. <br>
See you soon!

Silke