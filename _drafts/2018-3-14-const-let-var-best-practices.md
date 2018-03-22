---
layout: single
title:  "CONST, LET, and VAR Best Practices"
date:   2018-3-14 10:10:29 -0400
categories: javascript
header:
  image: /assets/images/const-let-var-apples.jpg
---
So when should you use `const`, `let`, or `var`?

## TL;DR
- Use `const` by default  
- Use `let` only if you need to reassign a variable  
- Do not use `var`

Note: our tl;dr is also a table of contents!  So click to jump to a section or just scroll your way through.  Your choice and I support both options!

## Before we get started
This article assumes you are familiar with the different types of variable declarations in ES6+ (e.g. `const`, `let`, and our old friend `var`).  If you need an introduction, here are a few great resources.
- [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) and [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) from Mozilla
- [A gentle introduction to ES6: const, let, var](https://hackernoon.com/js-var-let-or-const-67e51dbb716f) on hackernoon
- [You Don't Know JS - Chapter 2: Syntax](https://github.com/getify/You-Dont-Know-JS/blob/master/es6%20%26%20beyond/ch2.md) by Kyle Simpson

Ready?  Let's go!


## Goals of these best practices
- Simplify where and when to use the different variable declaration types
- Make our code consistent and easier to read
- Signal code intent (i.e. is this variable meant to change or not)
- Avoid unintended issues (e.g. hoisting, global scope pollution)


## Use `const` by default
A variable should represent one thing. Declaring our variables with `const` helps us achieve this goal as we cannot reassign a value to our identifier once it has been initialized. We also leave a message (i.e. signal) in our code to our future selves and future developers that our intent is this variable should not be reassigned.

> `const` is not a value that doesn't change, but rather it is an identifier that does not get reassigned.

{% highlight js %}
const WAIT_TIME = 5;
WAIT_TIME = 10; //TypeError: Attempted to assign to readonly property.
{% endhighlight %}


Note, that while variables declared with `const` cannot be reassigned, the values are still mutable when dealing with [complex types (e.g. Objects)]({{ site.baseurl }}{% post_url 2018-1-29-javascript-value-vs-reference %})

{% highlight js %}
const coolestHero = {
  name: 'Iron Man',
};

//while we cannot reassign the binding, we can change the value
coolestHero.name = 'Black Panther';
{% endhighlight %}

True immutability can be obtained through using `const` with primitive types.

Change `const` to `let` once you see the value contained by the variable needs to change

Why? This will help you clearly denote which variables should change and which should not.  Following this principal helps improve code readability as other developers will have a clearer sense of what variables change throughout program execution and which do not.

By following these practices we can easily single to ourselves and others reading our code what variables should change and which should not.
{% highlight js %}
const WAIT_TIME = 5;
const widget = new Widget();
let count = 0;
{% endhighlight %}


## Use `let` only if you need to reassign a variable  
So when should we use `let`? Only, use `let` when the value of the identifier needs to change.  

Some examples:
- `for` loops (e.g. i, j, etc.)
- Counters (e.g. for keeping track of current number of DOM children)
- Mathematical formulas
- Form data (i.e. text input value while user is typing)
- Toggle a boolean flah

better for loops with `let`
{% highlight js %}
const messages = ['Hello World', 'Wakanda Forever', 'Good morning'];
for (let i = 0; i < messages.length; i++ {
  console.log(messages[i]);
});
{% endhighlight %}

## Do not use`var`

*wait, really? Never as in never?*
Exactly, nope never, not ever.

*Ok, there has to be some cases where using var is OK*
Nah. We do not want to pollute the global scope. When creating variables using `var`, not only do we have to deal with hoisting, but we also inadvertently add properties to the global object. In this case of the browser, this is `window`, check it out.

{% highlight js %}
var title = 'Awesome Web Page';
//note: window is the global browser object
console.log(window.title);
{% endhighlight %}

## When should I use `var`?
Never use var.  

Why?
Using var has side effects, point to hoisting link.  
Var does not support block scope.  
Example

Benefits of using `const` and `let`
- Block scope
- No hoisting

## Conclusion

## Additional resources
- Eric Elliot: https://medium.com/javascript-scene/javascript-es6-var-let-or-const-ba58b8dcde75
- Zakas: ES6
- The Dr guy
- `var`, `let`, `const` overview on [Ponyfoo](https://ponyfoo.com/articles/var-let-const)
