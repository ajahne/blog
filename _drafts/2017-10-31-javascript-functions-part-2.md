---
layout: post
title:  "JavaScript Functions - Part 2b: Bind"
date:   2017-10-31 10:50:00 -0400
categories: jekyll javascript functions
---

### Introduction
Functions are first class objects, which gives them full access to properties and member functions.  Three key members of the Function object are _call_, _apply_, and _bind_. These methods allow us to reuse functions, simplify the passing of arguments, and even lock in the value of _this_.  

The following post will cover _bind_. Let's dive in.  

### Definition:
- **bind** – method of the Function object that creates a new function that when called has it’s _this_ value mapped to the given parameter and uses the set arguments
### bind
- Returns a new function with the value of this locked (bound) to a function – “this is handcuffed and locked down”
Simple Example
```
let boundFunction = myFunction.bind(thisValue);
```
```
let boundFunctionWithParam = myFunction.bind(thisValue, param);
```

More complex example in [JSFiddle](https://jsfiddle.net/f5vs5jug/11/) that illustrates helpful use cases of bind
- Be sure to read the comments as this example is showcasing a few different concepts

### Why/when would you use this function?
  - you want to lock in the value of _this_, helpful for event handlers
  - want to “partially apply” functions (“partial function application” is beyond the current scope of our discussion, but feel free to read up on it!)

### Readings
- Great definitions with examples from Mozilla on[bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
- TL;DR overview of call/apply/bind three functions from [codeplanet](https://codeplanet.io/javascript-apply-vs-call-vs-bind)
- An in depth walkthrough by [JavascriptIsSexy](http://javascriptissexy.com/javascript-apply-call-and-bind-methods-are-essential-for-javascript-professionals/) on all three essential methods

### Questions
- What is an area in your own code where you could utilize call/apply? What about bind?
- If this is set to null or undefined for call or apply, what this object does the function operate on?
- What is the key difference between call and apply?

### Conclusion
TBD
