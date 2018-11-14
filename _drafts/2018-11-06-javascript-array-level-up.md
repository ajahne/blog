---
layout: single
title:  "Leveling up our JavaScript Array methods"
date:  2018-11-06 10:00:00 -0400
categories: javascript
tags: javascript
header:
---

## Outline
- How I used to do  it
- How I am doing it now/want to do it

`Array.prototype.find()`
The `find()` method takes a "matching" function and returns the first value that is true or undefined if no value is found.

{% highlight js %}
const array1 = [5, 12, 8, 130, 44];

const found = array1.find(function(element) {
  return element > 10;
});

console.log(found); // 12
{% endhighlight %}


`Array.of()`
Replaces the constructor form of `Array()` and gets around the key `Array()` gotcha of passing in a number.
{% highlight js %}
const a1 = new Array();
const a2 = Array.of();
console.log(a1);  //[]
console.log(a2);  //[]

const b1 = new Array(5);
const b2 = Array.of(5);
console.log(b1);  //[undefined,undefined,undefined,undefined]
console.log(b2);  //[5]

const c1 = new Array(1,2,3,4,5);
const c2 = Array.of(1,2,3,4,5);
console.log(c1);  //[1, 2, 3, 4, 5]
console.log(c2);  //[1, 2, 3, 4, 5]

{% endhighlight %}

There are a couple cases where this may be useful, but most instances I still recommended creating an array with using the array literal syntax we have gotten accustom too:
{% highlight js %}
const a = [1,2,3,4,5];
{% endhighlight %}


`Array.from()`

`Array.prototype.findIndex()`
`Array.prototype.filter()`

`Array.prototype.fill()`

`Array.prototype.findIndex()`

`Array.prototype.includes()`

`Array.prototype.includes()`

`Array.prototype.copyWithin()`

## Additional Resources
- [Array.prototype.find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
