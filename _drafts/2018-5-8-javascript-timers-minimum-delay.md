---
layout: single
title:  'setTimeout(callback, 0) !== 0ms'
date:   2018-5-8 0:06:00 -0400
categories: javascript
header:
  image: /assets/images/timers.jpg
---
Outline
- setTimeout(cb, 0) !== 0ms
- Note: for the purpose of this discussion "instantaneous" or "instant" means code that can run immediately (e.g. was not placed on a queue by setTimeout or setInterval)

tl;dr
- `setTimeout` and `setInterval` have a minimum delay
  - 4ms in browsers
  - 1ms in node
- Implications
  - setting delay of 0ms with not happen instantaneously

If you want a piece of code to execute instantly:
```
//do this 
runAweseomeCode();

Not this
setTimeout(runAweseomeCode, 0);
```

## Introduction
- currently working on a program the randomizes the time it takes to complete.  It simulates a user's play-through by randomizing when certain actions (e.g. button click, data submission) occur.


### System Specifications
- Computer: Dell Latitude E5570. 16MB RAM, Processor: i7 2.60GHz. Windows 10
- Chrome - Version 66.0.3359.139
- Firefox - Version 60.0
- Node.js - Version 10.1.0

## Test Steps
How are the tests performed:
- open Chrome
- open developer tools
- open file
- see results

## Test Code

loop.js
```
console.time();
const arr = new Array(10000);
for (let i = 0; i < arr.length; i++) {
  arr[i] = new Object();
}
console.timeEnd();
```

loop-settimeout.js
```
const runTimer = ()=> {
  const createObject = element => {
    element = new Object();
  };
  
  console.time();
  const arr = new Array(10000);
  for (let i = 0; i < arr.length; i++) {
    setTimeout(createObject, 0, arr[i]);
  }
  console.timeEnd();
}
runInstant();
runTimer();

```

The latest code can be found [here](https://github.com/ajahne/js-examples/tree/master/timers/settimeout).

## Test Results
### Chrome
Note: Chrome provides more significant digits than Firefox or Node and thus the times are rounded to the nearest whole number to provide equivalent levels of precision.

Loop
- run 1: 2ms
- run 2: 4ms
- run 3: 7ms
- run 4: 3ms
- run 5: 4ms


loop-settimeout.js
- run 1: 66ms
- run 2: 74ms
- run 3: 62ms
- run 4: 65ms
- run 5: 68ms

### Firefox

loop.js
- run 1: 4ms
- run 2: 4ms
- run 3: 5ms
- run 4: 2ms
- run 5: 3ms

loop-settimeout.js
- run 1: 26ms
- run 2: 21ms
- run 3: 21ms
- run 4: 23ms
- run 5: 22ms

### Node

loop.js:
- run 1: 0.592ms
- run 2: 0.574ms
- run 3: 0.586ms
- run 4: 0.702ms
- run 5: 0.583ms

loop-settimeout.js:
- run 1: 18.832ms
- run 2: 17.423ms
- run 3: 16.748ms
- run 4: 18.811ms
- run 5: 16.926ms

## Additional Resources
- MDN [setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout)
- Node.js [setInterval](https://nodejs.org/api/timers.html#timers_setinterval_callback_delay_args)
and [setTimeout](https://nodejs.org/api/timers.html#timers_settimeout_callback_delay_args)
- console.time examples leveraged from [google developers](https://developers.google.com/web/tools/chrome-devtools/console/console-reference)
