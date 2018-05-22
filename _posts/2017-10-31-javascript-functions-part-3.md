---
layout: single
title:  "JavaScript Functions - Part 3: Bind"
date:   2017-10-31 10:50:00 -0400
categories: javascript
header:
  image: /assets/images/functions-part3-bind.jpg
---
As we have learned in [part 1](https://ajahne.github.io/blog/jekyll/javascript/functions/2017/10/09/javascript-functions-part-1.html) of our series, functions are [first class objects](https://stackoverflow.com/questions/705173/what-is-meant-by-first-class-object), which gives them full access to properties and methods. In [part 2](https://ajahne.github.io/blog/jekyll/javascript/functions/2017/10/24/javascript-functions-part-2.html), we examined [_call_ and _apply_](https://ajahne.github.io/blog/jekyll/javascript/functions/2017/10/24/javascript-functions-part-2.html).  In the following post we will cover another core method of the Function object, _bind_. Let's dive in.  

### Definition:
**bind** – method of the Function object that creates a new function that when called has it’s _this_ value mapped to the given parameter and uses the set arguments.

_bind_ returns a new function with the value of _this_ locked (bound) to a function  
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


### Example 1 - locking in the value of _this_
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

### Example 2 - partial function application
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

### Example 3 - using _bind_ in event handling

This is a more complex example to highlight the usage of _bind_.  **Please be sure to read the comments as this example is showcasing a few different concepts.**

{% highlight html %}
<div class="navigation">
  <button class="button-help" name="help button">Help</button>
  <button class="button-back" name="back button">Back</button>
  <button class="button-next" name="next button">Next</button>
</div>
{% endhighlight %}

{% highlight js %}
/**
 * Example illustrating usage of bind with event handlers
 */

/**
 * HeaderNavigation component
 * @example
 * const nav = new HeaderNavigation();
 */
const HeaderNavigation = (function() {
  'use strict';

  /**
   * Constructor
   */
  function Navigation() {
    this.name = 'navigation';
    this.init();
  }

  /**
   * Initialize our Navigation object
   * Get DOM elements for our nav: help, back, and next buttons
   * Add event listeners to each button
   */
  Navigation.prototype.init = function() {
    const nav = document.querySelectorAll('.navigation')[0];
    const buttonHelp = nav.querySelectorAll('.button-help')[0];
    const buttonBack = nav.querySelectorAll('.button-back')[0];
    const buttonNext = nav.querySelectorAll('.button-next')[0];

    //example of binding an anonymous function
    buttonHelp.addEventListener('click', function() {
        this.showHelp();            
    }.bind(this));

    //do not bind the value of "this" to the back button
    //notice that "back button" is printed to the screen, but
    //not "going to stage: ..."
    //NOTE: By hitting "F12" to see the developer tools console,
    //you will notice that there is an error
    //"TypeError: this.goToStage is not a function"
    //This occurs because the "this" in the case below refers
    //to the back button not to our Navigation
    buttonBack.addEventListener('click', this.click);

    //bind the click function to our Navigation Object
    //the "this" in .bind(this) refers to the Navigation Object
    buttonNext.addEventListener('click', 
                                this.click.bind(this, 'Stage 1'));
  };

  /**
   * Handle button click event
   * print the name of "this" (for tracking/testing)
   * go to the corresponding stage
   */
  Navigation.prototype.click = function() {
    console.log(`click: 'this' is the ${this.name}`);
    this.goToStage(arguments[0]);
  };

  /**
   * Print the stage we need to navigate to
   * @param {string} stage the stage to navigate to
   */
  Navigation.prototype.goToStage = function(stage) {
    console.log(`going to stage: ${stage}`);
  };

  Navigation.prototype.showHelp = function() {
  	alert(`You are now being helped by the ${this.name} :)`);
  }

  return Navigation;
}());

//Instantiate an instance of HeaderNavigation
const nav = new HeaderNavigation();
{% endhighlight %}
Link to [JSFiddle](https://jsfiddle.net/f5vs5jug/11/).


### Why/when would you use this function?
  - you want to lock in the value of _this_, helpful for event handlers (see: example 1 and example 3)
  - want to “partially apply” functions by locking in arguments (see: example 2)

### Conclusion
The Function object is a fundamental component of the JavaScript language and learning to leverage its _bind_ method can help us simplify code and promote reusability. Through examples, we have observed how _bind_ can be used to lock in the value of _this_, which is helpful to borrow functions and to ensure we are targeting the correct object in our programs (e.g. in event handlers).  By leveraging _bind_ we can also create partially applied functions that allow us to reuse arguments and functionality. For further reading, check out the additional resources below and be sure to try out your own examples.

### Additional Resources
- Great definitions with examples from [Mozilla on bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
- TL;DR overview of call/apply/bind functions from [codeplanet](https://codeplanet.io/javascript-apply-vs-call-vs-bind)
- An in depth walkthrough by [JavascriptIsSexy](http://javascriptissexy.com/javascript-apply-call-and-bind-methods-are-essential-for-javascript-professionals/) on all three essential methods
