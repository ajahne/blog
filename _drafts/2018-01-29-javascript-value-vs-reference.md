---
layout: post
title:  "Value vs Reference"
date:   2018-01-29 22:13:29 -0400
categories: jekyll javascript value reference
---

### Introduction

### What is the difference between a value and reference:
A value is a specific representation of a primitive while a reference points to a location in memory.  Multiple references can point to the same location in memory, therefore by changing the value at that location, the value of the reference will change as well.  

JavaScript contains different types of variables, primitives and references.

A reference points to a location in memory that contains a value.

### Primitive Values
Immutable (i.e. unchangeable) variable types:
- String
- Number
- Boolean
- Null
- Undefined

### Reference Values
Mutable (i.e. changeable) variable types:
- Object

### Examples
{% highlight js %}
let oldName = 'foo';
let copyName = (name) => {
  let copy = name;
  return copy;
}

let newName = copyName(oldName);

console.log(oldName);  //foo
console.log(newName);  //foo

oldName = 'bar';
console.log(oldName);  //bar
console.log(newName);  //foo
{% endhighlight %}

{% highlight js %}
let a = {
  name: 'a'
};
let copyObject = (objectToCopy) => {
  let temp = objectToCopy;
  return temp;
};
let b = copyObject(a);
b.name = 'b';
console.log(a.name);  //b
console.log(b.name);  //b

a.name = 'Vega';
console.log(a.name);  //Vega
console.log(b.name);  //Vega
{% endhighlight %}
