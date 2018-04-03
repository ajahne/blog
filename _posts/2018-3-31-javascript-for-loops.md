---
layout: single
title:  "Leveling up our `for` loops"
date:   2018-4-3 0:08:29 -0400
categories: javascript
header:
  image: /assets/images/up-arrows.jpg
---
So I don't know about you, but I am tired of writing the same ol' `for` loops over and over again. Each time I have to write `i=0; i<somethingLong; i++`, I think to myself (or mumble to my monitor), isn't there a better way of doing this?  Well yes there is!  ES6 introduces `for...of` and it's time for us to level up our loops.

The goal of this post is to improve our knowledge base while encouraging us to utilize the new `for...of` statement as we continue advancing our programming skills. So let's upgrade from `for` to `forEach` to the new hotness that is `for...of`.

### Before we get started
This article assumes you are familiar with `for` statements and loops in general. MDN provides great overviews [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/statements/for) and [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration#for_statement).

Let's loop!

## `for`
The O.G. The foundation.  The one, the only, the `for` loop.

{% highlight js %}
const list = [1, 2, 3, 4, 5];

for (let i = 0; i < list.length; i++) {
  console.log(list[i]);       //1, 2, 3, 4, 5
}
{% endhighlight %}

### `for` loops with `break` and `continue`
Using `continue`, we can skip to next iteration of the loop or terminate the current loop with `break`.
{% highlight js %}
const letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g'];

for (let i = 0; i < letters.length; i++) {
  //skip the 3rd element
  if (i === 2) {
    continue;
  }

  //do not execute after the 5th element
  if (i === 5) {
    break;
  }

  console.log(letters[i]);       //a, b, d, e
}
{% endhighlight %}

## `forEach`
Introduced with ES5 is the `forEach` method of the Array object. This method provides coding conciseness, allowing us to write less verbose statements.
{% highlight js %}
const list = [1, 2, 3, 4, 5];

list.forEach((element) => {
  console.log(element);     //1, 2, 3, 4, 5
});
{% endhighlight %}

Need the index and the array itself? `forEach` has got you covered.
{% highlight js %}
const list = ['a', 'b', 'c'];

list.forEach((element, index, array) => {
  console.log(`list[${index}]: ${element}`);    //list[0]: a, list[0]: b, list[0]: c
  console.log(`${array[index] === element}`);   //true, true, true
});
{% endhighlight %}

One of the downsides of the `forEach` method, is that it does not support `break` and `continue`.  So what if you need to `break` out of the loop or `continue` to the next step? `for...of` is the statement for you!

## `for...of`
The `for...of` statement provides us with the conciseness of `forEach` with the feature richness (e.g. `break` and `continue`) of the `for` statement.
{% highlight js %}
const list = [1, 2, 3, 4, 5];

for (let value of list) {
  console.log(value);     //1, 2, 3, 4, 5
}
{% endhighlight %}

### `for...of` vs `for...in`
`for...in` iterates over property names, while `for...of` iterates through the values in the array.
{% highlight js %}
const list = [1, 2, 3];
list.name = 'My Awesome List';

//for...in iterates over property names, so 'name' is looped over
for (let i in list) {
  console.log(i);       //0, 1, 2, name
}

//for...of iterates through the values in the array
for (let i of list) {
  console.log(i);       //1, 2, 3
}
{% endhighlight %}

### Getting `key` and `value` with `for...of`
Use destructuring to get key/value pairs
{% highlight js %}
const list = ['a', 'b', 'c'];

for (let [key, value] of list.entries()) {
  console.log(`${key} ${value}`);     //0 a, 1 b, 2 c
}
{% endhighlight %}

### Using `for...of` with `break` and `continue`
{% highlight js %}
const letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g'];

for (let [index, value] of letters.entries()) {
  //skip the 3rd element
  if (index === 2) {
    continue;
  }

  //do not execute after the 5th element
  if (index === 5) {
    break;
  }

  console.log(value);       //a, b, d, e
}
{% endhighlight %}

## Conclusion
By using `for...of` we can obtain the feature richness of the classic `for` loop, with the conciseness of the Array's `forEach` method.

Putting it all together, we can see the evolution from `for` to `forEach` to `for...of`.
{% highlight js %}
const arr = ['x', 'y', 'z'];

//for
for (let i = 0; i < arr.length; i++) {
  let element = arr[i];
  console.log(element);     //'x', 'y', 'z'
}

//forEach
arr.forEach((element) => {
  console.log(element);     //'x', 'y', 'z'
});

//for...of
for (let element of arr) {
  console.log(element);     //'x', 'y', 'z'
}
{% endhighlight %}

So now that we have leveled up our loops, we are ready to go [for]th and program even more awesomeness!  Check out the resources below and happy coding!

## Additional Resources
- Loops and Iteration from [Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)
- `for`, `forEach`, and `for...of` by [exploringjs](http://exploringjs.com/es6/ch_core-features.html#sec_for-foreach-forof)
- `Array.prototype.forEach` from [Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
- `for...of` from [Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
- `for...of` vs `for...in` on [stackoverflow](https://stackoverflow.com/questions/29285897/what-is-the-difference-between-for-in-and-for-of-in-javascript)
