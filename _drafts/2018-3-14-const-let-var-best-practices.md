---
layout: single
title:  "CONST, LET, and VAR Best Practices"
date:   2018-3-14 10:10:29 -0400
categories: javascript
header:
  image: /assets/images/const-let-var.jpg
---
So when should you use `const`, `let` or `var`?

## TL;DR
- Use `const` by default  
- Use `let` only if you need to reassign a variable  
- Do not use `var`

Note: our tl;dr is also a table of contents!  So click to jump to a section or just scroll your way through.  Your choice and I support both options!

## Before we get started
This is not an introduction to `const`, `let`, and `var`.  This article assumes you are familiar with these different types of variable declarations.  If you need an intro, here are a couple great resources.
- [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) and [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) from Mozilla
- link 2
- link 3

Ready?  Let's go!


- A variable should represent one thing


## Use `const` by default
> `const` is not a value that doesn't change, but rather it is an identifier that does not get reassigned.

A `const` cannot be reassigned, but values are still mutable when dealing with [complex types (e.g. Objects)]({{ site.baseurl }}{% post_url 2018-1-29-javascript-value-vs-reference %})

`const` is not a value that doesn't change, but rather it is an identifier that does not get reassigned.
{% highlight js %}
//working with primitives
const WAIT_TIME = 5;

const WAIT_TIME = 10;
{% endhighlight %}

Working with complex types
{% highlight js %}
//working with primitives
const superHero = {name:'Black Panther', secretIdentity:'T'};

//while we cannot reasign the binding, we can change the value

const WAIT_TIME = 10;
{% endhighlight %}


True immutability can be obtained through using const with primitive types.

Change `const` to `let` once you see the value contained by the variable needs to change

Why? This will help you clearly denote which variables should change and which should not.  This helps general readability as other developers will have a clearer sense of what variables change throughout program execution and which do not.

By following these practices we can easily single to ourselves and others reading our code what values should change and which should not.
{% highlight js %}
const WAIT_TIME = 5;
const widget = new Widget();
let count = 0;
{% endhighlight %}

The added benefit of using `const` is that we will receive an error if we try to reassign our identifier
{% highlight js %}
const WAIT_TIME = 5;

//later in the code

WAIT_TIME = 10; //TypeError: Attempted to assign to readonly property.
{% endhighlight %}


## When should I use `let`?
So when use let?
When the value of the identifier needs to change.  Some examples
- for loops (i)
- Counters (keeping track of current number of DOM child elements)
- Mathematical formulas
- Form data (i.e. text input value while user is typing)
- Flip a boolean flag/toggle

better for loops with `let`
{% highlight js %}
for (let i =0; )
{% endhighlight %}

## Never use `var`

*wait, really? Never as in never?*
Exactly, nope never, not ever.

*Ok, there has to be some cases where using var is OK*
Nah. We do not want to pollute the global scope. When creating variables using `var`, not only do we have to deal with hoisting, but we also inadvertently add properties to the global object. In this case of the browser, this is `window`, check it out.

{% highlight js %}

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


## Additional resources
- Eric Elliot: https://medium.com/javascript-scene/javascript-es6-var-let-or-const-ba58b8dcde75
- Zakas: ES6
- The Dr guy
- Ponyfoo: https://ponyfoo.com/articles/var-let-const
- Reddit:
