---
layout: post
title:  "JavaScript Scope"
date:   2018-01-11 20:56:29 -0400
categories: jekyll javascript scope
---

### What is scope?
Scope defines where a variable or function is accessible. It is the current context of execution within the program. Scopes are hierarchical, where child scopes can access parent scopes, but not vice versa. Scopes can be defined globally or locally and there are three core "buckets" of scope: global, function, and block.  

### Global Scope  
By default all variables and functions defined in JavaScript are global – accessible from anywhere in our code or any other code that is being utilized in conjunction with ours.

{% highlight js %}
let greeting = 'Hello';
{% endhighlight %}

As defined at the top of our program, this variable ```greeting``` is visible everywhere in our code.

{% highlight js %}
let greeting = 'Hello';
let greet = () => {
  console.log(greeting);
}
greet(); //Hello
{% endhighlight %}


**A note regarding global scope:**
- Best Practice in JavaScript programming is to reduce polluting the global scope.  The reason is that multiple scripts may be utilized in an application and naming conflicts can cause unexpected behavior.  
  - For example if you are using ```JQuery``` in your application renaming ```$``` would create issues
- Reducing global scope can be achieved through modules and namespaces. In short, both of these reduce the pollution of global scope by placing variables and functions under one “umbrella” variable name or function. 

### Function scope
Functions can also define scope, new areas where code is "visible".

{% highlight js %}
let saySomething = () => {
  let something = 'Saying something wonderful';
  console.log(something);
}
saySomething();         //Saying something wonderful
console.log(something); //ReferenceError: Can't find variable: something
{% endhighlight %}

Here we see that our function ```saySomething``` has defined its own variable ```something```. This variable cannot be "seen" globally and therefore cannot be used outside of the ```saySomething``` function.  
Going further, we can see that function scope overrides global scope within our function.
{% highlight js %}
let something = 'something';
let saySomething = () => {
  let something = 'Saying something wonderful';
  console.log(something);
}
saySomething();         //'Saying something wonderful'
console.log(something); //something
{% endhighlight %}

### Block scope
Introduced in ES6, block scope is now available in JavaScript. Block scope is defined within a pair of curly brackets (e.g. ```{}```) and may be optionally labeled. Block scope can only be utilized with ```let``` and ```const``` as declaring variables in a block with ```var``` will not work as expected.

{% highlight js %}
var x = 10;
if (true) {
  var x = 5;
  console.log(x); //5
}
console.log(x);   //5
{% endhighlight %}

**Statements defined with ```var``` do not have block scope.**

To achieve block scope, we must use ```let``` or ```const```
{% highlight js %}
let x = 10;
if (true) {
  let x = 5;
  console.log(x); //5
}
console.log(x);   //10
{% endhighlight %}

with ```const```
{% highlight js %}
const a = 1;
if (true) {
  const a = 2;
  console.log(a); //2
}
console.log(a);   //1
{% endhighlight %}

The previous examples were labeled block statements, the same can be done with unlabeled statements as well
{% highlight js %}
let x = 10;
{
  let x = 5;
  console.log(x); //5
}
console.log(x);   //10
{% endhighlight %}

### Conclusion
Scope defines where a variable or function is "visible" (i.e. can it be seen/used in the code).  

Furthermore, there are three levels of scope in JavaScript: Global, Function, and Block.
- Global: accessible anywhere in the code
- Function: only accessible within that function
- Block: only accessible within the specified block

See the links below for additional resources and happy coding!

### Additional Resources
- [Mozilla](https://developer.mozilla.org/en-US/docs/Glossary/Scope) provides a great definition and for further details, definitely dive into the [Wikipedia entry on Scope](https://en.wikipedia.org/wiki/Scope_(computer_science)).
- A [quick introduction](https://robertnyman.com/2008/10/09/explaining-javascript-scope-and-closures/) that does a great job of laying out global and function scope.
-  For a deep dive, that [explains all you wanted to know about scope](https://toddmotto.com/everything-you-wanted-to-know-about-javascript-scope/), this is an excellent article. 
- Sitepoint provides a great look into [demystifying variable scope and hoisting](https://www.sitepoint.com/demystifying-javascript-variable-scope-hoisting/).
- [Block scope by Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/block)
