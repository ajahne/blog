---
layout: single
title:  "JavaScript Functions - Part 2: Call and Apply"
date:   2017-10-24 10:50:00 -0400
categories: javascript
header:
  image: /assets/images/functions-part2-call-apply.jpg
---
Functions are [first class objects](https://stackoverflow.com/questions/705173/what-is-meant-by-first-class-object), which gives them full access to properties and methods.  Three key methods of the Function object are _call_, _apply_, and [_bind_]({{ site.baseurl }}{% post_url 2017-10-31-javascript-functions-part-3 %}). These methods allow us to reuse functions, simplify the passing of arguments, and even lock in the value of _this_.  

In the following post, we will cover _call_ and _apply_, while a follow up will talk about _bind_.  Often these three methods are combined in the same discussion, mainly due to each being a key method of the Function object, not necessarily because they are linked.  Two of these, _call_ and _apply_ are similar, so let's dive in and get to some definitions and examples.  

### Definitions:
- **call** – method of the Function object that invokes a function with a specified _this_ value and **individual arguments**
- **apply** – method of the Function object that invokes a function with a specified _this_ value and **an array of arguments**

### call and apply
  - Executes the current function immediately and returns the result of the action
  - Allows you to specify the value of _this_
    - Note: if the value of _this_ is not defined, the global (window in the browser) object will be used

So let's say I have an awesome function:
{% highlight js %}
function awesomeFunction (awesomeValue) {
  console.log('Everything is %o', awesomeValue);
}
{% endhighlight %}
We can invoke this function our standard way as outlined [here](https://ajahne.github.io/blog/jekyll/javascript/functions/2017/10/09/javascript-functions-part-1.html)

{% highlight js %}
awesomeFunction('Awesome'); //Everything is awesome
{% endhighlight %}

We can also use _call_ to invoke our function

{% highlight js %}
aweseomeFunction.call(null, 'Awesome'); //Everything is awesome
{% endhighlight %}

or use _apply_

{% highlight js %}
aweseomeFunction.apply(null, ['Awesome']); //Everything is awesome
{% endhighlight %}

Now let's break this down a little bit as there are a few things going on

**1) Why did we pass in _null_?**  
We passed in _null_ as the first parameter to _call_ and _apply_ is the _thisValue_. In our case, we are not referencing _this_ (it is not used at all in our function) so we can pass in _null_. We will explore using the _thisValue_ parameter in the later examples when we chain constructors below.

**2) What's going on with the second parameter?**  
These are the parameters to our function. In the case of _awesomeFunction_ there is only one parameter, the `awesomeValue` that we will log.  As _call_ takes individual parameters and _apply_ takes an array, we pass the parameters in accordingly.

**So what if we had a function that took multiple parameters, how might that look?**  
Glad you asked, let's try that out.

{% highlight js %}
function add(a, b) {
  return a + b;
}
{% endhighlight %}

Now let's invoke the standard way
{% highlight js %}
add(5,10) //15;
{% endhighlight %}

How would this look with _call_?
{% highlight js %}
add.call(null, 5, 10) //15;
{% endhighlight %}

And _apply_?
{% highlight js %}
add.apply(null, [5,10]) //15;
{% endhighlight %}

So the genereal form of each is:  
**call**

{% highlight js %}
myFunction.call(thisValue, param1, param2, param3, ... paramN);
{% endhighlight %}

**apply**
{% highlight js %}
myFunction.apply(thisValue, [param1, param2, param3, ... paramN]);
{% endhighlight %}

**Great, but ummm, why would I ever want to do this? In the example you showed, isn't the standard way less involved, less characters to type, and doesn't require me to pass in some weird _null_ parameter.**  
Why yes, the example was a simple one to show the general form of each function, you know walk before we can run and all that. Now that we have the basic syntax, let's go further.  Newness coming right up...

**Benefits of call and apply**    
These functions allow us to reuse (borrow) functions – “you have some cool functionality, may I use it”?
{% highlight js %}
const upper = "HELLO WORLD";
const lower = String.prototype.toLowerCase.call(upper);
{% endhighlight %}

**Simplifying function calls**    
Say I have an array of numbers and I want to find the highest number.  I might make a function similar to the one below
{% highlight js %}
const numbers = [5,8,3,9,11,2];

function getMax() {
  let max = numbers[0];
  for (let i = 1; i < numbers.length; i++) {
    if (numbers[i] > max) {
      max = numbers[i];
    }
  }
  return max;
}
{% endhighlight %}

So how might we leverage our newfound tools to simplify this code? We can do so by utilizing _apply_.
{% highlight js %}
const numbers = [5,8,3,9,11,2];

function getMax() {
  return Math.max.apply(null, numbers);
}
{% endhighlight %}


**Ok, but what else can we do?**  
Additionally, These methods allow us to utilize inheritance in the form of “parent” function calls (similar to the above point, but utilized frequently for “class” based design patterns in JavaScript)
{% highlight js %}
/**
 * Example illustrating usage of call and apply to utilize "parent"
 * function calls and implement inheritance-like features
 */

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

const iverson = new PointGuard('Allen Iverson', 3);
const kobe = new ShootingGuard('Kobe Bryant', 24);

console.log(`${iverson.name} ${iverson.number} ${iverson.position}`);  //Allen Iverson 3 PG
console.log(`${kobe.name} ${kobe.number} ${kobe.position}`);           //Kobe Bryant 24 SG
{% endhighlight %}
[Link to repl example](https://repl.it/repls/VigorousHandyNetworking)


**What about other positions and players?**  
I leave that as an exercises for the reader/voice in my head to code up.

### Why/when would you use these functions?
- **call/apply**
  - you want to reuse a previously defined function, such as for inheritance
  - you want to borrow another function’s capabilities
- **apply**
  - you want to pass in an array of parameters vs specifying each parameter individually

### Conclusion
Phew, not so bad, right? Right! In this post we have defined _call_ and _apply_, provided examples that show how to use each method, and outlined key benefits. By using _call_ and _apply_ we can reuse an object's methods, simplify function calls, and borrow constructors to create "class" based design. How might you be able to utilize _call_ and _apply_ in your programs?

### Additional Resources
- Great definitions with examples from Mozilla on [call](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call) and [apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
- TL;DR overview of call/apply/bind from [codeplanet](https://codeplanet.io/javascript-apply-vs-call-vs-bind)
- An in depth walkthrough by [JavascriptIsSexy](http://javascriptissexy.com/javascript-apply-call-and-bind-methods-are-essential-for-javascript-professionals/) on all _call_, _apply_, and _bind_
