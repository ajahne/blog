---
layout: single
title:  "Six ES6 methods to level up your Array game"
date:  2018-11-06 10:00:00 -0400
categories: javascript
tags: javascript
header:
  image: /assets/images/level-up-arrays.jpg
---
Time to level up our Array game!  With the advent of ES6, JavaScript `Arrays` have added new functionality that will enhance our code and streamline the way we have solve problems. In this post I will highlight six ES6 `Array` methods, outlining the ways we may have solved problems in the past and illustrating how we can use the new functions to do it (better) now.

Basically this post is a JavaScript `Array` version of **old and busted vs new hotness**.

<iframe width="560" height="315" src="https://www.youtube.com/embed/ha-uagjJQ9k" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>  <br/>

Let's get it.

## Table Of Contents
- [Array.of()](#arrayof)
- [Array.from()](#arrayfrom)
- [Array.prototype.find()](#arrayprototypefind)
- [Array.prototype.findIndex()](#arrayprototypefindIndex)
- [Array.prototype.fill()](#arrayprototypefill)
- [Array.prototype.includes()](#arrayprototypeincludes)
- [Bonus: Array.prototype.filter()](##bonus-arrayprototypefilter)

## `Array.of()`
The `Array.of()` method creates a new `Array` instance and can be used similarly to the constructor form of `Array()`.  However, `Array.of()` gets around the key `Array()` gotcha of passing in a number.  Let's create.  
{% highlight js %}
const a1 = new Array();
console.log(a1);  //[]
const a2 = Array.of();
console.log(a2);  //[]

//the gotcha...
const b1 = new Array(5);
console.log(b1);  //[undefined,undefined,undefined,undefined]
//the newness...
const b2 = Array.of(5);
console.log(b2);  //[5]

const c1 = new Array(1,2,3,4,5);
console.log(c1);  //[1, 2, 3, 4, 5]
const c2 = Array.of(1,2,3,4,5);
console.log(c2);  //[1, 2, 3, 4, 5]
{% endhighlight %}

There are a couple cases where this may be useful, but generally I still recommended **creating an array with using the array literal syntax** we have gotten accustom too:
{% highlight js %}
const a = [1,2,3,4,5];
{% endhighlight %}

## `Array.from()`
The `Array.from()` method creates a shallow copy of an `Array`.  We may have accomplished this in the past by creating a `shallowCopy()` function as outlined below.
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
{% endhighlight %}

However, we can simplify all of that now with one simple method, `Array.from()`:
{% highlight js %}
const arr = [1,2,3,4,5];
const a = Array.from(arr);
console.log(a);     //[ 1, 2, 3, 4, 5 ]
{% endhighlight %}

**A note about** `Array.from()`: This method copies the values, not the reference. So, the two arrays are not equal, as opposed to assigning an array to another variable, which ensures they point to the same location in memory, for example:
{% highlight js %}
const arr = [1,2,3,4,5];
const a = Array.from(arr);
const b = a;

console.log (a === arr);  //false
console.log (a === b);    //true
{% endhighlight %}

For more on value vs reference, check out [this post]({{ site.baseurl }}{% post_url 2018-1-29-javascript-value-vs-reference %})

## `Array.prototype.find()`
The `find()` method takes a "matching" function and returns the first value that is true or `undefined` if no value is found.

{% highlight js %}
const a = [5, 12, 8, 130, 44];

const found = a.find(function(element) {
  return element > 10;
});

console.log(found); // 12
{% endhighlight %}

Cool...so how might we use this to improve our JS Skills? Glad you asked, I got you.  This code is a modified example I pulled from a server validation script I wrote to check that our AWS infrastructure had been properly built via [Terrarform](https://www.terraform.io). Lot's of words, let's get to the code.
{% highlight js %}
const subnets = [
  {
    'name': 'subnet-a',
    'SubnetId': 1
  },
  {
    'name': 'subnet-b',
    'SubnetId': 2
  },
  {
    'name': 'subnet-c',
    'SubnetId': 3
  },
  {
    'name': 'subnet-d',
    'SubnetId': 4
  },
  {
    'name': 'subnet-e',
    'SubnetId': 5
  },  
];

//let's search the array of subnets to find a particular one given an ID
const getSubnetById = subnetId => {
  const numSubnets = subnets.length;
  for (let i=0; i < numSubnets; i++) {
    if (subnets[i]['SubnetId'] === subnetId) {
      return subnets[i];
    }
  }
}

console.log(getSubnetById(1));    //{ name: 'subnet-a', SubnetId: 1 }

//using the find method
const mySubnet = subnets.find(el => el['SubnetId'] === 1);
console.log(mySubnet);            //{ name: 'subnet-a', SubnetId: 1 }

//we could easily make this a reusable function
const findSubnetById = subnetId => subnets.find(el => el['SubnetId'] === subnetId);
console.log(findSubnetById(4));   //{ name: 'subnet-a', SubnetId: 4 }
{% endhighlight %}

As we can see from the Array method `find()` helped us reduce a lot of "boilerplate" code.  These are `for` loops we have all written a minimum of 27,841,991 times. Let's keep leveling up!

## `Array.prototype.findIndex()`
Say I wanted to find the index of the first value in an `Array` of numbers greater than 25, in ES5 (or earlier) I might've done something like this...
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

...but now ES6 is in the building! Enter `findIndex()`. This method takes a matching function and returns the index of the first element in the Array, which satisfies the condition.  
{% highlight js %}
const value = 25;
const indexWithNoWork = arr.findIndex(num => num > value);
console.log(indexWithNoWork); //2
{% endhighlight %}

## `Array.prototype.includes()`
What if we want to determine whether a value exists in an Array? We can use the `includes()` method to check if an element is included within an Array.
{% highlight js %}
var arr = [10,20,30,40,50];

//pre-ES6
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

//that ES6 wave
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

Please note that this method **will not change the length of the array**. So if you have an empty array, it will not add items:
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


## Bonus - `Array.prototype.filter()`
No post on leveling up can dared be written without the almighty `filter()`.  While not ES6 (originally introduced in ES5), this is a powerful method that can greatly improve code readability and efficiency. `filter()` takes a matching function and returns an array of all the elements that match the condition.

Let's return the list of elements greater than 25, showing both pre and post ES5 implementations.
{% highlight js %}
//pre-ES5
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

//ES5 now and forever
const newArray = arr.filter(num => num > value);
console.log(newArray);                //[ 30, 40, 50 ]
{% endhighlight %}

For a more in depth example, [check out this snippet](https://github.com/ajahne/js-examples/blob/master/arrays/array-filter-instances.js).

## Conclusion
The goal of this post is to show how by using these new functions we can simplify our programs, write less code that can reduce our cognitive load as we develop, and improve our utilization of Arrays.

## Additional Resources
- [Array.prototype.find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
- [Array API cheatsheet](https://gist.github.com/rauschma/f7b96b8b7274f2e2d8dab899803346c3)
- [Level up your .filter game from CSS-Tricks](https://css-tricks.com/level-up-your-filter-game/)
- [JavaScript Array Examples](https://github.com/ajahne/js-examples/tree/master/arrays)
- [A site showing whether an Array method mutates or not](https://doesitmutate.xyz)
