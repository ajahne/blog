---
layout: single
title:  'Removing Duplicates from an Array in JavaScript'
date:   2020-2-4 12:19:00 -0500
categories: javascript
tags: javascript, js, array
header:
  image: /assets/images/20-for-20-header.jpg
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

## Remove Duplicates

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
