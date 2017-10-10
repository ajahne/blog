## Functions Part 1:
Functions are a key element of JavaScript.  This will be a series of posts that will focus on core concepts. The examples will be provided in both ES5 and ES6. Arrow functions and ES6 specific syntax and features will be detailed in a separate post. This post outlines, what a function is, it's key features, and important takeaways. Let's dive in!

## What is a function?
A sequence of statements that performs a specific task(s). A function is “subroutine” that can be called (invoked) by code external or internal to it.  When a function is invoked internally (e.g. called within itself), it is called recursion. 

### Functions are “first class” objects:
THis is a critical principle, that you will probably hear often and may scrunch up your face the first time you comeo across it. What exactly does this mean? Frankly, it means that functions can (and do) have properties and methods - just like any other object. A few methods that functions have include call, apply, and bind.  Additionally functions can have properties as well
```
function echo(message) {
  console.log(message);
}
console.log(echo.name); //echo
```

### Functions create new scope
```
var foo = "bar";

function printFoo() {
  var foo = "baz";
  console.log(foo);
}
printFoo();       //baz
console.log(foo); //bar
```

### Function declarations vs Function expressions:
There are function expressions and function declarations. In short, starting with the keyword “function” deems a declaration, all other examples are function expressions.  
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

### Functions are hoisted.  
Because of this, you can use a function before you have declared it.  However, do note that function expressions are not hoisted

### Functions can take parameters  
``` 
function add (a,b) {
  return a+b;
}
```

### Functions can access their 'arguments'.
'arguments' is an array-like object that contains all of the arguments passed into the function 
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

### Functions can returns values
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

### Additional Resources:
- General function reference:
  - Function guide by Mozilla
  - Function reference by Mozilla
- Subroutine (function) definition via Wikipedia
- Functions as first class objects
  - But wait, what is this “first class object” you speak of? 
- Function Expressions vs Function Declarations
