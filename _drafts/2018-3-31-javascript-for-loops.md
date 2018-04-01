---
layout: single
title:  "Leveling up our `for` loops"
date:   2018-3-31 10:00:29 -0400
categories: javascript
header:
  image: /assets/images/up-arrows.jpg
---
So I don't know about you, but I am tired of writing the same `for` loops over and over. ES6 introduces `for of` and its time for us to level up our loops. The goal of this post is to get us using the new `for of` statement and improve our coding skills. So let's upgrade from `for` to `forEach` to the new hotness that is `for of`. Let's loop!

## for
The O.G. The original.  The one, the only, the `for` loop. Each time I have to write `i=0; i<somethingLong`, I think, isn't there a better way of doing this?  Well yes, but first, let's show out with some examples.

{% highlight js %}
const list = [1, 2, 3, 4, 5, 6, 7];
list.name = 'My Awesome List';

console.log('for');
for (let i = 0; i < list.length; i++) {
  console.log(`list[${i}]: ${list[i]}`);
}
{% endhighlight %}

### `for` loops with `break` and `continue`
{% highlight js %}
//can perform the same, but cannot use break and continue
console.log('\nforEach');
list.forEach((element, index, array)=>{
  console.log(`list[${index}]: ${element}`);
});

console.log('\nfor with a break');
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
Introduced with ES5 is the `forEach` method of the Array object. This gives us conciseness, allow us to write less verbose loops
{% highlight js %}
//can perform the same, but cannot use break and continue
console.log('\nforEach');
list.forEach((element) => {
  console.log(`${element}`);
});
{% endhighlight %}

### Need the index and the array itself? Its got you covered
{% highlight js %}
//can perform the same, but cannot use break and continue
console.log('\nforEach');
list.forEach((element, index, array) => {
  console.log(`list[${index}]: ${element}`);
});
{% endhighlight %}

## `for of`
The `for of` provides us with the conciseness of `forEach` with the feature richness (e.g. `break` and `continue`) for the original `for` statement.
{% highlight js %}
//for of iterates through the values in the array
console.log('\nfor of');
for (let i of list) {
  console.log(i);
}
{% endhighlight %}

### `for of` vs `for in`
`for in` iterates over property names, so 'name' is looped over, while `for of` iterates through the values in the array.
{% highlight js %}
const list = [1, 2, 3, 4, 5, 6, 7];
list.name = 'My Awesome List';

//iterates over property names, so 'name' is looped over
//e.g. the keys of your object
console.log('\nfor in');
for (let i in list) {
  console.log(`list[${i}]: ${list[i]}`);
}

console.log('\nfor of');
for (let i of list) {
  console.log(i);
    // console.log(`list[${i}]: ${list[i]}`);
}
{% endhighlight %}

### Getting `key` and `value` with `for of`
Using destructuring to get key/value pairs
{% highlight js %}
console.log('\nfor of');
for (let [key,value] of list.entries()) {
  console.log(`${key} ${value}`);
}
{% endhighlight %}

## Conclusion

## Additional Resources
- [Loops and Iteration on Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)
- [for, foreach, and for on exploringjs](http://exploringjs.com/es6/ch_core-features.html#sec_for-foreach-forof)
- [Array.prototype.forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
- [for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
