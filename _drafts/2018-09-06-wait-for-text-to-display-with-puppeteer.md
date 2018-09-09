---
layout: single
title:  "Wait for text to display a page with Puppeteer"
date:   2018-9-6 04:11:29 -0400
categories: javascript
tags: javascript puppeteer text
header:
  image: /assets/images/puppeteer-header-banner.jpg
---

## Outline
- intro - what we are trying to solve for
  - context into how this came about or you may need this
When using [puppeteer](https://github.com/GoogleChrome/puppeteer) there are times when you may need to check to see if text exists on a page.  

The core of this solution leverages Puppeteer's [waitForFunction](https://github.com/GoogleChrome/puppeteer/blob/v1.8.0/docs/api.md#pagewaitforselectororfunctionortimeout-options-args) in conjunction with a JavaScript function that will be evaluated within the page's context.  While you can wait for a specific selector, a request, or a navigation change, waiting for text to display on the page takes an extra step.  

Let's dive in and Geppetto it up!  

## Step by Step Guide

### install puppeteer
```
npm i puppeteer
# or "yarn add puppeteer"
```

### Create browser
```
const browser = await puppeteer.launch();
```

### Create page
```
const page = await browser.newPage();
```

### Go to desired URL
```
await page.goto(url)
```

### Check to see if text exists on the page
```
const options = { timeout: 300000 };
  //wait for page to load xml
await page.waitForFunction(
  'document.querySelector("body").innerText.includes("Clearing cache on");',
  options
);
```

### Do something now that the page has loaded (e.g. take a screenshot)
```
await page.screenshot()
```

## Conclusion

## Additional Resources
- [Puppeteer on Github](https://github.com/GoogleChrome/puppeteer)
- [Puppeteer on Google Developers](https://developers.google.com/web/tools/puppeteer/)
- [Puppeteer API](https://github.com/GoogleChrome/puppeteer/blob/v1.8.0/docs/api.md)
