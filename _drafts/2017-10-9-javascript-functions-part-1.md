## Definition: What is a function
A sequence of statements that performs a specific task(s). A function is “subroutine” that can be called (invoked) by code external or internal to it.  

### Key Takeaways:
- Functions are “first class” objects:
  - Functions can (and do) have properties and methods
- Functions create new scope

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

ES6 Example:
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
