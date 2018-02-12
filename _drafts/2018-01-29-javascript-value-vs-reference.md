---
layout: single
title:  "Value vs Reference"
date:   2018-01-29 22:13:29 -0400
categories: javascript
---
This article will explore variables and types, both primitive and complex, with the goal of solidifying our understanding of values and references.

## Variables and Types
Javascript is loosely typed, which means that variables can store values
of any type. Any variable can be assigned and reassigned values of all types.

{% highlight js %}
let a = '5';        //a is a String
let a = 5;          //a is a Number
let a = {prop:5};   //a is an Object
let a = false;      //a is a Boolean
{% endhighlight %}

### What is the difference between a variable and a value?
A variable is a container for a value. Further, **_values have types, variables do not_**.
{% highlight js %}
let a = '5';
typeof 'a';   //'String'
typeof '5';   //'String'

let a = 5;
typeof a;     //'Number'
typeof 5;     //'Number'
{% endhighlight %}

The value `5` has an intrinsic (i.e. innate) type of `'Number'` and the value of `'5'` has an intrinsic type of `'String'`.  This cannot be changed. **_The assignment of the variable can be changed, but the value itself cannot_**.

**Note**: 'typeof' returns the type of the underlying value, which the variable is assigned to. See [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof) for further details.

So now that we have a better sense of variables and values, what are the different value types we can have?

## JavaScript Types:
**Primitive**
- String
- Number
- Boolean
- Null
- Undefined
- Symbol

**Complex**
- Object

What about `Arrays` and `Functions`? Well, those are both just Objects too!

## What is the difference between a value and a reference?
OK, now get to the core of it. As we have seen, there are two categories of types: primitives and complex (i.e. Object).

We cannot change the value of a primitive, but we can change the value of a reference.

### Examples
#### Primitives: when working with primitives, we work directly with the value
{% highlight js %}
let a = 'foo';
let b = a;

console.log(a);  //foo
console.log(b);  //foo

b = 'bar';
console.log(a);  //foo
console.log(b);  //bar
{% endhighlight %}

#### Reference (i.e. Object): when working with objects, we work on a reference to the value
{% highlight js %}
let a = {
  name: 'foo'
};
let b = a;
console.log(a.name);  //foo
console.log(b.name);  //foo

b.name = 'bar';
console.log(a.name);  //bar
console.log(b.name);  //bar
{% endhighlight %}

### Pass by value vs Pass by reference
You can either pass a specific value to a function (e.g. a primitive such as a `Boolean` or `Number`) or you can pass in a reference (e.g. an `Object`).

### Passing values
Changing a value passed into a function, will not change the value of the original variable.
{% highlight js %}
let a = 10;

let increment = num => {
  num++;
  return num;
}
let b = increment(a);
console.log(a); //10;
console.log(b); //11;
{% endhighlight %}


### Passing references
Passing in and changing the value of a complex type (i.e. Object) will modify all variables that point to that value.
{% highlight js %}
let a = {
  value: 10
};

let increment = o => {
  o.value++;
  return o;
}
let b = increment(a);
console.log(a.value); //11;
console.log(b.value); //11;
{% endhighlight %}

Going further, this can sometimes have unexpected consequences if we want to copy an object.
{% highlight js %}
let a = {
  value: 10
};

let simpleCopy = o => {
  let temp = o;
  return temp;
};
let b = simpleCopy(a);
b.value = "25";
console.log(a.value); //25;
console.log(b.value); //25;
{% endhighlight %}
As we see, copying a reference did not give us a unique object. Instead object `a` and object `b` point to the same place in memory.  To obtain a unique copy of an object, we would have to copy out each property individually.  

**Note**: this can get very complicated with nested objects, so to avoid deep recursion, we often perform a "shallow copy" and copy the first level of an object.
{% highlight js %}
let a = {
  value: 10
};

let shallowCopy = o => {
  let temp = {};
  for (let key in o) {
    if (o.hasOwnProperty(key)) {
      temp[key] = o[key];
    }
  }
  return temp;
}
let b = shallowCopy(a);
b.value = "25";
console.log(a.value); //10;
console.log(b.value); //25;
{% endhighlight %}

## Conclusion
- JavasScript has seven data types: 6 primitive types and 1 complex type
  - `Arrays` and `Functions` of type `Object`, and therefore are treated as references
- Values have types, variables do not
- When accessing a primitive type, we work directly with the value
- When accessing an object (i.e. complex type), we work on a reference to the value
- When passing values into functions, Objects are being passed by reference, while primitives are passed in by copying the value.

## **Additional Resources**:
- [JavaScript data types and data structures by Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures)
- [You Don't Know JS: Types and Grammar](https://github.com/getify/You-Dont-Know-JS/tree/master/types%20%26%20grammar)
- [Value vs Reference by Educative](https://www.educative.io/collection/page/5679346740101120/5707702298738688/5685265389584384)
