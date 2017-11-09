---
layout: post
title:  "JavaScript Functions - Part 2: Call, Apply, Bind"
date:   2017-10-24 10:50:00 -0400
categories: jekyll javascript functions
---

### Introduction
Functions are first class objects, which gives them full access to properties and member functions.  Three key members of the Function object are _call_, _apply_, and _bind_. These methods allow us to reuse functions, simplify the passing of arguments, and even lock in the value of _this_.  

The following post will cover _call_ and _apply_. Let's dive in.  

### Definitions:
- **call** – method of the Function object that invokes a function with a specified _this_ value and individual arguments
- **apply** – method of the Function object that invokes a function with a specified _this_ value and an array of arguments

### call and apply
  - Execute the current function immediately and returns the result of the action
  - Allows you to specify the value of this – “who is this?”
  - Note: if the value of _this_ is not defined, the global (window in the browser) object will be used

So let's say I have an awesome function:
```
function awesomeFunction (awesomeValue) {
  console.log('Everything this is %o', awesomeValue);
}
```
We can invoke this function our standard way as outlined [here](https://ajahne.github.io/blog/jekyll/javascript/functions/2017/10/09/javascript-functions-part-1.html)

```
awesomeFunction('Awesome'); //Everything is awesome
```

We can also use call (or apply, but let's start with call) to invoke this function like so

```
aweseomeFunction.call(null, 'Awesome'); //Everything is awesome
```

or with apply

```
aweseomeFunction.apply(null, ['Awesome']); //Everything is awesome
```

Now let's break this down a little bit as there are a few things going on

1) Why did we pass in _null_?  
We passed in null as the first paramater to call is the _thisValue_. In our case, we are not referencing _this_ (it is not used at all in our function) so we can pass in null. We will explore using the _thisValue_ paramater in the later examples when chain constructors. 
 
2) What's going on with the second parameter?  
These are the parameters to our function. In the case of _awesomeFunction_ there is only one paramter, the value of aweome that we will log.  As _call_ takes individual and _apply_ takes an array, we pass the paramers in accordingly.

**So what if we had a function that took multiple parameters, how might that look?**  
Glad you asked, let's try that out.

```
function add(a, b) {
  return a + b;
}
```

Now let's invoke
```
add(5,10) //15;
```

How would this look with call?
```
add.call(null, 5, 10) //15;
```

And apply?
```
add.apply(null, [5,10]) //15;
```

Ok, so as we mentioned call and apply allow you to specify the value of _this_

So the genereal form of each is:  
**call**

```
myFunction.call(thisValue, param1, param2, param3);
```

**apply**
```
myFunction.apply(thisValue, [param1, param2, param3]);
```

**So what's the benefit?**
- Well, these functions allow you to reuse (borrow) functions – “you have some cool functionality, may I use it”?
Example:
```
let upper = "HELLO WORLD";
let lower = String.prototype.toLowerCase.call(upper);
```
- Allows you to utilize inheritance in the form of “parent” function calls (similar to above point, but utilized frequently for “class” based design patterns in JavaScript) – “And I thought you said there weren’t any classes in JS…” (Note: there aren’t! J)
```
/**
 * Example illustrating usage of call and apply to utilize "parent" function calls and implement
 * inheritance-like features
 */

let iverson;
let kobe;

/**
 * Print the value to the screen by writing the info to the innerHTML of our output div
 * @param {string} value the info to write to the DOM (i.e. print to screen)
 */
function print(value) {
    output.innerHTML += value;
    output.innerHTML += '<br>';
}

/**
 * Player function used to create a new player
 * @param {String} name - name of the player
 * @param {Number} number - the number on the player's jersey
 */
function Player(name, number) {
    this.name = name;
    this.number = number;
}

/**
 * Player function used to create a new point guard
 * @param {String} name - name of the player
 * @param {Number} number - the number on the player's jersey
 */
function PointGuard(name, number) {
    //note usage of call
    Player.call(this, name, number);
    this.position = 'PG';
}

/**
 * Player function used to create a new shooting guard
 * @param {String} name - name of the player
 * @param {Number} number - the number on the player's jersey
 */
function ShootingGuard(name, number) {
    //note usage of apply
    Player.apply(this, arguments);
    this.position = 'SG';
}

iverson = new PointGuard('Allen Iverson', 3);
kobe = new ShootingGuard('Kobe Bryant', 24);

console.log(iverson.name + ' ' + iverson.number + ' ' + iverson.position);  //Allen Iverson 3 PG
console.log(kobe.name + ' ' + kobe.number + ' ' + kobe.position);           //Kobe Bryant 24 SG
```
- [Link to example as JSFiddle](https://jsfiddle.net/0z3pyy27/2/)


### Why/when would you use these functions?
- **call/apply**
  - you want to reuse a previously defined function, such as for inheritance
  - you want to borrow another function’s capabilities
- **apply**
  - you want to pass in an array of parameters vs specifying each parameter individually (using apply)

### Readings
- Great definitions with examples from Mozilla on [call](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call), [apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply), and [bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
- TL;DR overview of call/apply/bind from [codeplanet](https://codeplanet.io/javascript-apply-vs-call-vs-bind)
- An in depth walkthrough by [JavascriptIsSexy](http://javascriptissexy.com/javascript-apply-call-and-bind-methods-are-essential-for-javascript-professionals/) on all three essential methods

### Questions
- What is an area in your own code where you could utilize call/apply? What about bind?
- If this is set to null or undefined for call or apply, what this object does the function operate on?
- What is the key difference between call and apply?

### Conclusion
TBD
