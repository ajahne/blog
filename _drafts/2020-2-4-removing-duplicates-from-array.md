---
layout: single
title:  'Removing Duplicates from an Array in JavaScript'
date:   2020-2-4 12:19:00 -0500
categories: javascript
tags: javascript, js, array
header:
  image: /assets/images/remove-duplicates-header.jpg
---

## Outline
- purpose (why are we writing about this)
- ways to remove duplicates
  - brute force solution - O(n^2)
  - solution with hashmap - O(n)
  - Leveraging ES6
    - use sets
    - using filter
    - using filter and indexOf
- conclusion
- additional resources

While preparing for interviews as a manager I needed to excel at programming, people management, execution, and system design. The toughest for me was to knock of the programming rust and resist data structures and algorithms


Interviewing is hard. Interviewing as a manager can be additionally difficult: As a manager we must be excellent at people management, technical leadership, execution, system design, and programming all at once. Remember we are not _just_ managers, but _engineering_ managers. Staying technical is a constant challenge in our field and can be even more challengeing when your "day job", does not include even a _byte_ of coding :). Whether managers should code or not is of great debate, yet regardless, managers are expected to if not be currently proficient, show that at one point they were a blackbelt ninja wizard (yes, I am being sarcastic).

The implication? The vast majority of job interviews as a manager will include a programming question or set of questions. This may be conducted in the initial phone screen, a take home leetcode / hackerrank test, during a dedicated portion of the interview loop, or all of the above.

So to knock the rust off, I have gone back into the dojo, sharpened my katanas, and tightened my gi (it still fits, if a little tight around the waist).

A standard phone screen / fizzbuzz question is the classic "remove duplicates from an array" problem. Please note, all of your top tier tech companies will _not_ ask this question. However, it is a great warmup and can both grow our time complexity understanding and show our range of language understanding.

Let's get to it!

## Remove Duplicates
From the book [Programming Interviews Exposed](https://www.amazon.com/Programming-Interviews-Exposed-Secrets-Landing/dp/1118261364)

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

Running the code is straightforward
```javascript
const duplicates = [5,2,3,2,5,5,1,7,2,1,5,8];
console.log(removeDuplicates(duplicates)); //[ 5, 2, 3, 1, 7, 8 ]
```

This is a brute force solution with a quadratic time complexity, i.e. O(n<sup>2</sup>). As we are looping through two arrays. Can we get to this to linear time? Yes, by using a hash-map we can!

## Removing Duplicates using a hash-map
In our brute force solution, we loop through the array twice, what if we were to loop through just once? We can do this by using a map to keep track of if we have previously added the current element to our _result_ array or not.  
```javascript
function dedup(array) {
  const result = [];
  const map = {};

  //loop through array
  //if the element has been seen, continue to next element.
  //if that element has not been seen, add it to the result array.
  for (let i = 0; i < array.length; i++) {
    if (map[array[i]]) {
      continue;
    } else {
      result.push(array[i]);
      map[array[i]] = true;
    }
  }
  return b;
}
```

Again we can run this code to see the results
```javascript
const a = [1,1,2,3,3,4,4,5,5];
const b = [2,3,3,1,2,7,5,5,4,9,4,14];
const c = [5,2,3,2,5,5,1,7,2,1,5,8];

console.log(dedup(a)) //[1,2,3,4,5]
console.log(dedup(b)) //[2,3,1,7,5,4,9,14]
console.log(dedup(c)) //[5,2,3,1,7,8]
```

The general idea of this solution is to maintain a mapping of our elements to a boolean value of whether the element has been added to our `result` array or not. Stated differently, the boolean represents either yes we have added this element to the `result` (`true`) or no we have not (`false`).

The chart below illustrates the state of variables, in the simple case of an array `[1,1,2]`.

|index | array[index] | map[index] | result
0 | 1 | undefined | [1]
1 | 1 | true | [1]
2 | 2 | undefined | [1,2]


## What about using ES6?

OK, Ajahne, this is cool and all, but can we leverage ES6?

Definitely, please note, that some interviewers may [veto built-in methods or utilizing certain objects](https://leetcode.com/discuss/interview-question/168757/Google%3A-Remove-Duplicates-from-Unsorted-Array), to get a better sense of how you approach a problem. In that case, it is still worth mentioning that "I would use a set in this way..." or "I could leverage filter like so...". Showing your knowledge of the language will definitely get you some brownie points!

With that being said, let me upgrade you!

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

## Removing duplicates using `Array.filter()`
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

### Removing duplicates using `Array.filter()` with `Array.indexOf()`

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

## Conclusion

## Additional Resources
- [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)
- [Array.prototype.indexOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)
- [Array.prototype.filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- [Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
- [Programming Interviews Exposed](https://www.amazon.com/Programming-Interviews-Exposed-Secrets-Landing/dp/1118261364)
- [Leetcode: Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
