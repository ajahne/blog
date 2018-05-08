---
layout: single
title:  "JavaScript Functions - Part 1"
date:   2017-10-09 20:56:29 -0400
categories: javascript
header:
  image: /assets/images/functions-part1.jpg
---
Functions are a fundamental element of JavaScript. This will be a multi-part series of posts focused on core concepts, with examples provided in both ES5 and ES6. This post outlines - at a high level - what a function is, its key features, and important takeaways. Let’s dive in!

### **What is a function?**
A function is a “subroutine” that can be invoked by code external or internal to it.  When a function is invoked internally (e.g. called within itself), it is called recursion. A function has a "function body", which is made up of one or more statements. Functions can have arguments (e.g. a passed in value) and also return a value.

So in short, functions are reusable bits of code that you can call (invoke) at some point in your program to execute a specific task.

### **Declaring (i.e. creating) a function.**
To create a function we "declare" it.  A function declaration is also called a function statement. This declaration also "defines" our function and is thus a function definition. Yup, three ways to say the same thing!
{% highlight js %}
function myFirstFunction() {
  //TODO: world changing code!
}
{% endhighlight %}

### **Invoking (i.e. calling) a function.**
Boom, simple, easy peasy...from our example above let's invoke!
{% highlight js %}
myFirstFunction();
{% endhighlight %}

Simply add "()" to the end of the function you declared and voila, invocation!

### **Functions are “first class” objects.**
This is a critical principle, that you will probably hear often and may scrunch up your face the first time you come across it. What exactly does this mean? Frankly, it means that functions can (and do) have properties and methods - just like any other object. A few methods that functions have include [_call_, _apply_]({{ site.baseurl }}{% post_url 2017-10-24-javascript-functions-part-2 %}), and [_bind_]({{ site.baseurl }}{% post_url 2017-10-31-javascript-functions-part-3 %}).  Additionally functions can have properties as well. Each function in JavaScript is a Function object.
{% highlight js %}
function echo(message) {
  console.log(message);
}

console.log(echo.name); //echo
{% endhighlight %}

### **Functions create new scope.**
{% highlight js %}
var foo = "bar";

function printFoo() {
  var foo = "baz";
  console.log(foo);
}

printFoo();       //baz
console.log(foo); //bar
{% endhighlight %}

### **Different ways to declare functions: declarations and expressions.**
So in our first example above - under declaring a function - we kinda/sorta didn't paint the entire picture.  There are different ways you can declare functions: function expressions and function declarations. In short, starting with the keyword “function” deems a declaration, all other examples are function expressions.  

Function declaration:
{% highlight js %}
function getName() {
  return 'name';
}
{% endhighlight %}
Function expression:
{% highlight js %}
var getName = function () {
  return 'name';
};
{% endhighlight %}

ES6 function expression (e.g. arrow function):
{% highlight js %}
let getName = () => 'name';
{% endhighlight %}

Function expressions can be named or anonymous, function declarations are named by default.

Anonymous function:
{% highlight js %}
var awesomeFunction = function() {
  //do something awesome
}
{% endhighlight %}
Named function expression:

{% highlight js %}
var myFunction = function myNamedFunction () {
  //do something amazing
}
{% endhighlight %}

### **Function declarations are hoisted.**  
Because of this, you can use a function before you have declared it.  However, do note that **function expressions are _not_ hoisted**

### **Functions can take parameters.**  
The parameters of a function are called arguments (see below for further details).
{% highlight js %}
function multiply (x, y) {
  return x * y;
}
{% endhighlight %}

### **Functions can access their 'arguments'.**
The 'arguments' property is an array-like object that contains all of the arguments passed into the function.
{% highlight js %}
function logArguments () {
  console.log(arguments);
}

logArguments(1,2,3) //[1,2,3]
{% endhighlight %}
Log the first argument:
{% highlight js %}
function logFirstArgument () {
  console.log(arguments[0]);
}

logFirstArgument(1,2,3) //1
{% endhighlight %}
Log the number of arguments:
{% highlight js %}
function logArgumentsLength () {
  console.log(arguments.length);
}

logArgumentsLength(1,2,3) //3
{% endhighlight %}

### **Functions can return values.**
Return values can be primitives, references, or other functions.
{% highlight js %}
function add (a, b) {
  return a + b;
}
{% endhighlight %}
ES6 example:
{% highlight js %}
let add = (a, b) => a + b;
{% endhighlight %}

### **Conclusion.**
We have learned the basics of functions, what they are, and how they operate at a high level. We have learned that they can take arguments and return values.  Additionally, functions create new scope.  We have learned the difference between a function declaration and a function expression, plus we have seen different examples in both ES5 and ES6. Next up, we dive even deeper. Feel free to try out some of your own examples and definitely check out the resources below.

### **Additional Resources**:
- General function reference:
  - [Function guide by Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
  - [Function reference by Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions)
- [Subroutine (function) definition via Wikipedia](https://en.wikipedia.org/wiki/Subroutine)
- Functions [as first class objects](https://appendto.com/2016/10/javascript-functions-as-first-class-objects/)
  - But wait, what is this [“first class object”](https://stackoverflow.com/questions/705173/what-is-meant-by-first-class-object) you speak of?
- [Function Expressions vs Function Declarations](https://www.sitepoint.com/function-expressions-vs-declarations/)
