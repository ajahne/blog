# Refatoring Notes - The first 100 pages

## TOC:
- [Intro](#intro)
- [Chapter 1: Refactoring: A First Example](#chapter-1-refactoring-a-first-example)
- [Chapter 2: Principles in Refactoring](#chapter-2-principles-in-refactoring)
- [Chapter 3: Bad Smells in Code](#chapter-3-bad-smells-in-code)
- [Chapter 4: Building Tests](#chapter-4-building-tests)

## Intro:
- refactoring definition on page xiv
- general approach to reading the book Read chapters 1-4 and skim the catalog
- a lesson learned by reading later on: "As long as I learn something, my time wasn’t wasted." 

## Chapter 1: Refactoring: A First Example
- For examples, imagine in the context of a larger system
- The compiler doesn’t care if the code is ugly or clean, but a human does
- Changes drive the need to refactor. If the code works and never needs to change, leave as is (page 5)
- Before refactoring, must have tests
- Have automated tests and test after every refactoring
- Advice is to ignore performance when refactoring, oftentimes the performance hits are negligible
- Compile, test, commit
- Note, when he refactored, he put all the new functions is the main function to avoid impacting other scopes
- Leave the codebase healthier than when you found it
- The true test of good code is how easy it is to change it (43)
- Common sequence: read the code, gain some insight and move insight from your head back into the code (43)
- Take small steps when refactoring

## Chapter 2: Principles in Refactoring
- Refactoring: Make code easier to understand and cheaper to modify
- Any bugs noticed during refactoring should still be present after refactoring (though latent bugs. One noticed can be fixed)
- Refactoring does not add new functionality
- Two hats: refactoring and new features
- Software with good internal design allows you to easily find how and where you need to make changes to add a new feature
- The rule of three: three strikes and then you refactor(pg50)
- Refactoring: move the understanding from your head into the code
- Don’t set aside time to do refactoring, it is part of writing code. Don’t set aside time to write an “if” statement, you just do it
- Planned refactoring should be rare. Most refactoring should be the unremarkable, opportunistic kind
- Most refactoring can be completed in a few minutes (word?!)
- Branch by abstraction
- Code reviews help spread knowledge through the development team, help more experienced developers pass knowledge to those less experienced, help people understand larger parts of the system, give opportunity for more people to suggest useful ideas (pg54)
- Implement refactoring and code review with pair programming
- Not refactor: code is a mess, but do not need to modify, then don’t need to refactor - only change when you need to understand how it works/ add features
- Problems with refactoring 
- There can be a tradeoff between large refactoring and adding a small feature
- As a tech lead, encourage refactoring, encourage the health of your system
- Those without experience in refactoring need mentorship
- Point of refactoring is not to create “clean code”, it is purely economic - we refactor to make is faster - these economic benefits should always be the driving factor
- Code ownership - published interfaces are harder to do (e.g. APIs)
- One of the key characteristics of refactoring is that it does not change the observable behavior of the program
- If I want to refactor, need self-testing code
- Doing refactoring on a large code base with poor test coverage? Leverage your IDE (post) - see Jay Bazuzis description on a safer way to do extract method (pg106) in C++
- “The dragon guarding this happy tale is the common lack of tests” - if you have a big legacy system with no tests, you can’t safely refactor into clarity
- Get from Qi - what areas of the code do we visit most frequently?
- Databases: release changes to production over multiple releases
- People only know what the need from software once they’ve had a chance to use it
- Build software that solves only the currently understood needs, but make it excellently designed for those needs
- The first foundation of refactoring is self-testing code
- Refactoring helps is write fast software - it slows software in the short term but makes simpler code that is easier to performance tune during optimization

## Chapter 3: Bad Smells in Code
- Mysterious name
- Duplicated code
- Long function
- If you have a good name for a function, you mostly don’t have too look at its body
- A heuristic they follow is if you find the need to comment something, replace it with a function instead
- Long parameter list
- Divergent change: when one module is changed in different ways for different reasons. E.g. three functions change when the DB changes and four change when financial statements change
- Shotgun surgery - when you make one change you have a lot of places to change
- Feature envy - when a module spends more time communicating with other data or functions in another module than within itself (not sure about this one, need to look into it)
- Data clumps
- Primitive obsession
- Repeated switches
- Loops - write and experiment with replacing it with maps
- Comments: when you feel the need to write a comment, first try to refactor the code so that any comment becomes superfluous

## Chapter 4: Building Tests
- make sure all tests are fully automatic and that they check their own results
- TDD was started by Kent Beck
- TDD: write a failing test, write the code that makes it work, refactor to ensure the code is as clean as possible (test-code-refactor)
- Refactoring requires tests
- Testing should be risk-driven (he does not test accessors that just read and write a field)
- Focus test areas that you are most worried about going wrong
- It is better to write and run incomplete tests than not to run incomplete tests
- General rule: one verify (I.e. assertion) per it clause (ie test)
- Probe the boundaries (e.g. when collections are empty, try 0 with numbers) - think of the boundary conditions under which things might go wrong and concentrate your tests there
- Be an enemy to your code
- Don’t let the fear that testing can’t catch all bugs stop you from writing tests that catch most bugs
- Add to the test suite as you refactor
- Architectures (often are and rightly so) judged on there testability
- Will often work on a test suite as much as we work on the main code
- When you get a big report, start by writing tests that expose the bug
- How confident are you in the code that some tests will fail when a defect is entered into the code
