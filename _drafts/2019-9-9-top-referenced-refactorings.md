---
layout: single
title:  "The Most Referenced Refactorings"
date:  2019-9-9 12:42:00 -0400
categories: javascript
tags: javascript, clean code, programming, books, refactoring
header:
  image: assets/images/refactoring-header-most-referenced-refactorings.jpg
---

[Refactoring (2nd Edition) by Martin Fowler](http://www.informit.com/store/refactoring-improving-the-design-of-existing-code-9780134757711) is one the *best* programming books I have read. Full stop.  I have utilized this book to train and coach developers on my team, improve the design of my code, and grow as an engineer. Similar to [Pragmatic Programmer](https://www.amazon.com/Pragmatic-Programmer-Journeyman-Master/dp/020161622X), [Clean Code](), and others, this book helped me level up as an engineer.

After reading the book, I wanted to ascertain which refactorings Martin mentioned the most.

## Outline and TOC (click to jump)
- [Purpose aka why did I do this?](#purpose-aka-why-did-i-do-this)
- [The Results aka Them Charts!](#the-results-aka-them-charts)
  -[What the data tells us](#so-what-does-this-data-tell-us)
- [Algorithm and Process (How the deed was done)](#part-2-how-the-deed-was-done)
- [Conclusion](#conclusion)
- [Additional Resources](#additional-resources)

## Purpose aka why did I do this?
I wanted to plot Martin's _(yep, we on a first name basis)_ most referenced refactorings. Why? Because I wanted to understand which refactorings were mentioned most often.  Almost every refactoring listed in the book depends upon another refactoring. For example "Extract Function" mentions "Split Variable (240)" and "Replace Temp with Query (178)". While I may utilize "Extract Function" often, could I improve the design of my code by better understanding those other two refactorings?

After reading the book, I had my list of fundamental refactorings, key techniques that I used in my own code and coached peers, senior engineers, and junior developers on (through code reviews, pair programming, etc.). However, what if I was missing something? What if there was a refactoring that I glossed over, but was referenced numerous times as a "prerequisite" for others that I should take a second look at. For example, after crunching the numbers I want to revisit "Replace Conditional with Polymorphism".

Furthermore, maybe I could gleam a bit of what Martin finds important or references the most. Could this information help me recommended to peers and other engineers certain refactorings to check out or "start with first". Martin tells the reader to [read the first 100 pages]({{ site.baseurl }}{% post_url 2019-3-29-refactoring-by-martin-fowler-chapter-notes %}), then skim the refactorings.  OK, but is there anything I should _skim_ a little bit more?

Lastly, I wanted to experiment with [Chart.js](https://www.chartjs.org) and [PDF.js](pdfjs). I had this idea of plotting the data and needed to see if I could do it.  A new opportunity, a new thing to learn, you know us engineers, we like that new and shiny. So, let's [shine](https://youtu.be/wuw6Xu9ZARU?t=40)!

Graph time!

## The Results aka Them Charts!
**The top 5 referenced refactorings**
![]({{site.baseurl}}/assets/images/refactoring-charts/refactoring-top-five-labeled.jpg)

**The top 10**
![]({{site.baseurl}}/assets/images/refactoring-charts/refactoring-top-10.png)

**The top 25**
![]({{site.baseurl}}/assets/images/refactoring-charts/refactoring-top-25.png)

<!-- <figure>
    <a href="/blog/assets/images/refactoring-charts/refactoring-top-25.png"><img src="/blog/assets/images/refactoring-charts/refactoring-top-25.png"></a>
    <figcaption>All the refactorings plotted, click to enlarge</figcaption>
</figure> -->


_Please note that there are over 60 refactorings and plotting all of those barely fits (legibly) on the screen.  To see the full data set, please [check out the code](https://github.com/ajahne/refactoring-references)._

## So what does this data tell us?
Well I knew the king of the land was (and is) "Extract Function". If there is _one_ refactoring you learn, let it be this one! It is referenced almost twice as much (85) as the next refactoring "Change Function Declaration" (45). It is the building block for numerous refactorings.

Additionally, techniques related to refactoring functions are highly referenced. As we know, functions are an essential building block of our programs, so it makes intuitive sense that these refactorings would rate highly. While this was insightful, I did not think four out of the top five would be related to functions!

So, my original hypothesis was that the following 5 refactorings would be referenced the most

> Extract Function  
> Move Function  
> Extract Variable  
> Inline Function  
> Rename Variable

So yeah...I was off!

In short, I hypothesized that there would be more references to refactorings related to variables and classes. And _this_ is why we do the experiment!

Now, because a refactoring is mentioned more than another does that make it more _important_?  No.  While "Extract Function" is essential, there are additional refactorings such as "Rename Variable", "Replace Temp with Query", and "Decompose Conditional" that are fundamental to make cleaner, more maintainable, and economic code.

Now that we've discussed the data, how did we do it?

# Part 2: How the deed was done.

## My initial thoughts and high level ideas
There are over 60 refactorings mentioned within the book and over 400 pages! Where to begin?

First I needed to convert the book (i.e. pdf) to text so I could read the information programmatically. My idea was to convert it to text (e.g a string) and perform a series regular expressions on the string to obtain the number of times a particular snippet (i.e. match) was found.

_A quick note:
I did not just search for the string of a refactoring, but the actual **page number** string that it appears on.  This was to avoid references to the refactoring that occurs in its own chapter. For example, if I were to search for "Extract Function" then I would get all of the references including those it own section, potentially skewing the data! I don’t want to include those. What I noticed is that Martin references the refactoring plus it’s page number (e.g. "(106)") when one refactoring refers to another. Based on this, all of my searches are based on the page number of the refactoring._

Once I found the information, I needed to double check a few of my results. To do this, yep you guessed it, I manually counted a few (whew!). I also used my IDE to search on the text file generated from PDF.js to see if my logic was correct. Plus I wrote a few tests!

Next, I needed to create the data structure needed for chart.js. With that I could being plotting my data.

I was inspired by an article that was like “hey have charts in your post” and I wanted that, so I made it. Chart.js is very easy to make charts with. However, ya boy needed images.

Hmmmm? A dilemma.

Chart.js has a function that returns the base64 encoded string. Once I have that I could create an image like so:

```javascript
chart.toBase64Image();
```

## Algorithm, process, and code breakdown
Once I had this image, right click, save as, and voila, charts! Whoa, no code for that you say? Nah, not at this time, this pet project already turned into a tiger, soon to be a Tetsuo, so I will enhance as times goes on. Version 1 my friends!

There are a few manual steps that I am looking to automate in future versions. However, small batches are king!

### Use PDF.js to read the file into memory
you can find the full source [here](https://github.com/ajahne/refactoring-references/blob/master/src/pdf/refactoring/parse-refactoring.js). My code is heavily inspired by the PDF.js example of [getinfo.js](https://github.com/mozilla/PDF.js/blob/master/examples/node/getinfo.js).

One important change I made was to handle newlines and spaces:

```javascript
return page.getTextContent({normalizeWhitespace:true}).then(function (content) {
  // Content contains lots of information about the text layout and
  // styles, but we need only strings at the moment
  const strings = content.items.map(function(item, index, array) {
    //.transform[5] is the y position of the current line
    //if a new "y", then its a new line, so add newline character
    let str = item.str;
    if (index > 0 && item.transform[5] !== array[index-1].transform[5]) {
      str = '\n' + str;
    }
    return str;
  });
//...more code, promises, etc.
});
```

Important to note in the above code is we want to ensure we are adding a new line character at the appropriate place. If we do not do this, lines will jumble together and make it harder for us to utilize our regex expressions later. We also normalize the white space, which according to the source

> replaces all occurrences of whitespace with standard spaces (0x20).

This helped both in programming and manual testing (e.g. ctrl+f in an IDE) to double check our logic.

### Save down the pdf to a text file
```javascript
fs.writeFile(outputFile, textContent, (err) => {
  if (err) throw err;
  console.log('file written');
});
```

### create a data structure based on the first page of Refactoring
- In the hardcover version of the book, all refactorings are listed with their corresponding page number). Note,I saved this down as a [json file](https://github.com/ajahne/refactoring-references/blob/master/src/regex/data/refactoring-page-numbers.json).

*refactoring-page-numbers.json*
```json
{
  "Change Function Declaration": "124",
  "Change Reference to Value": "252",
  "Change Value to Reference": "256",
  "Collapse Hierarchy": "380",
  "Combine Functions into Class": "144",
  "Combine Functions into Transform": "149",
  "Consolidate Conditional Expression": "263",
  "Decompose Conditional": "260",
  "Encapsulate Collection": "170",
  "Encapsulate Record": "162",
  "Encapsulate Variable": "132",
  "Extract Class": "182",
  "Extract Function": "106",
  "Extract Superclass": "375",
  "Extract Variable": "119",
  "Hide Delegate": "189",
  "Inline Class": "186",
  "Inline Function": "115",
  "Inline Variable": "123",
  "Introduce Assertion": "302",
  "Introduce Parameter Object": "140",
  "Introduce Special Case": "289",
  "Move Field": "207",
  "Move Function": "198",
  "Move Statements into Function": "213",
  "Move Statements to Callers": "217",
  "Parameterize Function": "310",
  "Preserve Whole Object": "319",
  "Pull Up Constructor Body": "355",
  "Pull Up Field": "353",
  "Pull Up Method": "350",
  "Push Down Field": "361",
  "Push Down Method": "359",
  "Remove Dead Code": "237",
  "Remove Flag Argument": "314",
  "Remove Middle Man": "192",
  "Remove Setting Method": "331",
  "Remove Subclass": "369",
  "Rename Field": "244",
  "Rename Variable": "137",
  "Replace Command with Function": "344",
  "Replace Conditional with Polymorphism": "272",
  "Replace Constructor with Factory Function": "334",
  "Replace Derived Variable with Query": "248",
  "Replace Function with Command": "337",
  "Replace Inline Code with Function": "222",
  "Replace Loop with Pipeline": "231",
  "Replace Nested Conditional with Guard Clauses": "266",
  "Replace Parameter with Query": "334",
  "Replace Primitive with Object": "174",
  "Replace Query with Parameter": "327",
  "Replace Subclass with Delegate": "381",
  "Replace Superclass with Delegate": "399",
  "Replace Temp with Query": "178",
  "Replace Type Code with Subclasses": "362",
  "Separate Query from Modifier": "306",
  "Slide Statements": "223",
  "Split Loop": "227",
  "Split Phase": "154",
  "Split Variable": "240",
  "Substitute Algorithm": "195"
}
```

### Read the text file into memory with node.js
```javascript
const file = '../pdf/assets/refactoring.txt';
...
...

fs.readFile(file, 'utf8', (err, data) => {
  if (err) throw err;
  const refactorings = createListOfRefactorings(data);
  sort(refactorings);
  createDataForChart(refactorings);
  writeRawData(refactorings);
});
```

This is the most straightforward piece and shows how I like to make my entry functions a TLDR. We can see what is data place. The `file` is the `refactoring.txt` which we saved down with our pdf module.

`createListOfRefactorings` makes an array of objects for each refactorig with its name, page number, and the number of references. You can find the full data set [here](https://github.com/ajahne/refactoring-references/blob/master/src/regex/data/refactorings-references-in-descending-order.json), below is a snippet of the results
```javascript
[
 {
  "name": "Extract Function",
  "page": "106",
  "references": 85
 },
 {
  "name": "Change Function Declaration",
  "page": "124",
  "references": 45
 },
 {
  "name": "Inline Function",
  "page": "115",
  "references": 34
 },
 {
  "name": "Move Function",
  "page": "198",
  "references": 32
 },
 {
  "name": "Inline Variable",
  "page": "123",
  "references": 18
 },

 //...more records

 {
  "name": "Replace Nested Conditional with Guard Clauses",
  "page": "266",
  "references": 1
 }
]
```

## To obtain this information, we use regex.
The `data` is the in memory text file of the refactoring book as a string.
```javascript
function createListOfRefactorings(data) {
  const pageNumbers = getRefactoringPageNumbers();
  const refactorings = [];
  for (let key in pageNumbers) {
    let re = new RegExp('\\(' + pageNumbers[key] + '\\)', 'ig');
    refactorings.push({
      name: key,
      page: pageNumbers[key],
      references: data.match(re).length
    });
  }
  return refactorings;
}
```

```javascript
let re = new RegExp('\\(' + pageNumbers[key] + '\\)', 'ig');
```

This above line is the meat, which searches the entire file (e.g. 'g') and is case insensitive (e.g. "i"), where `pageNumbers[key]` would be 106, in the case of "Extract Function". As we loop through we push each object onto our array of refactorings and return the result.

Once we have the refactorings, we can save this information to a file as seen [here](https://github.com/ajahne/refactoring-references/blob/master/src/regex/data/refactorings-references-in-descending-order.json)

However, this is not the way chart.js needs the data structured.

whew...still with me?  

Look if you are fading, I feel you!  I thought this would be a quick project and yo, did it get involved!  Water break...stretch...cool?  We back

### Use chart.js to plot the data
Ok, so Chart.js needs an array of labels (e.g. the names of all Refactorings) and the data to plot (e.g. the number of references). I simply converted one data structure to the other


And ended up with the following
```javascript
{
 "labels": [
  "Extract Function",
  "Change Function Declaration",
  "Inline Function",
  "Move Function",
  "Inline Variable",
  //...edited for brevity...
 ],
 "data": [
  85,
  45,
  34,
  32,
  18,
  //...edited for brevity...
 ]
}

This we could now plug into chart.js and voila...CHARTS!!!!

```

## Conclusion
Refactoring is an essential read.  If you are an experienced engineer, many of the techniques in the book you may already used. However, this book gave me the vocabulary, the words needed to describe _what_ I was doing as well as the _how_. In turn, I could more easily coach members of my team on these techniques.  


## Additional Resources
- [Source Code](https://github.com/ajahne/refactoring-references)
- [Refactoring: The First 100 pages]({{ site.baseurl }}{% post_url 2019-3-29-refactoring-by-martin-fowler-chapter-notes %})
- [Chart.js](https://www.chartjs.org) and [PDF.js](pdfjs).
