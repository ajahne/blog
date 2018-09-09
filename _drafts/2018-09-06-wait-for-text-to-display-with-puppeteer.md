---
layout: single
title:  "Waiting for text on a page with Puppeteer"
date:   2018-9-6 04:11:29 -0400
categories: javascript
tags: javascript puppeteer text chrome headless
header:
  image: /assets/images/puppeteer-header-banner.jpg
---
When using [Puppeteer](https://github.com/GoogleChrome/puppeteer) there are times when you may need to check to see if text exists on a page - perhaps to ensure that the page has fully loaded or before executing another step in your automation pipeline.   

Here is a (pseudo-code) solution to this problem:
{% highlight js %}
const browser = await puppeteer.launch();
const page = await browser.newPage();
await page.goto("http://ajahne.github.io/blog/");
await page.waitForFunction(
  'document.querySelector("body").innerText.includes("Hello Ajahne");',
);
{% endhighlight %}

The core of this solution leverages Puppeteer's [waitForFunction](https://github.com/GoogleChrome/puppeteer/blob/v1.8.0/docs/api.md#pagewaitforfunctionpagefunction-options-args) in conjunction with a JavaScript function that will be evaluated within the page's context.  While you can wait for a specific selector, a request, or a navigation change, waiting for text to display on the page takes an extra step.  

The full details are outlined below.

Let's dive in and [Geppetto](https://en.wikipedia.org/wiki/Mister_Geppetto) it up!  

## Step by Step Guide
For this example we will load up [espn.com](http://www.espn.com) (which is a relatively large site) and check for the text "NBA". You can use this example to load up any site and wait for any text.  However, please be aware of Puppeteer's [default timeout of 30 seconds](https://github.com/GoogleChrome/puppeteer/blob/v1.8.0/docs/api.md#pagesetdefaultnavigationtimeouttimeout) when doing so and extend it accordingly if your situation requires.

### Install Puppeteer
{% highlight shell %}
npm i puppeteer
# or "yarn add puppeteer"
{% endhighlight %}

### Create a browser instance
{% highlight js %}
const url = "http://espn.com";
const text = "NBA";
const browser = await puppeteer.launch();
{% endhighlight %}

### Create a page
{% highlight js %}
const page = await browser.newPage();
{% endhighlight %}

### Go to the desired URL
{% highlight js %}
await page.goto(url);
{% endhighlight %}

### Check to see if text exists on the page
{% highlight js %}
//wait for page to load and display the text
await page.waitForFunction(
  'document.querySelector("body").innerText.includes(text);',
);
{% endhighlight %}

### Do something now that the page has loaded (e.g. take a screenshot)
{% highlight js %}
await page.screenshot();
{% endhighlight %}

## The full script
{% highlight js %}
const puppeteer = require('puppeteer');
(async () => {
  const url = 'http://espn.com';
  const text = 'NBA';

  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await page.goto(url);

  try {
    await page.waitForFunction(
      text => document.querySelector("body").innerText.includes(text),
      {},
      text
    );
  }
  catch(e) {
    console.log(`The text "${text}" was not found on the page`);
  }

  await page.screenshot({path: 'page.png', fullPage:true});
  await browser.close();
})();
{% endhighlight %}

### Run the script (assumes code saved to "`wait-for-text.js`")
{% highlight shell %}
node wait-for-text.js
{% endhighlight %}

## Conclusion
We have created a solution that will wait for text on a page to display before proceeding to the next step in execution.  This script is helpful if you have any server side scripts (e.g. PHP) that may render text on the page by modifying the DOM without changing the URL.  Good luck with your puppeteering and check out the additional resources below.  Happy coding!

## Additional Resources
- [Puppeteer on Github](https://github.com/GoogleChrome/puppeteer)
- [Puppeteer on Google Developers](https://developers.google.com/web/tools/puppeteer/)
- [Puppeteer API](https://github.com/GoogleChrome/puppeteer/blob/v1.8.0/docs/api.md)
- [StackOverflow: wait for text to appear with Puppeteer](https://stackoverflow.com/questions/46825300/wait-for-text-to-appear-when-using-puppeteer/46825433)
