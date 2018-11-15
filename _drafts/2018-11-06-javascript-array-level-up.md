---
layout: single
title:  "Leveling up our JavaScript Array methods"
date:  2018-11-06 10:00:00 -0400
categories: javascript
tags: javascript
header:
  image: /assets/images/level-up-arrays.jpg
---

## Outline
- How I used to do  it
- How I am doing it now/want to do it

## `Array.of()`
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


## `Array.from()`
{% highlight js %}
function shallowCopy (a) {
  var temp = [];
  a.forEach(function(value){
    temp.push(value);
  });
  return temp;
};

const arr = [1,2,3,4,5];
const temp = shallowCopy(arr);
console.log(temp);  //[ 1, 2, 3, 4, 5 ]

//let's simplify all of that!
const a = Array.from(arr);
console.log(a);     //[ 1, 2, 3, 4, 5 ]
{% endhighlight %}

A note about `Array.of()`: it performs a shallow copy, copying the values, not the reference. So, the two arrays are not equal, as opposed to assigning an array to another variable, which ensures they point to the same reference, for example
{% highlight js %}
const arr = [1,2,3,4,5];
const a = Array.from(arr);
const b = a;

console.log (a === arr);  //false
console.log (a === b);    //true
{% endhighlight %}

## `Array.prototype.find()`
The `find()` method takes a "matching" function and returns the first value that is true or undefined if no value is found.

{% highlight js %}
const array1 = [5, 12, 8, 130, 44];

const found = array1.find(function(element) {
  return element > 10;
});

console.log(found); // 12
{% endhighlight %}


## `Array.prototype.findIndex()`
Say I wanted to find the index of the first value > 25, in ES5 (or lower) I might create something like this...
{% highlight js %}
var arr = [10,20,30,40,50];
var value = 25;
var index;

function getIndex(array, value) {
  for (var i = 0; i < array.length; i++) {
    if (array[i] > value) {
      return i;
    }
  }
}

index = getIndex(arr, value);
console.log(index);           //2
{% endhighlight %}

...but now ES6 in the building! Simplifying all of our code.
{% highlight js %}
const indexWithNoWork = arr.findIndex(num => num > value);
console.log(indexWithNoWork); //2
{% endhighlight %}


## `Array.prototype.filter()`
{% highlight js %}
var arr = [10,20,30,40,50];
var value = 25;
var filteredArray;

function filter(array, value) {
  var temp = [];
  for (var i = 0; i < array.length; i++) {
    if (array[i] > value) {
      temp.push(array[i]);
    }
  }
  return temp;
}

filteredArray = filter(arr, value);
console.log(filteredArray);           //[ 30, 40, 50 ]

const newArray = arr.filter(num => num > value);
console.log(newArray);                //[ 30, 40, 50 ]
{% endhighlight %}

## `Array.prototype.fill()`

## `Array.prototype.includes()`

## `Array.prototype.copyWithin()`

## Additional Resources
- [Array.prototype.find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
