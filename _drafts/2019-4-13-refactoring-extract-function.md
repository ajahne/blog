---
layout: single
title:  "Refactoring: Extract Function"
date:  2019-4-13 7:42:00 -0500
categories: javascript
tags: javascript, clean code, programming, books, refactoring
header:
  image: assets/images/refactoring-header-chapter-notes.jpg
---

#Outline
- Purpose - why even write this?
- What is refactoring
  - link to previous post
- Provide definition of Extract function
- Provide example of extract function
- conclusion
- additional resources


## Extract function
> Understand what the code is doing, then extract it into its own function named after its intent

{% highlight js %}
function printOwing(invoice) {
  printBanner();
  let outstanding  = calculateOutstanding();

  //print details
  console.log(`name: ${invoice.customer}`);
  console.log(`amount: ${outstanding}`);  
}
{% endhighlight %}

{% highlight js %}
function printOwing(invoice) {
  printBanner();
  let outstanding  = calculateOutstanding();
  printDetails(outstanding);

  function printDetails(outstanding) {
    console.log(`name: ${invoice.customer}`);
    console.log(`amount: ${outstanding}`);
  }
}
{% endhighlight %}

The process
- read and understand the code
- identify areas of the code we can pull out
- pull code out and duplicate it into a function (don't worry, this duplication is temporary)
- have the function call
- test after each step


## Additional Resources
[Refactoring - Extract Function](https://refactoring.com/catalog/extractFunction.html)
