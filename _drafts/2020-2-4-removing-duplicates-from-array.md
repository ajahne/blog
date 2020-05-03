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
  - brute force for loop - O(n^2);
  - solution with hash?  - is there an O(n) solution w/o using built in functions?
    - probably if you use a frequency table
  - use sets
  - use filter
  - use reduce
  - can you use map?
- conclusion
- additional resources

While preparing for interviews as a manager I needed to excel at programming, people management, exceution, and system design. The toughest for me was to knock of the programming rust and revist data structures and algorithms


Interviewing is hard. Interviewing as a manager can be additionally difficult: As a manager we must be excellent at people management, technical leadership, execution, system design, and programming all at once. Remember we are not _just_ managers, but _engineering_ managers. Staying technical is a constant challenge in our field and can be even more challengeing when your "day job", does not include even a _byte_ of coding :). Whether managers should code or not is of great debate, yet regardless, managers are expected to if not be currently proficient, show that at one point they were a blackbelt ninja wizard (yes, I am being sarcastic).

The implication? The vast majority of job interviews as a manager will include a programming question or set of questions. This may be conducted in the initial phone screen, a take home leetcode / hackerrank test, during a dedicated portion of the interview loop, or all of the above.

So to knock the rust off, I have gone back into the dojo, sharpened my katanas, and tightened my gi (it still fits, if a little tight around the waist).

A standard phone screen / fizzbuzz question is the classic "remove duplicates from an array". Please note, all of your top tier tech companies will _not_ ask this question. However, it is a great warmup and can both grow your time complexity understanding and show your range of language understanding.

Let's get to it!

## Remove Duplicates
From the book "Programming Interviews Exposed"

So how might we approach this problem?

## Brute Force
One solution is to loop through the original _array_ and for every element in the array, check to see if it exists in our _result_ array. If the element exists in _result_ skip to the next element, if not, add it to the _result_ array. Once complete, return _result_.  
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

This is brute force solution with a quadratic time complexity, i.e. O(n<sup>2</sup>). As we are looping through 2 arrays, each one of size n. Can we do better? Can we get to this to linear time? Yes, yes we can!

## Removing Duplicates using a hashmap
In our brute force solution, we loop through the array twice, what if we loop through once, We can do this by using a map to keep track if we have previously added the current element to our _result_ array or not.  
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


## What about using ES6?

OK, Ajahne, this is cool and all, but can we leverage ES6?

Well yes, we can. Please note, that some interviewers may veto this to get a better sense of how you approach a problem. In that case, it is still worth mentioning that "I would use a set" or "I could leverage filter" to show your knowleged of the language will definitely get you some brownie points!

So how might we do this in modern JavaScript?


## Removing duplicates using a Set
My preferred method if removing duplicates from an array is to use a `Set`. As a set can only have unique values by definition, it is primed specifically to solve this problem.
```javascript
const array = [1,1,2,3,3,4,4,5,5];
const set = new Set(a);
const uniqueArray = [...set];
console.log(uniqueArray);
```
What we do is create an array, make a new set using this array as an initial parameter to the Set's constructor. We can then use the spread operator to transform a set into an Array.


Furthermore, you can then one line this as
```javascript
const unique = [...new Set(array)];
console.log(unique)
```

Cool, so how else might we do this?

## Removing duplicates using Array.filter()
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

### Removing duplicates using Array.filter() with Array.indexOf()

```javascript
function dedupWithFilterAndIndexOf(a) {
  return a.filter((element, index) => a.indexOf(element) === index);
}

const a = [1,1,2,3,3,4,4,5,5];
const b = [2,3,3,1,2,7,5,5,4,9,4,14];
const c = [5,2,3,2,5,5,1,7,2,1,5,8];
xw
console.log(dedupWithFilterAndIndexOf(a)) //[1,2,3,4,5]
console.log(dedupWithFilterAndIndexOf(b)) //[2,3,1,7,5,4,9,14]
console.log(dedupWithFilterAndIndexOf(c)) //[5,2,3,1,7,8]
```

## Conclusion

## Additional Resources
