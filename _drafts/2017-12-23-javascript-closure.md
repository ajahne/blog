---
layout: post
title:  "JavaScript Closure"
date:   2017-12-23 6:10:00 -0400
categories: jekyll javascript functions closure
---

### Introduction
We are back! The fun with functions tour continues.  Next stop…Closure!  

Oftentimes we as developers hear the term “closure” and become filled with anxiety.  Closures are not something mythical or magical, not some mystical creature hiding in the wilderness.  Rather, they are a practical concept that we use every time we write a function. The concept of Closure is sometimes confusing, but becomes clearer when we work with examples and write code.  Closures are also the building block for key JavaScript patterns  such as modules.  

### Definition
The academic definition of closure can simply be “an inner function defined in an outer function” or “the creation of a function, creates a closure”.  While both of these statements are technically true, they do not get to the practical purposes and application of closures.  

**A technical definition**: A function that references the lexical scope.

**A practical definition**:  An inner function defined in an outer function that retains access to the outer function’s scope (e.g. variables) after the outer function has returned.
 - Technically, the outer function does not have to return

### Key takeaways
- Every JavaScript function forms a closure
- It “encloses” the lexical scope
  - E.g.: A function that is defined on global scope, encloses the global variables and has access to them
- An inner function has three scope chains
  - Its own scope, its containing function’s scope, and global scope
- An inner function has access to the outer function’s variables and arguments

### Closures and lexical scoping
- **Lexical scoping**: the scope declared at author time.
- Closures can access their lexical scope (variables declared at author time), even when it is executed outside of its lexical scope (i.e. called at a later time)

### Why/when would we use closure?
Closures can help us address the following:

**Privacy**
- JavaScript does not have private methods.  However, the use of closures, can emulate this concepts. Privacy is a way of separating concerns, keeping non-essential methods from being accessed through your public API.

- This codepen example showcases the utilization of closure to emulate private methods.

**State**
- We can also use closure to maintain the value(‘state’) of function arguments at a certain time. We do this through the technique of partial function application. This way we can apply only a subset (i.e. ‘partial’ set) of arguments to a function.
- Check out this codepen example of partial function application, using closure to maintain state.

**Some more practical examples**:

**Loops**
- Sometimes creating a function in a loop (say creating a callback for a DOM event listener) may not work as expected given how the closure is created.  To better handle this scenario and ensure our handlers work as expected in our loops, we can utilize additional closures.

**SetTimeout**
- Another time we may run into challenges with scope and require closures is with setTimeout.  To illustrate the different ways (through IFFE, through explicit function calls) that we can ensure we are accessing variables as expected, explore this setTimeout example.

### Conclusion
Ok, how was that? Still with me? Let’s recap:  
Closure occurs every time a function is created and this function has access to the variables of its outer scope (be it global or a containing function).   Additionally, this function retains access to this outer scope and can continue to access this scope (variables, etc.).  Not so bad, right? OK?, OK. For additional examples and readings, check out the resources below.

### Additional Resources
- A great [introduction to closures from Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) that provides practical cases
- A great stackoverflow answer with additional examples
- [JavaScript is sexy](http://javascriptissexy.com/understand-javascript-closures-with-ease/) on understanding closures
- Additional medium resource of closure in plain English
- Mastering the JS interview by answering, What is closure? Note: examples are ES6
