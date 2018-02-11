---
layout: single
title:  "Introduction to Javascript modules: import and export"
date:   2018-01-22 23:41:29 -0400
categories: javascript
---
JavaScript modules are now supported in most modern browsers. Let's start using them!

Browser support includes:
- Edge 16+
- Chrome 61+
- Safari 10.1+
- iOS Safari 10.3+
- Chrome for Android 62+

Be sure to check out [caniuse](https://caniuse.com/#search=export) for the latest.

Now let's code.

### Setup
We will not be using a module loader, bundler, or third party tool (e.g. no babel, webpack, rollup, etc.) as we are leveraging modern browsers. For this to work, we will need to use `type="module"` for our scripts.

_index.html_
{% highlight html %}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ES6 module demo</title>
</head>
<body>
<script type="module" src="main.js"></script>
</body>
</html>
{% endhighlight %}

Our folder structure will be
```
src
  |_ index.html
  |_ main.js
  |_ module.js
```
where `module.js` may be `add.js`, `mathUtils.js`, etc., based on the example.

### Export
Want to maximize code reuse? JavaScript modules help us achieve this goal.  The `export` statement allows us to write modules that can export objects, functions, or primitive values, which can then be utilized by other programs using the `import` statement.

There are two ways to export: default and named. Let's write a quick utility and then show how to utilize default and named exports.

_add.js_
{% highlight js %}
let add = (a,b) => a + b;
{% endhighlight %}

#### **Default export**
The default export will be exported by, yep you guessed it, default.  This means that it will be the base import used by another piece of code.  Let's see how that works.

_add.js_
{% highlight js %}
let add = (a,b) => a + b;
//export my function for later use (i.e. import)
export default add;
{% endhighlight %}

_main.js_
{% highlight js %}
import add from './add.js';
console.log(add(5,4));  //9
{% endhighlight %}

As the `add` function is the default export, even if we change the name of the identifier when importing, it will still map to the `add` function.
{% highlight js %}
//changing the identifier to show how it does not matter
import foo from './add.js';
console.log(foo(5,4));  //9
{% endhighlight %}

We can also export our function without giving it a name.  
{% highlight js %}
export default function(a,b) {
  return a + b;
};
{% endhighlight %}
We can still use it in our code the same way as before
{% highlight js %}
import add from './add.js';
console.log(add(5,4));  //9
{% endhighlight %}

#### **Named export**
Named export allows us to export several values. When using import, we must use the same name (i.e. identifier) for the corresponding item.  

_multiply.js_
{% highlight js %}
const multiply = (x,y) => x * y;
export {multiply};
{% endhighlight %}

_main.js_
{% highlight js %}
import {multiply} from './multiply.js';
console.log(multiply(10,10));  //100
{% endhighlight %}

Now, what happens if we try to change the name of our function when importing? Recall that when using default exports, we could change our local identifier and still obtain our default. What happens with named exports?  

_multiply.js_
{% highlight js %}
const multiply = (x,y) => x * y;
export {multiply};
{% endhighlight %}

_main.js_
{% highlight js %}
import foo from './multiply.js';
console.log(foo(10,10));  // SyntaxError: Importing binding name 'default' cannot be resolved by star export entries.
{% endhighlight %}

Doing this will cause an error.

**With named exports, we can import multiple items as once**  

_mathUtils.js_
{% highlight js %}
function add(x,y) {
  return x + y;
}

let multiply = (x,y) => x * y;

export {add, multiply};
{% endhighlight %}

_main.js_
{% highlight js %}
import {add, multiply} from './mathUtils.js';
console.log(add(5,4));  //9
console.log(multiply(10,10));  //100
{% endhighlight %}

### Import
The `import` statement allows us to import code which is exported by a module.  

For the following examples, we will utilize the module below.   

_mathUtils.js_
{% highlight js %}
function add(a,b) {
  return a + b;
}

function subtract(a,b) {
  return a - b;
}

function multiply(a,b) {
  return a * b;
}

function divide(a,b) {
  return a / b;
}

function logAnswer(answer) {
  console.log(answer);
}

export default logAnswer;
export {add,subtract,multiply,divide};
{% endhighlight %}


#### Import a single export from a module
{% highlight js %}
import {add} from './mathUtils.js';
console.log(add(5,4));  //9
{% endhighlight %}
This will insert `add` into the current scope.

#### Import multiple exports from a module
{% highlight js %}
import {add, subtract} from './mathUtils.js';
console.log(add(5,4));        //9
console.log(subtract(5,4));   //1
{% endhighlight %}

This will insert both `add` and `subtract` into the current scope.

#### Import all contents from a module
{% highlight js %}
import * as myMathUtils from './mathUtils.js';
console.log(myMathUtils.multiply(5,5));  //25
{% endhighlight %}

This will insert `myMathUtils` into the current scope and allow us to access all the exports from the module.  **Note**: to use the exports we must utilize dot notation (e.g. `myModule.doSomething()`);

#### Import default export
{% highlight js %}
import log from './mathUtils.js';
log('Hello Module'); //Hello Module
{% endhighlight %}

**A note on default import**  
Default exports do not require brackets (i.e. `{}`) when importing.
{% highlight js %}
import add from './add.js';
console.log(add(5,4));  //9
{% endhighlight %}

### Conclusion
JavaScript modules can help us achieve key programming best practices including code reuse, separation of concerns, encapsulation, and more. As modern browsers now support JavaScript modules through the addition of ```type="module"``` to our scripts, we can leverage `import` and `export` to build ES6 modules today.

### Additional Resources
- [Import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) and [Export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) by Mozilla.
- Modules in depth by [Mozilla](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/) and [Ponyfoo](https://ponyfoo.com/articles/es6-modules-in-depth#export)
- [A simple intro to JavaScript import and exports](https://medium.com/@thejasonfile/a-simple-intro-to-javascript-imports-and-exports-389dd53c3fac)
- Using [ES6 modules in modern browsers](https://www.contentful.com/blog/2017/04/04/es6-modules-support-lands-in-browsers-is-it-time-to-rethink-bundling/)
- And more information on using [modules in browsers today](https://jakearchibald.com/2017/es-modules-in-browsers/)
