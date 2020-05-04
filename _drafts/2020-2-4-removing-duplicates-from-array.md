---
layout: single
title:  'How to Remove Duplicates from an Array in JavaScript'
date:   2020-2-4 12:19:00 -0500
categories: javascript
tags: javascript, js, array
header:
  image: /assets/images/remove-duplicates-header.jpg
---
As I prepare to interview for a wide array (_pun intended_) of engineering leadership and management positions, I have extensively practiced numerous programming problems and system design questions. A standard interview question is the classic "remove duplicates from an array" problem. This may be asked in a phone screen, online, or during an on-site. While many tech companies may _not_ ask this specific question, it is a great practice interview problem that can help grow [our time complexity understanding](https://www.interviewcake.com/article/java/big-o-notation-time-and-space-complexity) and further enhance our programming proficiency.

## Table of Contents
- The Remove Duplicates Problem
  - Standard ways to remove duplicates
    - Brute force solution - O(n<sup>2</sup>)
    - Solution with hash-map - O(n)
  - Removing duplicates with ES6
    - Using a `Set`
    - Using `filter()`
    - Using `filter()` and `indexOf()`
- Conclusion
- Additional Resources

## TL;DR
Remove duplicates with a Set (ES6)
```javascript
const unique = [...Set([1,1,2,2,5,5,3])]; //[1,2,5,3]
```

Remove duplicates with a hash-map (no ES6)
```javascript
function removeDuplicates(array) {
  const result = [];
  const map = {};

  for (let i = 0; i < array.length; i++) {
    if (map[array[i]]) {
      continue;
    } else {
      result.push(array[i]);
      map[array[i]] = true;
    }
  }
  return result;
}
```

Now that you see where we are heading, how did we get there? Let's start with the problem statement and pushed forward!

## The Removing Duplicates Problem
From the book [Programming Interviews Exposed](https://www.amazon.com/Programming-Interviews-Exposed-Secrets-Landing/dp/1118261364):

>  Given an unsorted list of integers, write a function that returns a new list with all duplicate values removed.

So how might we approach this problem?

## Brute Force
One solution is to have two arrays. One for our input and one for our output. The basic algorithm consists of looping through the original `array` (i.e. list) and for every element in the array, check to see if it exists in our `result` array. If the element exists in `result` skip to the next element, if not, add it to the `result` array. Once complete, return `result`.  
```javascript
function removeDuplicates(array) {
  const result = [];
  for (let i = 0; i < array.length; i++) {
    let exists = false;
    for (j = 0; j < result.length; j++) {
      if (array[i] === result[j]) {
        exists = true;
        break;
      }
    }
    if (!exists) {
      result.push(array[i]);
    }
  }
  return result;
}
```

Running the code is straightforward.
```javascript
const duplicates = [5,2,3,2,5,5,1,7,2,1,5,8];
removeDuplicates(duplicates); //[ 5, 2, 3, 1, 7, 8 ]
```

This is a [brute force](https://www.quora.com/What-is-brute-force-in-programming) solution with a O(n<sup>2</sup>) time complexity. This algorithm's time complexity stems from the fact that we are looping through two arrays. Can we get to this to linear time, i.e. O(n)? Yes we can, by using a hash-map!

## Remove Duplicates using a hash-map
In our brute force solution, we loop through the array twice, what if we were to loop through just once? We can do this if we use an object to keep track of key value pairs, i.e. our "hash-map". The "key" is the element in the array, and the value is true or falsy. This map keeps track of whether we have previously added the current element to our `result` array or not.
```javascript
function removeDuplicates(array) {
  const result = [];
  const map = {};

  //loop through array
  //if the element has been seen, continue to next element.
  //if that element has not been seen,
  //add it to the result array.
  for (let i = 0; i < array.length; i++) {
    if (map[array[i]]) {
      continue;
    } else {
      result.push(array[i]);
      map[array[i]] = true;
    }
  }
  return result;
}
```

Again we can run this code to see the results
```javascript
const a = [1,1,2,3,3,4,4,5,5];
const b = [2,3,3,1,2,7,5,5,4,9,4,14];
const c = [5,2,3,2,5,5,1,7,2,1,5,8];

removeDuplicates(a) //[1,2,3,4,5]
removeDuplicates(b) //[2,3,1,7,5,4,9,14]
removeDuplicates(c) //[5,2,3,1,7,8]
```

The general idea of this solution is to maintain a mapping of our elements to a boolean value of whether the element has been added to our `result` array or not. Stated differently, the boolean represents either yes we have added this element to the `result` (`true`) or no we have not (`false`).

The chart below illustrates the state of variables, in the simple case of an array `[1,1,2]`.

|index | array[index] | map[index] | result
0 | 1 | undefined | [1]
1 | 1 | true | [1]
2 | 2 | undefined | [1,2]


## What about using ES6?

_OK, Ajahne, this is cool and all, but can we leverage ES6?_

Definitely, please note, that some interviewers may [veto built-in methods or utilizing certain objects](https://leetcode.com/discuss/interview-question/168757/Google%3A-Remove-Duplicates-from-Unsorted-Array).

_Oh, really?_

Yeah, they may do this to get a better sense of how you approach a problem. In that case, it is still worth mentioning that "I would use a set in this way..." or "I could leverage filter like so...". Showing your knowledge of the language will definitely get you some brownie points!

_Got it. But I'm still waiting..._

Bet, [let me upgrade you](https://www.youtube.com/watch?v=6nr8hPnZfMU)!

## Removing duplicates using a `Set`
My preferred method of removing duplicates from an array is to use a `Set`. By definition, a set can only contain unique values, so it is the perfect data structure to solve this problem.
```javascript
const array = [1,1,2,3,3,4,4,5,5];
const set = new Set(a);
const uniqueArray = [...set];
console.log(uniqueArray);
```
What we do in the above code is create an Array, make a new Set using our array as an initial parameter to the Set's constructor, and then use the spread operator to transform our set into an Array.

Furthermore, you can one line this solution.
```javascript
const unique = [...new Set(array)];
console.log(unique)
```

Cool, so how else might we do this?

## Remove duplicates using `Array.filter()`
We can upgrade our original "optimized" solution, replacing our `for` loop, with `filter`. The filter function takes a callback and returns a new array comprised only of elements that pass our test.
```javascript
function dedup_filter_inline(a) {
  const map = {};
  return a.filter(element => {
    if (map[element]) {
      return false
    } else {
      map[element] = true;
      return true;
    }
  });
}

const a = [1,1,2,3,3,4,4,5,5];
const b = [2,3,3,1,2,7,5,5,4,9,4,14];
const c = [5,2,3,2,5,5,1,7,2,1,5,8];

console.log();
console.log(dedup_filter_inline(a)) //[1,2,3,4,5]
console.log(dedup_filter_inline(b)) //[2,3,1,7,5,4,9,14]
console.log(dedup_filter_inline(c)) //[5,2,3,1,7,8]
```

### Remove duplicates using `Array.filter()` and `Array.indexOf()`
Building on the previous example, we can leverage `indexOf` in our callback to filter out elements that appear more than once.

```javascript
function dedupWithFilterAndIndexOf(a) {
  return a.filter((element, index) => a.indexOf(element) === index);
}

const a = [1,1,2,3,3,4,4,5,5];
const b = [2,3,3,1,2,7,5,5,4,9,4,14];
const c = [5,2,3,2,5,5,1,7,2,1,5,8];

console.log(dedupWithFilterAndIndexOf(a)) //[1,2,3,4,5]
console.log(dedupWithFilterAndIndexOf(b)) //[2,3,1,7,5,4,9,14]
console.log(dedupWithFilterAndIndexOf(c)) //[5,2,3,1,7,8]
```

For each element in the array, we check to see if it's index matches the current index. This works because `indexOf` returns the _first_ index at which a given element can be found and -1 if it does not exist. So, if we have an array with duplicate elements, the indeces of each will be different, but call to indexOf will return the first index. So in our check of ` a.indexOf(element) === index` if these indeces are different, then this element is _not_ the first element with this value and should not be added to our resulting array.

Let's look at the scenario when we have an array `[1,2,2]`

|index | element | indexOf(element) | result | note
0 | 1 | 0 | [1] | the element's index and the first index of this element match, so we add it to the result
1 | 1 | 0 | [1] | when we look up 1, its first index (indexOf) is 0, so we know this is a duplicate, and skip it
2 | 2 | 2 | [1,2] | the element's index and the first index of this element match, so we add it to the result

## Conclusion
There are numerous ways to remove duplicate from an Array and as we prepare for programming interviews! What other ways have you found to remove duplicates? Solving programming problems in preparation for my interview loops has been invaluable. It is worth learning these different techniques, widening our understanding of JavaScript, and leveraging our Big O understanding to build optimized solutions that will help us not only in our interviews, but on the job and beyond!

There are numerous ways to remove duplicates from an Array and as we prepare for programming interviews! What other ways have you found to remove duplicates? Solving programming problems in preparation for my interview loops has been invaluable. It is worth learning these different techniques to widen our JavaScript skillset and leverage our Big O understanding to build optimized solutions that will help us not only in our interviews, but on the next job and beyond!

Check out the additional resources below and happy coding!

## Additional Resources
- [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)
- [Array.prototype.indexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)
- [Array.prototype.filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- [Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
- [Programming Interviews Exposed](https://www.amazon.com/Programming-Interviews-Exposed-Secrets-Landing/dp/1118261364)
- [Leetcode: Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
- [Big O notation](https://www.interviewcake.com/article/java/big-o-notation-time-and-space-complexity)
