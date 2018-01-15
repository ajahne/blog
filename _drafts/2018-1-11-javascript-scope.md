---
layout: post
title:  "JavaScript Scope"
date:   2018-01-11 20:56:29 -0400
categories: jekyll javascript scope
---

### Introduction

**Some best practices:**
- Best Practice in JavaScript programming is to reduce polluting the global scope.  The reason is that multiple scripts may be utilized in an application and naming conflicts can cause unexpected behavior.
- Reducing global scope can be achieved through modules and namespaces – topics for further discussion. In short, both of these reduce the pollution of global scope by placing variables and functions under one “umbrella” variable name or function. 

### Definition:
Scope defines where a variable or function is accessible. It is the current context of execution within the program. Scopes are hierarchical, where child scope can access parent scopes, but not vice versa.

### Global Scope  
By default all variables and functions defined in JavaScript are global – accessible from anywhere in our code or any other code that is being utilized in conjunction with ours.

{% highlight js %}
let greeting = 'Hello Global';
{% endhighlight %}

As defined at the top of our program, this variable ```greeting``` is visible everywhere in our code.

{% highlight js %}
let greeting = 'Hello Global';
let greet = () => {
  console.log(greeting);
}
greet(); //Hello Global
{% endhighlight %}


### Function scope
Functions can also define scope, new areas where code is "visible". Building off our previous example:

{% highlight js %}
let greeting = 'Hello Global';
let greet = () => {
  console.log(greeting);
}
let greetLocal = () => {
  let greeting = 'Hello Local';
  console.log(greeting);
}
greet();      //Hello Global
greetLocal(); //Hello Local
{% endhighlight %}

### Block scope
Introduced in ES6, block scope is now available in JavaScript. Block scope is defined within a pair of curly brackets (e.g. ```{}```) and may be optionally labeled.


### Conclusion
- There are three levels of scope in JavaScript: Global, Function(local), and block
  - Global: accessible anywhere in the code
  - Function: only accessible within that function
  - Block: only accessible within the specified block

### Additional Resources
- [Mozilla](https://developer.mozilla.org/en-US/docs/Glossary/Scope) provides a great definition and for further details, definitely dive into the [Wikipedia entry on Scope](https://en.wikipedia.org/wiki/Scope_(computer_science)).
- A [quick introduction](https://robertnyman.com/2008/10/09/explaining-javascript-scope-and-closures/) that does a great job of laying out the two levels of scope.
-  For a deep dive, that [explains all you wanted to know about scope](https://toddmotto.com/everything-you-wanted-to-know-about-javascript-scope/), this is an excellent article. 
- Sitepoint provides a great look into [demystifying variable scope and hoisting](https://www.sitepoint.com/demystifying-javascript-variable-scope-hoisting/).
