---
layout: single
title:  "Searching for text on a page with Puppeteer"
date:   2018-9-6 04:11:29 -0400
categories: javascript
tags: javascript
header:
  image: /assets/images/puppeteer-header-banner.jpg
---


# outline
- intro - what we are trying to solve for
  - context into how this came about or you may need this
When using [puppeteer](https://github.com/GoogleChrome/puppeteer) there are times when you may need to check to see if text exists on a page.  
- Dev steps
  - install puppeteer
  - create browser
  ```
  const browser = await puppeteer.launch();
  ```
  - create page
  ```
  const page = await browser.newPage();
  ```
  - go to desired page
  ```
  await page.goto(url)
  ```
  - check to see if text exists on the page
  ```
  const options = { timeout: 300000 };
    //wait for page to load xml
  await page.waitForFunction(
    'document.querySelector("body").innerText.includes("Clearing cache on");',
    options
  );
  ```
  - do something now that the page has loaded (e.g. take a screenshot)
  ```
  await page.screenshot()
  ```

# conclusion
