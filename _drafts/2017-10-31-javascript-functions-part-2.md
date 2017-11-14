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
- Returns a new function with the value of _this_ locked (bound) to a function – “this is handcuffed and locked down”  
Simple Example
```
let boundFunction = myFunction.bind(thisValue);
```
```
let boundFunctionWithParam = myFunction.bind(thisValue, param);
```

More complex example in [JSFiddle](https://jsfiddle.net/f5vs5jug/11/) that illustrates helpful use cases of _bind_
- Be sure to read the comments as this example is showcasing a few different concepts

```
/**
 * Example illustrating usage of bind with event handlers
 */

//div to print our output
var output = document.querySelectorAll('#output')[0];
//instance of HeaderNavigation
var nav;

/**
 * HeaderNavigation component
 * @example
 * var myNav = new HeaderNavigation();
 */
var HeaderNavigation = (function() {
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
    //notice that 'back button' is printed to the screen, but not "going to stage: ..."
    //NOTE: By hitting "F12" to see the developer tools console, you will
    //notice that there is an error "uncaught TypeError: this.goToStage is not a function"
    //This occurs because the "this" in the case below refers to the back button
    //not to our Navigation
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
   * @param {string} stage the stage to nagivate to (current prints)
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
 * Print the value to the screen by writing the info to the innerHTML of our output div
 * @param {string} value the info to write to the DOM (i.e. print to screen)
 */
function print(value) {
  output.innerHTML += value;
  output.innerHTML += '<br>';
}

nav = new HeaderNavigation();
```

### Why/when would you use this function?
  - you want to lock in the value of _this_, helpful for event handlers
  - want to “partially apply” functions (“partial function application” is beyond the current scope of our discussion, but feel free to read up on it!)

### Conclusion
TBD

### Additional Resources
- Great definitions with examples from Mozilla on[bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
- TL;DR overview of call/apply/bind three functions from [codeplanet](https://codeplanet.io/javascript-apply-vs-call-vs-bind)
- An in depth walkthrough by [JavascriptIsSexy](http://javascriptissexy.com/javascript-apply-call-and-bind-methods-are-essential-for-javascript-professionals/) on all three essential methods
