---
layout: single
title:  "Leveling up our `for` loops"
date:   2018-3-31 10:00:29 -0400
categories: javascript
header:
  image: /assets/images/up-arrows.jpg
---
So I don't know about you, but I am tired of writing the same `for` loops over and over. ES6 introduces `for...of` and its time for us to level up our loops. The goal of this post is to get us using the new `for...of` statement and improve our coding skills. So let's upgrade from `for` to `forEach` to the new hotness that is `for...of`. Let's loop!

### Before we get started
This article assumes you are familiar with `for` statements and loops in general. MDN provides great overviews [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/statements/for) and [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration#for_statement).

Let's loop!

## for
The O.G. The original.  The one, the only, the `for` loop. Each time I have to write `i=0; i<somethingLong`, I think, isn't there a better way of doing this?  Well yes, but first, let's show out with some examples.

{% highlight js %}
const list = [1, 2, 3, 4, 5, 6, 7];
list.name = 'My Awesome List';

for (let i = 0; i < list.length; i++) {
  console.log(`list[${i}]: ${list[i]}`);
}
{% endhighlight %}

### `for` loops with `break` and `continue`
{% highlight js %}

for (let i = 0; i < list.length; i++) {
  //skip the 2nd index
  if (i == 2) {
    continue;
  }

  //do not execute after the 5th element
  if (i == 5) {
    break;
  }

  console.log(`list[${i}]: ${list[i]}`);
}
{% endhighlight %}

## `forEach`
Introduced with ES5 is the `forEach` method of the Array object. This gives us conciseness, allowing us to write less verbose loops.
{% highlight js %}
const list = [1, 2, 3, 4, 5, 6, 7];

//for reference, our basic for loop
for (let i = 0; i < list.length; i++) {
  console.log(list[i]);
}

//implementing the above with forEach
list.forEach((element) => {
  console.log(element);
});
{% endhighlight %}

### Need the index and the array itself? `forEach` has got you covered.
{% highlight js %}
const list = ['a', 'b', 'c'];
list.forEach((element, index, array) => {
  console.log(`list[${index}]: ${element}`);
  console.log(`${array[index] === element}`);
});
{% endhighlight %}

One of the downsides of the `forEach` method, is that is does not support `break` and `continue`.  So what if you need to `break` out and/or `continue` to the next step? `for...of` is the statement for you!

## `for...of`
The `for...of` provides us with the conciseness of `forEach` with the feature richness (e.g. `break` and `continue`) of the `for` statement.
{% highlight js %}
for (let i of list) {
  console.log(i);
}
{% endhighlight %}

### `for...of` vs `for...in`
`for...in` iterates over property names, while `for...of` iterates through the values in the array.
{% highlight js %}
const list = [1, 2, 3];
list.name = 'My Awesome List';

//iterates over property names, so 'name' is looped over
//e.g. the keys of your object
for (let i in list) {
  console.log(i);
}

for (let i of list) {
  console.log(i);
}
{% endhighlight %}

### Getting `key` and `value` with `for...of`
Using destructuring to get key/value pairs
{% highlight js %}
for (let [key,value] of list.entries()) {
  console.log(`${key} ${value}`);
}
{% endhighlight %}

## Putting it all together
So let's go `for` ==> `forEach` ==> `for...of`

## Conclusion

## Additional Resources
- [Loops and Iteration on Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)
- [for, foreach, and for on exploringjs](http://exploringjs.com/es6/ch_core-features.html#sec_for-foreach-forof)
- [Array.prototype.forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
- [for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
