---
layout: single
title:  'setTimeout(callback, 0) !== 0ms'
date:   2018-5-8 0:06:00 -0400
categories: leadership
header:
  image: /assets/images/timers.jpg
---
Outline
- setTimeout(cb, 0) !== 0ms
- currently working on a program the randomizes the time it takes to complete.  It simulates a user's play-through by randomizing when certain actions (e.g. button click, data submission) occur.
- Note: for the purpose of this discussion "instantaneous" or "instant" means code that can run immediately (e.g. was not placed on a queue by setTimeout or setInterval)
- setTimeout and setInterval have a minimum delay
  - 4ms in browsers
  - 1ms in node
- Implications
  - setting delay of 0ms with not happen instantaneous
- Nice to have
  - charts

## Examples to create

### Specifications
- System: Dell Latitude E5570. 16MB RAM, Processor: i7 2.60GHz. Windows 10
- Chrome - Version 66.0.3359.139
- Firefox - Version 60.0
- Node.js - Version 6.12.3

### Browser
All tests are performed on chrome.
How are the tests performed:
- open Chrome
- open developer tools
- open file
- see results

timer.js
```
const runInstant = () => {
  console.time();
  const arr = new Array(10000);
  for (let i = 0; i < arr.length; i++) {
    arr[i] = new Object();
  }
  console.timeEnd();
}

const runTimer = ()=> {
  const createObject = element => {
    element = new Object();
  }
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
The latest code can be found here.

### Browser Results
**Chrome**  
Loop
- run 1:
- run 2:
- run 3:
- run 4:
- run 5:

Loop with setTimeout
- run 1:
- run 2:
- run 3:
- run 4:
- run 5:

**Firefox**
Loop
- run 1:
- run 2:
- run 3:
- run 4:
- run 5:

Loop with setTimeout
- run 1:
- run 2:
- run 3:
- run 4:
- run 5:


### Node Results
Loop
- run 1:
- run 2:
- run 3:
- run 4:
- run 5:

Loop with setTimeout
- run 1:
- run 2:
- run 3:
- run 4:
- run 5:

## Additional Resources
- MDN [setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout)
- Node.js [setInterval](https://nodejs.org/api/timers.html#timers_setinterval_callback_delay_args)
and [setTimeout](https://nodejs.org/api/timers.html#timers_settimeout_callback_delay_args)
