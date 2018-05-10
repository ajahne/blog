---
layout: single
title:  'setTimeout(fn, 0) !== 0ms'
date:   2018-5-10 01:49:00 -0400
categories: javascript
header:
  image: /assets/images/timers.jpg
---
When working with timers, setting a delay of 0, does not equate to 0ms or "instant" execution. This longer than expected delay may occur because the OS/browser/system is busy with other tasks or because the timer has been throttled.

_Note: for the purpose of this discussion "instantaneous" or "instant" means code that can run immediately (e.g. code that was not placed on a queue by setTimeout or setInterval)_

### Timeout Throttling
Each JavaScript environment, be it the browser or Node.js, throttles `setTimeout` and `setInterval`. This throttle means that `setTimeout` and `setInterval` have a minimum delay that is greater than 0ms.  

**The minimum delay is:**
- 4ms in browsers ([per MDN](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout#Notes))
  - This throttle occurs when successive calls are triggered due to callback nesting or after a certain number of successive intervals
- 1ms in Node.js ([per Node docs](https://nodejs.org/api/timers.html#timers_settimeout_callback_delay_args))

The implication being that setting a delay of 0ms will not happen instantaneously.

### Late timeouts
From MDN
> The timeout can also fire later when the page (or the OS/browser itself) is busy with other tasks.  One important case to note is that the function or code snippet cannot be executed until the thread that called `setTimeout()`` has terminated. 

For example:

{% highlight js %}
function runAwesomeCode() {
    console.log('Everything is awesome');
}
setTimeout(runAwesomeCode, 0);
console.log('Awesomeness completed');
{% endhighlight %}

Results in

{% highlight js %}
Awesomeness completed
Everything is awesome
{% endhighlight %}

Not quite what we expected, is it?  This is because even though we set a delay of 0, the code within a timer is placed on a queue and scheduled to run at the next opportunity, not immediately. Code that is currently executing  must complete before functions on the queue are run.

## Background aka how did this come up?
At my company, one of our current strategic initiatives is to enhance the scalability of our infrastructure.  To that end, members of the DevOps team are conducting performance tests on our servers to better understand the maximum user load we can support while maintaining our KPIs. To facilitate this testing, the team is building a tool that simulates a play-through on our web application and randomizes when certain actions (e.g. button clicks, data submissions) occur. Once completed, this tool will be "spawned" across multiple server instances to hammer our infrastructure :).

A requirement of this tool is to both run "instantly" (to maximize hits per minute) and "randomly" (within specified ranges of time) to simulate user interaction.

While testing, we observed that when setting a timeout of 0, the overall play-through was taking longer than expected.  After further research, we discovered that yes, a delay of 0, does not equal 0ms and is definitely not "instant".  

Now that we have a little background, let's dive into tests we conducted to illustrate the minimum delay used by `setTimeout` and `setInterval`.

## Testing details and steps:

### System Specifications
- Computer: Dell Latitude E5570. 16MB RAM, Processor: i7 2.60GHz. Windows 10
- Chrome - Version 66.0.3359.139
- Firefox - Version 60.0
- Node.js - Version 10.1.0

### How the tests were performed:  
**In the browser:**  
run the following steps 5 times for each file
- load [loop.html](https://github.com/ajahne/js-examples/blob/master/timers/settimeout/loop.html) or [loop-settimeout.html](https://github.com/ajahne/js-examples/blob/master/timers/settimeout/loop-settimeout.html) in the browser
- open up developer tools
- view results
- clear cache
- refresh the browser

**In Node.js:**  
run each statement below 5 times
```
node loop.js
```
```
node loop-settimeout.js
```

## Test Code
`loop.js`
{% highlight js %}
console.time();
const arr = new Array(10000);
for (let i = 0; i < arr.length; i++) {
  arr[i] = new Object();
}
console.timeEnd();
{% endhighlight %}

`loop-settimeout.js`
{% highlight js %}
const createObject = element => {
  element = new Object();
};

console.time();
const arr = new Array(10000);
for (let i = 0; i < arr.length; i++) {
  setTimeout(createObject, 0, arr[i]);
}
console.timeEnd();
{% endhighlight %}

The code can be found [here](https://github.com/ajahne/js-examples/tree/master/timers/settimeout).

## Test Results
### Chrome
_Note: Chrome provides more significant digits than Firefox and thus the times are rounded to the nearest whole number to provide equivalent levels of precision._

|Run      |loop.js      |loop-settimeout.js|
|---------|-------------|------------------|
|1        |2ms          |66ms
|2        |4ms          |74ms
|3        |7ms          |62ms
|4        |3ms          |65ms
|5        |4ms          |68ms

### Firefox  

|Run      |loop.js      |loop-settimeout.js|
|---------|-------------|------------------|
|1        |4ms          |26ms
|2        |4ms          |21ms
|3        |5ms          |21ms
|4        |2ms          |23ms
|5        |3ms          |22ms

### Node  

|Run      |loop.js      |loop-settimeout.js|
|---------|-------------|------------------|
|1        |0.592ms      |18.832ms
|2        |0.574ms      |17.423ms
|3        |0.586ms      |16.748ms
|4        |0.702ms      |18.811ms
|5        |0.583ms      |16.926ms

## Conclusion
By comparing `for` loops that do and do not utilize timers, our test results confirm that `setTimeout` and `setInterval` indeed have a minimum delay.
**Knowing this, if you want a piece of code to execute instantly, do not use timers.**
{% highlight js %}
//To ensure code runs immediately
//do this
runAweseomeCode();

//Not this
setTimeout(runAweseomeCode, 0);
{% endhighlight %}

Check out the additional documentation below and happy coding!

## Additional Resources
- MDN [setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout)
- Node.js [setInterval](https://nodejs.org/api/timers.html#timers_setinterval_callback_delay_args)
and [setTimeout](https://nodejs.org/api/timers.html#timers_settimeout_callback_delay_args)
- console.time examples leveraged from [google developers](https://developers.google.com/web/tools/chrome-devtools/console/console-reference)
