---
layout: single
title: "JavaScript Closure"
date: 2017-12-23 6:10:00 -0400
categories: javascript
header:
  image: /assets/images/functions-part4-closure.jpg
---
We are back! The fun with functions tour continues.  Next stop…Closure!  

Oftentimes we as developers hear the term “closure” and become filled with anxiety.  Closures are not something mythical or magical, not some mystical creature hiding in the wilderness.  Rather, they are a practical concept that we use every time we write a function. The concept of Closure is sometimes confusing, but becomes clearer when we work with examples and write code.

Let's dive into our first closure:

{% highlight js %}
const castMagicSpell = (magicSpell) => {
  const magicWords = `I am casting ${magicSpell}`;
  //the closure allows our doMagic function 
  //to access the magicWords variable
  const doMagic = () => {
    console.log(magicWords);
  }
  doMagic();
}

castMagicSpell('abracadabra'); //I am casting abracadabra
{% endhighlight %}

Pretty straightforward, now let's go further, starting with some definitions.

### Definition
The "academic" definition of closure can simply be “an inner function defined in an outer function” or “the creation of a function, creates a closure”.  While both of these statements are technically true, they do not get to the practical purposes and application of closures.  

**A technical definition**: A function that references the lexical scope.

**A practical definition**: An inner function defined in an outer function that retains access to the outer function’s scope (e.g. variables) after the outer function has returned. _Technically, the outer function does not have to return_.

### Key takeaways
- Every JavaScript function forms a closure
- It “encloses” the lexical scope
  - E.g.: A function that is defined on global scope, encloses the global variables and has access to them
- An inner function has three scope chains
  - Its own scope, its containing function’s scope, and global scope
- An inner function has access to the outer function’s variables and arguments

### Closures and lexical scoping
- **Lexical scoping**: the scope declared at author time.
- Closures can access their lexical scope (variables declared at author time), even when it is executed outside of its lexical scope (i.e. called at a later time)

### Why/when would we use closure?
So all that is well and good, but what can we actually do?  Why do we even care?  Well, by using closures we can write code that addresses the following two concepts: privacy and state.

**Privacy**  
JavaScript does not have private methods.  However, the use of closures, can emulate this concept. Privacy is a way of separating concerns, keeping non-essential methods from being accessed through our public API.

{% highlight js %}
const createDinnerMaker = () => {
  let temperature = 0;
  
  const bake = food => {
    console.log('baking: ' + food);
  }
  
  const bakeChicken = () => {
    setOvenTemperature(425);
    bake('chicken');
  }
  
  const bakeFish = () => {
    setOvenTemperature(350);
    bake('fish');
  }
  
  const setOvenTemperature = value => {
    temperature = value;
  }  
  
  return {
    bakeChicken,
    bakeFish
  }
}

//calling the function makeDinner returns an object
//this return triggers the closure.
const myDinnerMaker = createDinnerMaker();
myDinnerMaker.bakeChicken(); //baking chicken
myDinnerMaker.bakeFish();    //baking fish
{% endhighlight %}
You can view the codepen version [here](https://codepen.io/ajahne/pen/BRgXyp?editors=0012).

**State**  
We can also use closure to maintain the value (i.e. ‘state’) of function arguments at a certain time. We do this through the technique of partial function application. This way we can apply only a subset (i.e. ‘partial’ set) of arguments to a function.

{% highlight js %}
const number = '271-7713';

const addAreaCode = areaCode => {
  return (number) => {
    return areaCode + number;
  }
}

const addNewYorkAreaCode = addAreaCode('212-');
const addSpringfieldAreaCode = addAreaCode('413-');

console.log(addSpringfieldAreaCode(number)); //413-271-7713
console.log(addNewYorkAreaCode(number));     //212-271-7713
{% endhighlight %}
You can view the codepen version [here](https://codepen.io/ajahne/pen/gWNVrw?editors=0012).

### More examples

**Loops**  
Sometimes creating a function in a loop (say creating a callback for a DOM event listener) may not work as expected given how the closure is created ([see codepen example](https://codepen.io/ajahne/pen/jmjgLx?editors=1011)).  To better handle this scenario and ensure our handlers work as expected in our loops, we can [utilize additional closures](https://codepen.io/ajahne/pen/LyKwOE?editors=1011).

**SetTimeout**  
Another time we may run into challenges with scope and require closures is with `setTimeout`.  To illustrate the different ways (through IFFE, through explicit function calls) that we can ensure we are accessing variables as expected, [explore this setTimeout example](https://codepen.io/ajahne/pen/qmzJgp).

### Conclusion
Ok, still with me? Let’s recap: Closure occurs every time a function is created and this function has access to the variables of its outer scope (be it global or a containing function).  Additionally, this function retains access to this outer scope and can continue to access this scope (variables, etc.).  Not so bad, right? Right. For additional examples and readings, check out the resources below.

### Additional Resources
- A great [introduction to closures from Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) that provides practical cases
- A great [stackoverflow answer](https://stackoverflow.com/questions/111102/how-do-javascript-closures-work) with additional examples
- [JavaScript is sexy](http://javascriptissexy.com/understand-javascript-closures-with-ease/) on understanding closures
- Additional medium resource of [closures in plain English](https://medium.freecodecamp.org/whats-a-javascript-closure-in-plain-english-please-6a1fc1d2ff1c)
- Mastering the JS interview by answering, [what is closure?](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36)
