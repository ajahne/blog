---
layout: single
title:  "Leveling up our JavaScript Array methods"
date:  2018-11-06 10:00:00 -0400
categories: javascript
tags: javascript
header:
  image: /assets/images/cto-meeting-scaling-nyc1.jpg
---

`Array.prototype.find()`

{% highlight js %}
const array1 = [5, 12, 8, 130, 44];

const found = array1.find(function(element) {
  return element > 10;
});

console.log(found); // 12
{% endhighlight %}

## Additional Resources
- [Array.prototype.find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
