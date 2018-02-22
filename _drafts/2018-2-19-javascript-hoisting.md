---
layout: single
title:  "JavaScript Hoisting"
date:   2018-2-19 21:45:29 -0400
---
Hoisting is the process of lifting and declaring a variable defined with `var` to the top of its scope, be it functional scope (if defined in function) or global scope (if declared outside of a function). Additionally, function declarations are hoisted to the top of the current scope as well.

Let's dive into some code.

## Hoisting Variables
{% highlight js %}
console.log(a);   //null
var a = 5;
{% endhighlight %}

The above is actually created as
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

### Let's go a bit further, what about variable hoisting within a function?
{% highlight js %}
function getValue() {

}
{% endhighlight %}

## Hoisting Functions
Function declarations are hoisted to the top of the scope chain (e.g. the top of file)
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

### Function Hoisting overrides variable hoisting

## ES6 Block Scope and Hoisting
The good news is that block scope helps us avoid pitfalls introduced through with hoisting.  
Let's bring back our previous example instead using `let` and `const` instead of `var`.

{% highlight js %}
console.log(a);   //ReferenceError: can't access lexical declaration 'a' before initialization
let a = 5;
{% endhighlight %}

And we will get the same error with `const`
{% highlight js %}
console.log(a);   //ReferenceError: can't access lexical declaration 'a' before initialization
const a = 5;
{% endhighlight %}

In this case, the errors are a good thing!  We do not want to inadvertently access a variable before we have declared and initialized it.  This will help us create cleaner and more maintenable code by know what we write is actual order of operation. 

## Conclusion
Identifiers (i.e. variables) declared with the `var` key word are created as if they are defined at the top of the scope (be it function or global).  This process is called "hoisting" and applies to variables defined with `var` and function declarations.

## Additional Resources
- Hoisting definition by [Mozilla](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)
- `var` definition from [Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
- [JavaScriptIsSexy](http://javascriptissexy.com/javascript-variable-scope-and-hoisting-explained/) on variable hoisting
- Getting [back to basics on JavaScript Hoisting](https://www.sitepoint.com/back-to-basics-javascript-hoisting/) with Sitepoint
