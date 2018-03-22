---
layout: single
title:  "CONST, LET, and VAR Best Practices"
date:   2018-3-22 2:35:29 -0400
categories: javascript
header:
  image: /assets/images/const-let-var-apples.jpg
---
When should you use `const`, `let`, or `var`?

## TL;DR
- [Use `const` by default](#use-const-by-default)  
- [Use `let` only if you need to reassign a variable](#use-let-only-if-you-need-to-reassign-a-variable)  
- [Do not use `var`](#do-not-use-var)

**Note**: the tl;dr is also a table of contents!  So click to jump to a section or just scroll your way through.  It's your choice and I support both options!

## Before we get started
This article assumes you are familiar with the different types of variable declarations in ES6+ (e.g. `const`, `let`, and our old friend `var`).  If you need an introduction, here are a few great resources.
- [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) and [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) from Mozilla
- [A gentle introduction to ES6: const, let, var](https://hackernoon.com/js-var-let-or-const-67e51dbb716f) on hackernoon
- [You Don't Know JS - Chapter 2: Syntax](https://github.com/getify/You-Dont-Know-JS/blob/master/es6%20%26%20beyond/ch2.md) by Kyle Simpson

Ready?  Let's go!

## Goals of these best practices
- Define a standard variable declaration ruleset
- Make our code consistent and easier to read
- Signal code intent (i.e. is this variable meant to change or not)
- Avoid unintended issues (e.g. [hoisting]({{ site.baseurl }}{% post_url 2018-2-19-javascript-hoisting %}), global object pollution)

## Use `const` by default
A variable should represent one thing. Declaring our variables with `const` helps us achieve this goal as we cannot change the assignment of our identifier once it has been initialized. We also leave a message (i.e. signal) in our code to our future selves and future developers that this variable should not be reassigned.

> `const` is not a value that doesn't change, but rather it is an identifier that does not get reassigned.

{% highlight js %}
const WAIT_TIME = 5;
WAIT_TIME = 10; //TypeError: Attempted to assign to readonly property.
{% endhighlight %}

Note, that while variables declared with `const` cannot be reassigned, the values are still mutable when dealing with [complex types (i.e. Objects)]({{ site.baseurl }}{% post_url 2018-1-29-javascript-value-vs-reference %})

{% highlight js %}
const coolestHero = {
  name: 'Iron Man'
};

//while we cannot reassign the binding, we can change the value
coolestHero.name = 'Black Panther';
{% endhighlight %}

True immutability can be obtained through using `const` with primitive types.

**Change `const` to `let` once you see the value contained by the variable needs to change**

Why? This will help you clearly denote which variables should change and which should not.  Following this principal helps improve code readability as other developers will have a clearer sense of what variables change throughout program execution and which do not.

## Use `let` only if you need to reassign a variable  
Some examples:
- `for` loops (e.g. i, j, etc.)
- Counters (e.g. for keeping track of the current number of DOM children)
- Mathematical formulas
- Form data (i.e. text input value while the user is typing)
- Toggling a boolean flag

Let's create better for loops with `let`
{% highlight js %}
const messages = ['Hello World', 'Wakanda Forever', 'Good morning'];
for (let i = 0; i < messages.length; i++) {
  console.log(messages[i]);
};
{% endhighlight %}

## Do not use `var`
_In honor of our old friend `var`, let's talk it out and have a little fun..._  

**_Hello, Ajahne_**  
What's up?

**_So I really shouldn't use `var` anymore?_**  
Nope.

**_Why not?_**  
Well for one, using `var` has side effects and pollutes the global scope. When creating variables using `var`, not only do we have to deal with [hoisting]({{ site.baseurl }}{% post_url 2018-2-19-javascript-hoisting %}), but we also inadvertently add properties to the global object. Check it out.

{% highlight js %}
var title = 'Awesome Web Page';
//note: window is the global browser object
console.log(window.title);  //Awesome Web Page
{% endhighlight %}

**_Well, I just won't use `var` in the global scope and I'll be fine._**  
Not so fast, `var` does not support [block scope]({{ site.baseurl }}{% post_url 2018-1-11-javascript-scope %}).  
{% highlight js %}
var x = 10;
if (true) {
  var x = 5;
  console.log(x); //5
}
console.log(x);   //5
{% endhighlight %}

**_Well then._**  
Yep, that one has caught many a developer.  

**_So what if I am writing legacy JavaScript or am working in a mixed code base?_**  
If you must use `var`, be sure to declare your variables at the top of your scope chain. But really, it's time to pour one out for `var`.  Start targeting modern browsers and/or incorporating [babel](https://babeljs.io) into your workflow :).

## Conclusion
By following these best practices for using `const`, `let`, and `var`, we can easily signal to ourselves and others the intent of our variables within the code.
{% highlight js %}
const WAIT_TIME = 5;
const widget = new Widget();
let count = 0;
{% endhighlight %}

Additionally, by utilizing these best practices, we create a consistent ruleset for our variables, avoid legacy declaration 'gotchas', and - ultimately - produce cleaner code.

Be sure to check out the additional resources below and happy coding!

## Additional resources
- [Nicholas Zakas](https://leanpub.com/understandinges6/read#leanpub-auto-emerging-best-practices-for-block-bindings) on emerging best practices for `const` and `let`
- [Eric Elliott](https://medium.com/javascript-scene/javascript-es6-var-let-or-const-ba58b8dcde75) on `var`, `let`, and `const`
- From `var` to `const` in [exploringjs](http://exploringjs.com/es6/ch_core-features.html#sec_from-var-to-const)
- `var`, `let`, `const` overview on [Ponyfoo](https://ponyfoo.com/articles/var-let-const)
