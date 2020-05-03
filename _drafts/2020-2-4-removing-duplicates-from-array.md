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

A standard phone screen / fizzbuzz question is the classic "remove duplicates from an array". Please note, all of your top tier tech companies will _not_ ask this question. However, it is a great warmup and can both grow your space complexity understand and show your range of language understanding.

Let's get to it!

## Remove Duplicates
From the book "Programming Interviews Exposed"

### Brute Force O(n^2)

```javascript
function removeDuplicates(in_arr) {
  const out_arr = [];
  for (let i = 0; i < in_arr.length; i++) {
    let exists = false;
    for (j = 0; j < out_arr.length; j++) {
      if (in_arr[i] === out_arr[j]) {
        exists = true;
        break;
      }
    }
    if (!exists) {
      out_arr.push(in_arr[i]);
    }
  }
  return out_arr;
}
```

Running the code is straightforward
```javascript
const duplicates = [5,2,3,2,5,5,1,7,2,1,5,8];
console.log(removeDuplicates(duplicates)); //[ 5, 2, 3, 1, 7, 8 ]
```

### Removing Duplicates, smarter using a hashmap
```javascript
function dedup(a) {
  const b = [];
  const map = {};

  //loop through array, if that number has not been seen
  //add it to the array, if it has, continue to next element
  for (let i = 0; i < a.length; i++) {
    if (map[a[i]]) {
      continue;
    } else {
      b.push(a[i]);
      map[a[i]] = true;
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

### Removing duplicates using a Set
```javascript
const array = [1,1,2,3,3,4,4,5,5];
const set = new Set(a);
const uniqueArray = [...set];
console.log(uniqueArray);
```

you can then one line this as
```javascript
const unique = [...new Set(array)];
console.log(unique)
```


### Removing duplicates using Array.filter()
```javascript
function dedup_filter(a) {
  const map = {};

  function isUnique(element) {
    if (map[element]) {
      return false
    } else {
      map[element] = true;
      return true;
    }
  }
  return a.filter(isUnique);
}

function dedup_filter_inline(a) {
  const map = {};
  // return a.filter(isUnique);
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

console.log(dedup_filter(a)) //[1,2,3,4,5]
console.log(dedup_filter(b)) //[2,3,1,7,5,4,9,14]
console.log(dedup_filter(c)) //[5,2,3,1,7,8]

console.log();
console.log(dedup_filter_inline(a)) //[1,2,3,4,5]
console.log(dedup_filter_inline(b)) //[2,3,1,7,5,4,9,14]
console.log(dedup_filter_inline(c)) //[5,2,3,1,7,8]
```

### Removing duplicates using Array.filter() with Array.indexOf()
```javascript
function dedup_filter_indexOf(a) {
  return a.filter((element, index) => a.indexOf(element) === index);
}

const a = [1,1,2,3,3,4,4,5,5];
const b = [2,3,3,1,2,7,5,5,4,9,4,14];
const c = [5,2,3,2,5,5,1,7,2,1,5,8];

console.log(dedup_filter_indexOf(a)) //[1,2,3,4,5]
console.log(dedup_filter_indexOf(b)) //[2,3,1,7,5,4,9,14]
console.log(dedup_filter_indexOf(c)) //[5,2,3,1,7,8]
```
