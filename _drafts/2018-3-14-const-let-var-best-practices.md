---
layout: single
title:  "CONST, LET, and VAR Best Practices"
date:   2018-3-14 10:10:29 -0400
categories: javascript
---
So when should you use `const`, `let` or `var`?

## Summary:
- Use `const` by default  
- Use `let` if you need to reassign a variable  
- Never use `var`

## Overview
A variable should represent one thing

Use const by default
Const cannot be reassigned, but are still mutable when dealing with complex types (add link)

Const is not a value that doesn't change, but rather it is an identifier that does not get reassigned.

True immutability can be obtained through using const with primitive types.

Change const to let once you see the value contained by the variable needs to change

Why? This will help you clearly denote which variables should change and which should not.  This helps general readability as other developers will have a clearer sense of what variables change throughout program execution and which do not.

So when use let?
When the value of the identifier needs to change.  Some examples
For loops (i)
Counters (keeping track of current number of DOM child elements)
Mathematical formulas
Form data (i.e. text input value while user is typing)
Flip a boolean flag/toggle

Never use var.  

Why?
Using var has side effects, point to hoisting link.  
Var does not support block scope.  
Example

Benefits of using const and let
Lexical scope
Block scope
No hoisting

Naming conventions
In general, variables are nouns and noun phrases
For example
See Google for more examples

When using const, follow these practices
For immutable values and values that you explicitly do not want to change use constant case

Show examples of const case with var as well.

Point to links that show constant case is a general programming convention understood across different programming languages

For mutable values (e.g. objects) use camel case

## Additional resources
- Eric Elliot: https://medium.com/javascript-scene/javascript-es6-var-let-or-const-ba58b8dcde75
- Zakas: ES6
- The Dr guy
- Ponyfoo: https://ponyfoo.com/articles/var-let-const
- Reddit:
