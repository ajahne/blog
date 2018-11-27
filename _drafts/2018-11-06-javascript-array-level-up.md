---
layout: single
title:  "Leveling up our JavaScript Array game"
date:  2018-11-06 10:00:00 -0400
categories: javascript
tags: javascript
header:
  image: /assets/images/level-up-arrays.jpg
---
Time to level up our Array game!  With the advent of ES6, JavaScript Arrays have added new functionality that will enhance and help simplify the way we have previously done things. For each highlighted function I will outline the ways we may have solved problems in the past and how we can use the new functions to do it now.

Basically this post is a JavaScript Array version of **old and busted vs new hotness**.

<iframe width="560" height="315" src="https://www.youtube.com/embed/ha-uagjJQ9k" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>  <br/>

The goal of this post is to show how by using these new functions we can simplify our programs, write less code that can reduce our cognitive load as we develop, and improve our utilization of Arrays. Let's get it.

## TOC/TL;DR
- `Array.of()`
- `Array.from()`
- `Array.prototype.find()`
- `Array.prototype.findIndex()`
- `Array.prototype.filter()`
- `Array.prototype.fill()`
- `Array.prototype.includes()`
- `Array.prototype.copyWithin()`

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

A note about `Array.from()`: it performs a shallow copy, copying the values, not the reference. So, the two arrays are not equal, as opposed to assigning an array to another variable, which ensures they point to the same reference, for example:
{% highlight js %}
const arr = [1,2,3,4,5];
const a = Array.from(arr);
const b = a;

console.log (a === arr);  //false
console.log (a === b);    //true
{% endhighlight %}

## `Array.prototype.find()`
The `find()` method takes a "matching" function and returns the first value that is true or `undefined` if no value is found.

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

## `Array.prototype.includes()`
{% highlight js %}
var arr = [10,20,30,40,50];
var value

function existsInArray(array, value) {
  //before would use index of
  for (var i = 0; i < array.length; i++) {
    if (array.indexOf(value) !== -1) {
      return true;
    }
  }
  return false;
}

console.log(existsInArray(arr, 40));      //true
console.log(existsInArray(arr, 4));       //false
console.log(existsInArray(arr, 'hello')); //false

console.log(arr.includes(40));            //true
console.log(arr.includes(4));             //false
console.log(arr.includes('hello'));       //false
{% endhighlight %}

## `Array.prototype.fill()`
The `fill()` method fills all (or part) of an array.
{% highlight js %}
const d = Array(5).fill(0);
console.log(d);             //[0,0,0,0,0]
const e = Array(5);
console.log(e);             //[undefined,undefined,undefined,undefined,undefined];
{% endhighlight %}

Please note that it will not change the length of the array. So if you have an empty array, it will not add items
{% highlight js %}
const a = [];//Array.of();
console.log(a);             //[]
const b = a.fill(0, 1, 3);
console.log(a);             //[]
console.log(b);             //[]

const c = [1,2,3];
console.log(c.fill(0, 1));  //[1,0,0]
{% endhighlight %}

How might we use this function?  Well, let's envision the following scenario: What if you have a game board represented by an array and you wanted to (re)initialize each value in the array to -1 (basically "reset") the game?

{% highlight js %}
var board = [];
var length = 5;
var initialValue = -1;

//Previously, we may have written a function like the following to set an initial
//value for every element in our array
function initializeBoard(board, length, initialValue) {
  for (var i = 0; i < length; i++) {
    board[i] = initialValue;
  }
}

initializeBoard(board, length, initialValue);
console.log(board);         //[ -1, -1, -1, -1, -1 ]

//new way of doing it
const newBoard = [];
newBoard.length = length;
newBoard.fill(-1);
console.log(newBoard);      //[ -1, -1, -1, -1, -1 ]

//or better yet...
const newBoard2 = Array(length).fill(-1);
console.log(newBoard2);     //[ -1, -1, -1, -1, -1 ]
{% endhighlight %}

## `Array.prototype.copyWithin()`
{% highlight js %}
const arr = [10,20,30,40,50];
const foo = arr.copyWithin(1, 0);
console.log(arr);   //[ 10, 10, 20, 30, 40 ]
console.log(foo);   //[ 10, 10, 20, 30, 40 ]
{% endhighlight %}

## Additional Resources
- [Array.prototype.find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
- [Array API cheatsheet](https://gist.github.com/rauschma/f7b96b8b7274f2e2d8dab899803346c3)
- [Level up your .filter game from CSS-Tricks](https://css-tricks.com/level-up-your-filter-game/)
