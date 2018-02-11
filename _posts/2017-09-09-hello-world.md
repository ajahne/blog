---
layout: single
title:  "Hello Blog!"
date:   2017-09-09 20:56:29 -0400
---

### Hello Blog!  Here is my first (test) post!!!  

I am using this post to try out **different** _markdown_ ~~syntax~~ including
- code snippets
- links
- and more!

**JavaScript** snippet:
{% highlight js %}
//simple lines to prove highlight
const message = 'Hello World';
console.log(message);
{% endhighlight %}

**_HTML_** snippet:
{% highlight html %}
<html>
  <head>
    <title>HTML syntax</title>
  </head>
  <body>
    <p class="text">Hello World</p>
    <div id="box">Block</div>
  </body>
<html>
{% endhighlight %}

``CSS`` snippet:
{% highlight css %}
.text {
  color: #003366;
  font-size: 16px;
}

#box {
  width: 100px;
  height: 100px;
}
{% endhighlight %}

Testing out URLs:
Check out the [post I wrote about JavaScript functions]({{ site.baseurl }}{% post_url 2017-10-9-javascript-functions-part-1 %}) as well as my [github page][github]!

[github]: https://github.com/ajahne
