---
layout: single
title:  "Leveling up our `for` loops"
date:   2018-3-31 10:00:29 -0400
categories: javascript
header:
  image: /assets/images/up-arrows.jpg
---
So I don't know about you, but I am tired of writing the same `for` loops over and over. ES6 introduces `for of` and we can level up our loops. So let's upgrade from `for` to `forEach` to the new hotness that is `for of`.  Let's loop!


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

### for loops with break and continue
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

## forEach
Introduced with ES5 is the `forEach` method of the Array object. This gives us conciseness and
{% highlight js %}
//can perform the same, but cannot use break and continue
console.log('\nforEach');
list.forEach((element) => {
  console.log(`${element}`);
});
{% endhighlight %}

### need the index and the array itself? Its got you covered
{% highlight js %}
//can perform the same, but cannot use break and continue
console.log('\nforEach');
list.forEach((element, index, array) => {
  console.log(`list[${index}]: ${element}`);
});
{% endhighlight %}

## for of
### for of vs for in
{% highlight js %}
//iterates over property names, so 'name' is looped over
//e.g. the keys of your object
console.log('\nfor in');
for (let i in list) {
  console.log(`list[${i}]: ${list[i]}`);
}

//for of iterates through the values in the array
console.log('\nfor of');
for (let i of list) {
  console.log(i);
    // console.log(`list[${i}]: ${list[i]}`);
}
{% endhighlight %}

## Conclusion

## Additional Resources
http://exploringjs.com/es6/ch_core-features.html#sec_for-foreach-forof
