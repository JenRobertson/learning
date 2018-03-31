# JS Questions:

## Explain event delegation ##

## Explain how `this` works in JavaScript ## 

This refers to the object that you are currently inside.
For example, in an object, `this` can be used to reference a property of the object like `this.cheese`

## Explain how prototypal inheritance works ## 

A prototype is a template for something. If you inherit from a prototype, you get all of its methods and properties

 ##  What do you think of AMD vs CommonJS? ## 

I dont know

 ##  Explain why the following doesn't work as an IIFE: ## 
  An `IIFE` stands for `Immediately invoking function expression`.
 `function foo(){ }();`

   It wouldn't work because the compiler thinks it is a *function declaration## rather  ###than a *function expression*

   ### What needs to be changed to properly make it an IIFE? ###

  Put brackets around the function so that the compiler treats it as an expression, not a declaration.

  Example of it working:

  ```js
  (function foo(){ console.log('go!');})();
  ```

## What's the difference between a variable that is: `null`, `undefined` or undeclared? ##

  `null` is an object. You can use when creating variables when you don't have a value yet.

 `undefined` is a type. It is when a variable does not exist. All assigned (no value assigned to it yet) variables have a value of undefined.

`undeclared` means the variable was declared without the `var` keyword, e.g. `cheese = 2;` It is in the global scope.


  ### How would you go about checking for any of these states? ###

  You could check if it is null with `cheese === null`
  You can check if its undefined by going `typeOf(cheese) === 'undefined'` (typeOf always returns a string)
  I DONT KNOW HOW TO CHECK FOR UNDECLARED

## What is a closure, and how/why would you use one? ##

A closure is a function that contains another function. The other function knows the vars of the one its in, but they are private. NO¬

## Can you describe the main difference between a `forEach` loop and a `.map()` loop and why you would pick one versus the other? ##

A map is more suited if you want to create a copy of the thing but modified by a function.

## What's a typical use case for anonymous functions? ##

In a callback?

## How do you organize your code? (module pattern, classical inheritance? ##

I dont know :(

## What's the difference between host objects and native objects? ###

Nope

## Difference between: `function Person(){}`, `var person = Person()`, and `var person = new Person()`?

`function Person(){}` is a function declaration
`var person = Person()` is an expression, and when run it will take the value returned from Person and assign to person
`var person = new Person()` assigns a new object instance to the variable person

## What's the difference between `.call` and `.apply`? ###

dunno fam

## Explain `Function.prototype.bind`. ###

Changes the value of this to be that of the parents.

## What's the difference between feature detection, feature inference, and using the UA  ###string?
## Explain Ajax in as much detail as possible. ###

AJAX stands for Asyncronous javascript and xml

Its used for loading in a resource
You can make a request and wait for it to come back, and then execute a call back when its done

## What are the advantages and disadvantages of using Ajax? ###
## Explain how JSONP works (and how it's not really Ajax). ###
## Have you ever used JavaScript templating? ###
   ### If so, what libraries have you used? ###

   I use template strings yes..


## Explain "hoisting". ###

Hoisting is where a function declarations are loaded before any code is executed. so even if the function is called above where it sits in the code, it will still work because it is stored in memory. therefore it is like the function declaration has been `hoisted` to the top of the file

## Describe event bubbling. ###

Where events, like clicks, bubble up from child to parent and so on. Like an onclick in a dom for example?

## What's the difference between an "attribute" and a "property"? ###

i thought an attribute was like in HTML where <a class="attribute"> but a property is something that a javascript object or class can have, which can be accessed with dot notation.

## Why is extending built-in JavaScript objects not a good idea? ###

Because you might break everything?

## Difference between document load event and document DOMContentLoaded event? ###
## What is the difference between `==` and `===`? ###
## Explain the same-origin policy with regards to JavaScript. ###
## Make this work: ###
```javascript
duplicate([1,2,3,4,5]); // [1,2,3,4,5,1,2,3,4,5]
```
## Why is it called a Ternary operator, what does the word "Ternary" indicate? ###

Ternary means theres's 3 parts to it.

## What is `"use strict";`? what are the advantages and disadvantages to using it? ###


* Create a for loop that iterates up to `100` while outputting **"fizz"** at multiples of `3`, **"buzz"** at multiples of `5` and **"fizzbuzz"** at multiples of `3` and `5`
* Why is it, in general, a good idea to leave the global scope of a website as-is and never touch it?


## Why would you use something like the `load` event? Does this event have  ###disadvantages? Do you know any alternatives, and why would you use those?
## Explain what a single page app is and how to make one SEO-friendly. ###
## What is the extent of your experience with Promises and/or their polyfills? ###
## What are the pros and cons of using Promises instead of callbacks? ###
## What are some of the advantages/disadvantages of writing JavaScript code in a  ###language that compiles to JavaScript?
## What tools and techniques do you use debugging JavaScript code? ###
## What language constructions do you use for iterating over object properties and  ###array items?
## Explain the difference between mutable and immutable objects. ###
   ### What is an example of an immutable object in JavaScript? ###
   ### What are the pros and cons of immutability? ###
   ### How can you achieve immutability in your own code? ###
## Explain the difference between synchronous and asynchronous functions. ###
## What is event loop? ###
   ### What is the difference between call stack and task queue? ###
## Explain the differences on the usage of `foo` between `function foo() {}` and `var  ###foo = function() {}`
## What are the differences between variables created using `let`, `var` or `const`? ###
## What are the differences between ES6 class and ES5 function constructors? ###
## Can you offer a use case for the new arrow `=>` function syntax? How does this new  ###syntax differ from other functions?
## What advantage is there for using the arrow syntax for a method in a constructor? ###
## What is the definition of a higher-order function? ###
## Can you give an example for destructuring an object or an array? ###
## ES6 Template Literals offer a lot of flexibility in generating strings, can you give  ###an example?
## Can you give an example of a curry function and why this syntax offers an advantage? ###
## What are the benefits of using `spread syntax` and how is it different from `rest  ###syntax`?
## How can you share code between files? ###
## Why you might want to create static class members? ###
