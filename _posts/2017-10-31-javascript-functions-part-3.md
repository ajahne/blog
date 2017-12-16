---
layout: post
title:  "JavaScript Functions - Part 3: Bind"
date:   2017-10-31 10:50:00 -0400
categories: jekyll javascript functions
---

### Introduction
As we have learned in [part 1](https://ajahne.github.io/blog/jekyll/javascript/functions/2017/10/09/javascript-functions-part-1.html) of our series, functions are [first class objects](https://stackoverflow.com/questions/705173/what-is-meant-by-first-class-object), which gives them full access to properties and methods. In [part 2](https://ajahne.github.io/blog/jekyll/javascript/functions/2017/10/24/javascript-functions-part-2.html), we examined [_call_ and _apply_](https://ajahne.github.io/blog/jekyll/javascript/functions/2017/10/24/javascript-functions-part-2.html).  In the following post will cover another core method of the Function object, _bind_. Let's dive in.  

### Definition:
**bind** – method of the Function object that creates a new function that when called has it’s _this_ value mapped to the given parameter and uses the set arguments.

_bind_ returns a new function with the value of _this_ locked (bound) to a function – “this is handcuffed and locked down”  
General form:
{% highlight js %}
aFunction.bind(_thisValue_, arg1, arg2,..., argN); 
{% endhighlight %}

### Examples
{% highlight js %}
let boundFunction = myFunction.bind(thisValue);
{% endhighlight %}

{% highlight js %}
let boundFunctionWithParam = myFunction.bind(thisValue, param);
{% endhighlight %}


#### Example 1 - locking in the value of _this_
{% highlight js %}
this.name = "Global";
const component = {
  name: "Component",
  getName: function() {
    return this.name;
  }
};

const getName = component.getName;

console.log(getName()); // "Global"

const boundGetName = getName.bind(component);
console.log(boundGetName()); //"Component"
{% endhighlight %}

So what happened in our previous example? Why was "Component" printed and not "Global"?  The reason is that we bound the _this_ value to our component object.  Even though the first call to getName() returns "Global", we subsequently locked the value of _this_ to the component in our bound function.

#### Example 2 - partial function application
We can also utilize _bind_ to create a function with a predefined set of arguments. 
{% highlight js %}
function multiply(x,y) {
  return x * y; 
}

//Create a function that will triple any number
const triple = multiply.bind(null,3);
console.log(triple(10));  //30
{% endhighlight %}
We have set the "x" value and pass in the value of "y" whenever we call our "triple" function.  Notice in this example how we passed in _null_ for the value of _this_ and also passed in the values last (this follows our function signature). 

#### Example 3 - using _bind_ in event handling

This is a out a more complex example to highlight the usage of bind.  **Please be sure to read the comments as this example is showcasing a few different concepts.**

{% highlight js %}
/**
 * Example illustrating usage of bind with event handlers
 */

//instance of HeaderNavigation
let nav;

/**
 * HeaderNavigation component
 * @example
 * var myNav = new HeaderNavigation();
 */
let HeaderNavigation = (function() {
  'use strict';

  /**
   * Instantiate Navigation and then initialize
   */
  function Navigation() {
    this.name = 'navigation';
    this.init();
  }

  /**
   * Initialize our Nagivation object
   * Grab the DOM elements that make up our nav: help, back, and next buttons
   * Add event listenrs to each button
   */
  Navigation.prototype.init = function() {
    this.element = document.querySelectorAll('.navigation')[0];
    this.buttonHelp = this.element.querySelectorAll('.button-help')[0];
    this.buttonBack = this.element.querySelectorAll('.button-back')[0];
    this.buttonNext = this.element.querySelectorAll('.button-next')[0];

    //using this as an example to show binding on an anonymous function
    this.buttonHelp.addEventListener('click', function() {
        this.showHelp();            
    }.bind(this));

    //do not bind the value of this to the back button
    //notice that 'back button' is printed to the screen, but 
    //not "going to stage: ..."
    //NOTE: By hitting "F12" to see the developer tools console, 
    //you will notice that there is an error 
    //"uncaught TypeError: this.goToStage is not a function"
    //This occurs because the "this" in the case below refers 
    //to the back button not to our Navigation
    this.buttonBack.addEventListener('click', this.click);

    //bind the click function to our Navigation Object
    //the this in .bind(this) refers to the Navigation Object
    this.buttonNext.addEventListener('click', this.click.bind(this, 'Stage 1'));
  };

  /**
   * Handle button click event
   * print the name of "this" (for tracking/testing)
   * go to the corresponding stage
   */
  Navigation.prototype.click = function() {
    print('click: ' + this.name);
    this.goToStage(arguments[0]);
  };

  /**
   * Print the stage we need to navigate to
   * @param {string} stage the stage to navigate to (current prints)
   */
  Navigation.prototype.goToStage = function(stage) {
    print('going to stage: ' + stage);
  };

  Navigation.prototype.showHelp = function() {
  	alert('You are now being helped :)');
  }

  return Navigation;
}());

/**
 * Print the value to the screen
 * @param {string} value the info to log 
 */
function print(value) {
  console.log(value);
}

nav = new HeaderNavigation();
{% endhighlight %}
Link to [JSFiddle](https://jsfiddle.net/f5vs5jug/11/).


### Why/when would you use this function?
  - you want to lock in the value of _this_, helpful for event handlers (see: example 1 and example 3)
  - want to “partially apply” functions by locking in arguments (see: example 2)

### Conclusion
The Function object is a fundamental component of the JavaScript language and learning to leverage its _bind_ method can help us simplify code and promote reusability. Through examples, we have observed how _bind_ can be used to lock in the value of _this_, which is helpful to borrow functions and to ensure we are targeting the correct object in our programs (e.g. in event handlers).  By leveraging _bind_ we can also create partially applied functions that allow us to reuse arguments and functionality. For further reading, check out the additional resources below and be sure to try out your own examples.

### Additional Resources
- Great definitions with examples from [Mozilla on bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
- TL;DR overview of call/apply/bind three functions from [codeplanet](https://codeplanet.io/javascript-apply-vs-call-vs-bind)
- An in depth walkthrough by [JavascriptIsSexy](http://javascriptissexy.com/javascript-apply-call-and-bind-methods-are-essential-for-javascript-professionals/) on all three essential methods
