---
layout: single
title:  "Hoisting in JavaScript"
date:   2018-2-23 0:49:29 -0400
categories: javascript
---
>Hoisting is the process of lifting and declaring a variable defined with `var` to the top of its scope, be it functional scope (if defined in function) or global scope (if declared outside of a function). Additionally, function declarations are hoisted to the top of the current scope as well.

Let's dive into some code.

## Hoisting Variables
So now that we have our definition, what do mean by "lifted and declared"?
{% highlight js %}
console.log(a);   //null
var a = 5;
{% endhighlight %}

The above is actually executed as the following:
{% highlight js %}
var a;
console.log(a);   //null
a = 5;
{% endhighlight %}

We can see the difference between declaring a variable (that is hoisted) and not declaring a variable at all.
{% highlight js %}
console.log(a);   //null
console.log(b);   //ReferenceError: Can't find variable: b
var a = 5;
{% endhighlight %}

Let's go a bit further, what about variable hoisting within a function?
{% highlight js %}
function getX() {
  if (condition) {
    var x = 5;    
    // x exists with a value of 5
    return x;
  } else {
    // x exists with a value of null
    return null;
  }
  // x exists with a value of null
}
{% endhighlight %}

Given that there is no block scope when using `var`, the variable `x` is hoisted to the top of the function.
{% highlight js %}
function getX() {
  var x;
  if (condition) {
    x = 5;    
    // x exists with a value of 5
    return x;
  } else {
    // x exists with a value of null
    return null;
  }
  // x exists with a value of null
}
{% endhighlight %}

As variables as hoisted, so are function declarations.

## Hoisting Functions
Function declarations are hoisted to the top of the scope chain.
{% highlight js %}
console.log(add(1,2));   //3

function add(a,b) {
  return a+b;
}
{% endhighlight %}

Function expressions are not hoisted
{% highlight js %}
console.log(add(1,2));   //TypeError: add is not a function. (In 'add(1,2)', 'add' is undefined)

var add = function(a,b) {
  return a+b;
}
{% endhighlight %}

Function hoisting overrides variable hoisting
{% highlight js %}
console.log(typeof foo);  //function
var foo;
function foo() {
  return 'bar';
}
console.log(typeof foo);  //function
{% endhighlight %}

For reference, if we did not have the function declaration, our log statement would print `undefined`
{% highlight js %}
console.log(typeof foo);  //undefined
var foo;
{% endhighlight %}

Initializing our variable will override the function declaration.
{% highlight js %}
console.log(typeof foo);  //function
var foo = 'baz';
function foo() {
  return 'bar';
}
console.log(typeof foo);  //string
{% endhighlight %}

This is because during execution, the above example is actually changed to the following:
{% highlight js %}
function foo() {
  return 'bar';
}
var foo;
console.log(typeof foo);  //function
foo = 'baz';
console.log(typeof foo);  //string
{% endhighlight %}

Confusing, no? Shouldn't what we write at author time (i.e. the lexical scope) be the same as what is happening during execution? Why yes, yes it should be.  Enter ES6!

## ES6 Block Scope and Hoisting
The good news is that block scope helps us avoid pitfalls introduced with hoisting. Let's bring back our previous example using `let` and `const` instead of `var`.

Using `let` in this manner will trigger an error.
{% highlight js %}
console.log(a);   //ReferenceError: can't access lexical declaration 'a' before initialization
let a = 5;
{% endhighlight %}

And we will get the same error with `const`.
{% highlight js %}
console.log(a);   //ReferenceError: can't access lexical declaration 'a' before initialization
const a = 5;
{% endhighlight %}

In this case, the errors are a good thing!  We do not want to inadvertently access a variable before we have declared and initialized it.  This will help us create cleaner and more maintainable programs as the JavaScript engine will execute the code in the order that we wrote it (i.e. author time).

## Conclusion
Identifiers (i.e. variables) declared with the `var` keyword are created as if they are defined at the top of the scope (be it function or global).  This process is called "hoisting" and applies to variables defined with `var` and function declarations.

While block scope with `const` and `let` allows us to avoid the pitfalls of hoisting when writing modern JavaScript, it is still important to understand this concept as you may work in a mixed code base (e.g. ES5 and ES6), are writing ES5 and below based on your requirements, or are simply curious of all JavaScript's quirks and are targeting a 100% completion rate.

Check out the further reading below and happy coding!

## Additional Resources
- Hoisting definition by [Mozilla](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)
- `var` definition from [Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
- [JavaScriptIsSexy](http://javascriptissexy.com/javascript-variable-scope-and-hoisting-explained/) on variable hoisting
- Getting [back to basics on JavaScript Hoisting](https://www.sitepoint.com/back-to-basics-javascript-hoisting/) with Sitepoint
