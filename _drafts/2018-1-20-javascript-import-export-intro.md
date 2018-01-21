---
layout: post
title:  "A quick introduction to Javascript import and export"
date:   2018-01-20 22:10:29 -0400
categories: jekyll javascript import export
---

### Introduction
JavaScript modules are now supported in most modern browsers.
Browser support includes:
- Edge 16+
- Chrome 61+
- Safari 10.1+
- iOS Safari 10.3+
- Chrome for Android 62+

Be sure to check out [caniuse](https://caniuse.com/#search=export) for the latest.

Now let's code.

### Setup
We will not be using a module loader, bundler, or third party tool (e.g. no babel, webpack, rollup, etc.) as we are leveraging modern browsers. For this to work, we will need to use ```type="module"``` for our script.

_index.html_
{% highlight html %}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ES6 module demo</title>
</head>
<body>
<script type="module" src="main.js"></script>
</body>
</html>
{% endhighlight %}

### Export
The first thing we want to do is write code and allow that code to be used in another place, we can achieve this with ```export```.

There are two ways to export: default and named. Let's write a quick utility and then show how to utilize default and named

_utils.js_
{% highlight js %}
let add = (a,b) => a + b;
{% endhighlight %}

#### default
The default export will be exported by, yep you guessed it default.  This means that it will be the base import by another piece of code.  Let's see how that works
_utils.js_
{% highlight js %}
let add = (a,b) => a + b;

export default add;
{% endhighlight %}

_main.js_
{% highlight js %}
import add from 'utils.js'

console.log(add(5,4));  //9
{% endhighlight %}

as the ```add``` function is the default export, even if we change the name of the identifier when importing, it will still map to the ```add``` function.
{% highlight js %}
//changing the identifier to show how it does not matter
import foo from 'utils.js'

console.log(foo(5,4));  //9
{% endhighlight %}


#### named

### Import

### More examples

### Conclusion

### Additional Resources
