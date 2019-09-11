---
layout: single
title:  "The Most Referenced Refactorings"
date:  2019-9-9 12:42:00 -0400
categories: javascript
tags: javascript, clean code, programming, books, refactoring
header:
  image: assets/images/refactoring-header-most-referenced-refactorings.jpg
---

# Outline
- Intro
- Purpose, why am I doing this?
- Takeaways: what did I learn?
- How did I do it
  - used pdf.js to read the file into memory
  - saved down the pdf to a text file
  - read the text file into memory with node.js
  - used regex to find the references
  - saved the references as a data file
  - used chart.js to plot the data
- Links to refactorings
  - Should I write about extract function?
- How can you use this data
- Conclusion
- Additional resources

## Intro
Refactoring is one the best programming books I have read. Full stop!  I have used this book to train and coach developers on my team.  I have used this book to make my programs and code better. Similar to pragmattic proggrammer, clean code, and others, this book helped me level up as an engineer. I've recommended this book to junior and senior developers a like.  

If you are an experienced engineer, many of the techniques in the book you may already used. Some are similar to things we may have read in clean code, etc. However, this book gave me a vocabulary, the words need to describe what I was doing as well as the how. In turn I could more easily coach members of my team on these techniquest.  I highly encourage you to copy this book!

## Purpose aka why did I do this
I wanted to plot the most referenced refactorings from Martin Fowler's book.  Why? Because I wanted to understand which refactorings were mentioned the most often.  Almost every refactoring listed in the book depends upon another refactoring. For example..."blah" referances "foo", "bar", and "baz"!

After reading the book, I had my list of fundamental refactorings, key techniques that I used in my own code and coached peers and junior developers on (through code review, etc.). However, what if I was missing something? What if there was a refactoring that I glossed over, but was referenced numerous times as a "prerequstie" for others that I should take a second look at.

Additionally, maybe I could gleam a bit of what Martin finds important or references the most.

Lastly, could this help me recommended to peers and other engineers certain refactorings to check out or "start with first". Martin tells the reader to read the first 100 pages, then skim the refactorings.  OK, but is there anything I should skim a little bit more?

Also, I wanted to try out chart.js and pdf.js. I wanted to try something new and see if I could do this.  A new opportunity, a new thing to learn, you know us engineers, we like that new and shiny. So, let's shine!

Graph time!

## The Results

Ok, Ajahne, enough talking (typing). What did you find?

Well I knew the king of the land was (and is) "Extract Function". If there is _one_ refactoring you learn, let it be this one!

So, my original hypothese was that the following 5 refactorings would be referenced the most
