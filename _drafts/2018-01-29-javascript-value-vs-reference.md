---
layout: post
title:  "Value vs Reference"
date:   2018-01-29 22:13:29 -0400
categories: jekyll javascript value reference
---

### Introduction

### What is the difference between a value and reference:
A value is a specific representation of information while a reference points to a location in memory.  Multiple references can point to the same location in memory, therefore by changing the value at that location, the value of the reference will change as well.  

JavaScript contains different types of variables, primitives and references.

A reference points to a location in memory that contains a value.

### Primitive Values
- String
- Number
- Boolean
- Null
- Undefined
- Symbol

### Reference Values
- Object

### Examples
{% highlight js %}
let a = 'foo';
let b = a;

console.log(a);  //foo
console.log(b);  //foo

b = 'bar';
console.log(a);  //foo
console.log(b);  //bar
{% endhighlight %}

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
You can either pass a specific value to a function (i.e. a primititve such as a `Boolean` or `Number`) or you can pass in a reference (e.g. an `Object`).

#### Passing values
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


#### Passing references
Passing in and changing a reference will change all variables that point to that value.
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
As we see, copying a reference did not give us a unique object. Instead but object `a` and object `b` point to the same place in memory.  To obtain a unique copy of an object, we would have to copy out each property individually.  **Note**: this can get very complicated with nested object, so to avoid deep recursion, we often perform a "shallow copy" and copy the first level of an object.
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
