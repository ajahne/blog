---
layout: post
title:  "JavaScript Functions - Part 2: Call, Apply, Bind"
date:   2017-10-24 10:50:00 -0400
categories: jekyll javascript functions
---

### Introduction
TBD

### Definitions:
- call – method of the Function object that calls a function with a specified this value and individual arguments
- apply – method of the Function object that calls a function with a specified this value and an array of arguments
- bind – method of the Function object that creates a new function that when called has it’s this value mapped to the given parameter and uses the set arguments

### call and apply
  - Execute the current function immediately and returns the result of the action
  - Allows you to specify the value of this – “who is this?”
Examples:
``` 
myFunction.call(thisValue, param1, param2);
```
```
myFunction.apply(thisValue, [param1, param2, param3]);
```
- Note: if the value of this is not defined, the global (window in the browser) object will be used
- Allows you to reuse (borrow) functions – “you have some cool functionality, may I use it”?
Example:
```
var upper = "HELLO WORLD";
var lower = String.prototype.toLowerCase.call(upper);
```
- Allows you to utilize inheritance in the form of “parent” function calls (similar to above point, but utilized frequently for “class” based design patterns in JavaScript) – “And I thought you said there weren’t any classes in JS…” (Note: there aren’t! J)
- [JSFiddle Example](https://jsfiddle.net/0z3pyy27/2/)

### bind
- Returns a new function with the value of this locked (bound) to a function – “this is handcuffed and locked down”
Simple Example
```
var boundFunction = myFunction.bind(thisValue);
```
```
var boundFunctionWithParam = myFunction.bind(thisValue, param);
```

More complex example in [JSFiddle](https://jsfiddle.net/f5vs5jug/11/) that illustrates helpful use cases of bind
- Be sure to read the comments as this example is showcasing a few different concepts
 
### Why/when would you use these functions?
- call/apply
  - want to reuse a previously defined function, such as for inheritance or to borrow another function’s capabilities
  - want to pass in an array of parameters vs specifying each parameter individually (using apply)
- bind
  - want to lock in the value of this, helpful for event handlers
  - want to “partially apply” functions (“partial function application” is beyond the current scope of our discussion, but feel free to read up on it!)
 
### Readings
- Great definitions with examples from Mozilla on [call](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call), [apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply), and [bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
- TL;DR overview of the three functions from [codeplanet](https://codeplanet.io/javascript-apply-vs-call-vs-bind)
- An in depth walkthrough by [JavascriptIsSexy](http://javascriptissexy.com/javascript-apply-call-and-bind-methods-are-essential-for-javascript-professionals/) on all three essential methods

### Questions
- What is an area in your own code where you could utilize call/apply? What about bind?
- If this is set to null or undefined for call or apply, what this object does the function operate on?
- What is the key difference between call and apply?

### Conclusion
TBD
