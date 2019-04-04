---
layout: single
title:  "Refactoring: The First 100 Pages"
date:  2019-3-31
categories: javascript books
tags: javascript, clean code, programming, books, refactoring
header:
  image: assets/images/refactoring-header-chapter-notes.jpg
---
I am in the process of reading [Refactoring by Martin Fowler](https://www.amazon.com/gp/product/0134757599) and have recently finished the first 100 pages.  What is so special about the first 100 pages? Well, Martin himself _(yep, we're on a first name basis)_ tells the reader _(yours truly)_ that to get the most out of the book read the first four chapters, then skim and leverage the refactoring catalog as needed. And how long are the first four chapters...yup, you guessed it...100 pages!  

This is not a review of the book nor a JavaScript filled example-a-thon _(in process btw)_, but rather my key takeaways and chapter notes. I use these notes to augment my learning and leverage them to effectively use refactoring in my own work.  While not a review, I highly recommend this book if you architect systems, design software, want to advance as an engineer, and/or have a passion for clean, maintainable, and self-documenting code. And, let's be real, every self-respecting programmer cares about _all_ of these things :).

Let's dive in!

## Contents:
- [What is refactoring?](#what-is-refactoring)
- [My key takeaways](#my-key-takeaways)
- Chapter Notes:
  - [Chapter 1: Refactoring: A First Example](#chapter-1-refactoring-a-first-example)
  - [Chapter 2: Principles in Refactoring](#chapter-2-principles-in-refactoring)
  - [Chapter 3: Bad Smells in Code](#chapter-3-bad-smells-in-code)
  - [Chapter 4: Building Tests](#chapter-4-building-tests)

## What is refactoring?
Refactoring is a particular approach to cleaning up code. The term can be used as either a noun or verb.

> Refactoring (noun): a change made to the internal structure of software to make it easier to understand and cheaper to modify without changing its observable behavior.

Refactoring can also be used as a verb:

> Refactoring (verb): to restructure software by applying a series of refactorings without changing its observable behavior.

**The key takeaway**: make modifications to the internal structure of the code to augment development _without_ modifying the external behavior (e.g. public interface).

Speaking of key takeaways...

## My Key Takeaways
- The first foundation of refactoring is self-testing code!
  - Refactoring **requires** testable software
- Making development faster is the purpose of refactoring
- Make changes in small batches. Take small steps:
  - Update code, compile, test, commit, loop...
- Changes drive the need to refactor. If code works, and does not need to change, leave as is and do not refactor. Only refactor code when you need to make changes to the code.
- Legacy code without tests is very difficult to refactor _(yeah, tell me about it!)_
- When you need to add a new feature, take time to clean up the code _(this is the opportune time to refactor!)_
- Ultimately, you want to learn more about the system and from that learning improve the code, do not keep that learning in your head! Write it down and put it directly into the system.
- There are two hats: refactoring and adding new features
  - Refactoring **does not** add new features  
- Lastly, follow the scout rule:
> Leave the code cleaner than you found it  

Or as Three Stacks told me...
<iframe width="560" height="315" src="https://www.youtube.com/embed/-JfEJq56IwI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe> <br/>


On to the ~~cliff~~ Ajahne notes!

# Chapter Notes

## Chapter 1: Refactoring: A First Example
- The compiler doesn’t care if the code is ugly or clean, but a human does
- Changes drive the need to refactor. If the code works and never needs to change, leave as is (p. 5)
- Before refactoring, must have tests
  - Have automated tests and test after every refactoring
- Advice is to ignore performance when refactoring, oftentimes the performance hits are negligible
- Compile, test, commit
- Leave the codebase healthier than when you found it
- The true test of good code is how easy it is to change it (p. 43)
- Common sequence: read the code, gain some insight and move insight from your head back into the code (p. 43)
- Take small steps when refactoring

## Chapter 2: Principles in Refactoring
- Refactoring: Make code easier to understand and cheaper to modify
- Any bugs noticed during refactoring should still be present after refactoring (though latent bugs once noticed can be fixed)
- Refactoring does **not** add new functionality
- Two hats: refactoring and new features
- Software with good internal design allows you to easily find how and where you need to make changes to add a new feature
- The rule of three: three strikes and then you refactor (p. 50)
- Refactoring: move the understanding from your head into the code
- **Don’t set aside time to do refactoring, it is part of writing code**. You don’t set aside time to write an “if” statement, you just do it
- Planned refactoring should be rare. Most refactoring should be the unremarkable, opportunistic kind
- Most refactoring can be completed in a few minutes _(word?!)_
- Code reviews help spread knowledge through the development team
  - it helps more experienced developers pass knowledge to those less experienced
  - it helps people understand larger parts of the system and gives opportunity for more people to suggest useful ideas (p. 54)
- Implement refactoring and code review with pair programming
- **When not to refactor**: code is a mess, but do not need to modify, then don’t need to refactor - only change when you need to understand how it works/ add features
- Problems with refactoring
  - There can be a tradeoff between large refactoring and adding a small feature
  - Those without experience in refactoring need mentorship
- As a tech lead, encourage refactoring, encourage the health of your system
- **Point of refactoring is not to create “clean code”, it is purely economic - we refactor to make is faster - these economic benefits should always be the driving factor**
- Code ownership - published interfaces are harder to do (e.g. APIs)
- One of the key characteristics of refactoring is that it does not change the observable behavior of the program
- If I want to refactor, need self-testing code
- Doing refactoring on a large code base with poor test coverage? Leverage your IDE (post) - see Jay Bazuzis description on a safer way to do extract method (p. 106) in C++
- “The dragon guarding this happy tale is the common lack of tests” - **if you have a big legacy system with no tests, you can’t safely refactor into clarity**
- Databases: release changes to production over multiple releases
- People only know what they need from software once they’ve had a chance to use it
- Build software that solves only the currently understood needs, but make it excellently designed for those needs
- The first foundation of refactoring is self-testing code
- Refactoring helps us write fast software - it slows software in the short term but makes simpler code that is easier to performance tune during optimization

## Chapter 3: Bad Smells in Code
- _Multiple code smells, review this chapter and the table in the back for reference_
- TODO: create a table with name, description, and corresponding refactoring!
- A couple quick points that stood out to me
  - If you have a good name for a function, you mostly don’t have to look at its body
  - A heuristic they follow is if you find the need to comment something, replace it with a function instead
  - Comments: when you feel the need to write a comment, first try to refactor the code so that any comment becomes superfluous
- Some "smells" include
  - Mysterious name
  - Duplicated code
  - Long function
  - Data clumps
  - Primitive obsession
  - Repeated switches
  - Long parameter list
  - Divergent change: when one module is changed in different ways for different reasons. E.g. three functions change when the DB changes and four change when financial statements change
  - Shotgun surgery - when you make one change you have a lot of places to change
  - Feature envy - when a module spends more time communicating with other data or functions in another module than within itself

## Chapter 4: Building Tests
- Make sure all tests are fully automatic and that they check their own results
- TDD: write a failing test, write the code that makes it work, refactor to ensure the code is as clean as possible (test-code-refactor)
- Refactoring requires tests _(this is mentioned like 17,319,451 times!)_
- Testing should be risk-driven _(he does not test accessors that just read and write a field)_
- Focus test areas that you are most worried about going wrong
- **It is better to write and run incomplete tests than not to run incomplete tests**
- General rule: one verify (i.e. assertion) per it clause (i.e. test)
- Probe the boundaries (e.g. when collections are empty, try 0 with numbers) - think of the boundary conditions under which things might go wrong and concentrate your tests there
- Be an enemy to your code
- Don’t let the fear that testing can’t catch all bugs stop you from writing tests that catch most bugs
- Add to the test suite as you refactor
- Architectures often are (and rightly so) judged on there testability
- Will often work on a test suite as much as we work on the main code
- When you get a bug report, start by writing tests that expose the bug
- How confident are you in the code that some tests will fail when a defect is entered into the code
