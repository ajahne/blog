## Functions Part 1: Introduction
Functions are a fundamental element of JavaScript.  This will be a series of posts that will focus on core concepts. The examples will be provided in both ES5 and ES6. Arrow functions, generator functions, and ES6 specific syntax and features will be detailed in a separate post. This post outlines - at a high level - what a function is, its key features, and important takeaways. Let's dive in!

### What is a function?
A function is a “subroutine” that can be invoked by code external or internal to it.  When a function is invoked internally (e.g. called within itself), it is called recursion. A function has a "function body", which is made up of one ore more statements.. Functions can have arguments (e.g. passed in a value) and also return a value. 

So in short, functions are reuable bits of code that you can call (invoke) at some point in your program to execute a specific task. 

### Declaring a function
A function declaration is also called a function statement. This declaration also, "defines" our function and is thus a function definition. Yup, three ways to say the same thing! 
```
function myFirstFunction() {
  //space for world changing code!
}
```

### Invoking (calling) a function
Boom, simple, easy peasy...from our example above
```
myFirstFunction();
```
Simply add "()" to the end of the function your declared and voila, invokation!

### Functions are “first class” objects.
This is a critical principle, that you will probably hear often and may scrunch up your face the first time you come across it. What exactly does this mean? Frankly, it means that functions can (and do) have properties and methods - just like any other object. A few methods that functions have include call, apply, and bind.  Additionally functions can have properties as well. Each function in JavaScuprt is a Function object. 
```
function echo(message) {
  console.log(message);
}
console.log(echo.name); //echo
```

### Functions create new scope.
```
var foo = "bar";

function printFoo() {
  var foo = "baz";
  console.log(foo);
}
printFoo();       //baz
console.log(foo); //bar
```

### There are different ways to declare functions: declarations vs expressions.
So in our first example above - under declaring a function - we kinda/sorta didin't paint the entire picture.  There are different ways you can declare functions: function expressions and function declarations. In short, starting with the keyword “function” deems a declaration, all other examples are function expressions.  
Function declaration:
``` 
function getName() {
  return 'name';
}
```
Function expression:
``` 
var getName = function () {
  return 'name';
};
```

ES6 function expression (e.g. arrow function)
```
let getName = () => 'name';
```

Function expressions can be named or anonymous, function declarations are named by default. 

Anonymous function 
```
var awesomeFunction = function() {
  //do something awesome
}
```
Named function expression

```
var awesomeFunction = function awesomeFunctionName () {
  //do something awesome
}
```

### Functions are hoisted.  
Because of this, you can use a function before you have declared it.  However, do note that function expressions are not hoisted

### Functions can take parameters.  
The parameters of a function are called arguments (see below for further details). 
``` 
function add (a,b) {
  return a+b;
}
```

### Functions can access their 'arguments'.
The 'arguments' is an array-like object that contains all of the arguments passed into the function. 
```
function logArguments () {
  console.log(arguments);
}

logArguments(1,2,3) //[1,2,3]
```
Log the first argument:
```
function logFirstArgument () {
  console.log(arguments[0]);
}

logFirstArgument(1,2,3) //1
```
Log number of arguments:
```
function logArgumentsLength () {
  console.log(arguments.length);
}

logFirstArgument(1,2,3) //3
```

### Functions can returns values.
Return values can be primitives, references, or other functions
```
function add (a,b) { 
  return a + b;
}
```
ES6
```
let add = (a,b) => a+b;
```

### Conclusion.
We have learned the basics of functions, what they are, and how the operate at a high level. We have learned that they can take arguments and return values, while also creating new scope.  We have learned the difference between a function declaration and a function expression, plus we have seen different examples in both ES5 and ES6. Next up, we dive even deeper. Feel free to try out some of your own examples and definitely check out the resources below. 

### Additional Resources:
- General function reference:
  - Function guide by Mozilla
  - Function reference by Mozilla
- Subroutine (function) definition via Wikipedia
- Functions as first class objects
  - But wait, what is this “first class object” you speak of? 
- Function Expressions vs Function Declarations
