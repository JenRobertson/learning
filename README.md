# JS Questions:

## Explain event delegation ##

Event delegation is what allows a parent element to have an event listener attached to it. The children inside it will also listen for the event, and pass it back up to the parent. The exact child which triggered the event can be found by looking inside `e.target`.

""The event is dispatched to its target  EventTarget and any event listeners found there are triggered. Bubbling events will then trigger any additional event listeners found by following the EventTarget's parent chain upward, checking for any event listeners registered on each successive EventTarget. This upward propagation will continue up to and including the Document.""

----
## Explain how `this` works in JavaScript ## 

`this` is different depending on its *context*

**Global context**
(If in a browser), `this` refers to the window. (global in node)
```js
a = 10;
this.a //=== 10
```

**Function context**

*Bind*

If you call bind on a function, passing in an argument, you will be able to access the variable passed in as this.


```js
function hello() {
	console.log(this);
	console.log(this.a);
}

hello();//Window, undefined

hello = hello.bind({a: "hello"});

hello();//{a: "hello"},hello
```
*call and apply*
Do the same thing as bind but you dont have to save them as a function, you just call it.
```js
hello.call({a: "hello"});

hello.apply({a: "helloapply"});
```
Apply uses arrays, call you have to count:

```js
function add(c, d) {
  return this.a + this.b + c + d;
}

var o = {a: 1, b: 3};

// The first parameter is the object to use as
// 'this', subsequent parameters are passed as 
// arguments in the function call
add.call(o, 5, 7); // 16

// The first parameter is the object to use as
// 'this', the second is an array whose
// members are used as the arguments in the function call
add.apply(o, [10, 20]); // 34
```
*Arrow functions*
`this` refers to the enclosing lexical context's `this`

**Object context**

A function called on an object (e.g. `myObject.getHeight()`) `this` will refer to the properties of that object.

----

## Explain how prototypal inheritance works ## 

A prototype is a template for something. If you inherit from a prototype, you get all of its methods and properties

Every object has a prototype property. If something is called on it but it doesnt have it, it will look into its prototype / parent for it. This keeps objects nice and light.

-----

 ##  Explain why the following doesn't work as an IIFE: ## 
  An `IIFE` stands for `Immediately invoking function expression`.
 `function foo(){ }();`

   It wouldn't work because the compiler thinks it is a *function declaration* rather  than a *function expression*

   ### What needs to be changed to properly make it an IIFE? ###

  Put brackets around the function so that the compiler treats it as an expression, not a declaration.

  Example of it working:

  ```js
  (function foo(){ console.log('go!');})();
  ```

----

## What's the difference between a variable that is: `null`, `undefined` or undeclared? ##

  `null` is an object. You can use when creating variables when you don't have a value yet.

 `undefined` is a type. All unassigned (no value assigned to it yet) variables have a value of undefined.

`undeclared` means the variable was declared without the `var` keyword, e.g. `cheese = 2;` It is in the global scope.

```js
var a;//undefined
var b = null;//null
```
  ### How would you go about checking for any of these states? ###

  You could check if it is null with `cheese === null`
  You can check if its undefined by going `typeOf(cheese) === 'undefined'` (typeOf always returns a string)
  I DONT KNOW HOW TO CHECK FOR UNDECLARED

-----

## What is a closure, and how/why would you use one? ##

A closure is a function that contains another function. The other function knows the vars of the one its in, but they are private. 

```js
const hello = 'hello!';
function makeFamilyMembersSurname (surname) {
	return function (forename) {
  	console.log(forename + " " + surname);
  }
}
const robertsonMaker = makeFamilyMembersSurname("robertson");
robertsonMaker("jenny");
/* 
console.dir(robertsonMaker); */

function privateThing() {
	var secret = 'secret thing';
	return {
  	getSecret: () => {
    	console.log('getting ' + secret);
    },
    setSecret: (newthing) => {
    	secret=newthing;
    }
  }
}

const myObject = privateThing();

myObject.getSecret();
myObject.setSecret('newthing');
myObject.getSecret();

```

## Can you describe the main difference between a `forEach` loop and a `.map()` loop and why you would pick one versus the other? ##

A map is more suited if you want to create a copy of the thing but modified by a function.

------

## What's a typical use case for anonymous functions? ##

You can use an anonymous function as a callback, as it does not need a name. e.g.

```js
thing.addEventListener('click', function () {
  console.log('click!');
});
```

------

## How do you organize your code? (module pattern, classical inheritance? ##

I dont know :(

------

## What's the difference between host objects and native objects? ###

Both terms are defined in the ECMAScript specification:

native object
object in an ECMAScript implementation whose semantics are fully defined by this specification rather than by the host environment.

NOTE Standard native objects are defined in this specification. Some native objects are built-in; others may be constructed during the course of execution of an ECMAScript program.

Source: http://es5.github.com/#x4.3.6

host object
object supplied by the host environment to complete the execution environment of ECMAScript.

NOTE Any object that is not native is a host object.

Source: http://es5.github.com/#x4.3.8

A few examples:

Native objects: Object (constructor), Date, Math, parseInt, eval, string methods like indexOf and replace, array methods, ...

Host objects (assuming browser environment): window, document, location, history, XMLHttpRequest, setTimeout, getElementsByTagName, querySelectorAll, ...

------
## Difference between: `function Person(){}`, `var person = Person()`, and `var person = new Person()`?

`function Person(){}` is a function declaration
`var person = Person()` is an expression, and when run it will take the value returned from Person and assign to person
`var person = new Person()` assigns a new object instance to the variable person

e.g.

```js
function cheese () {
	this.colour = 'yellow';
	this.smell = 'bad';
}

const two = new cheese();
//this refers to object which called the function, so they are added to two.
console.log(window.smell);//undefined
console.log(two.smell);//bad

const one = cheese();
//this refers to object which called the function, so window. so its added to window.
console.log(window.smell);//bad
console.log(one.smell);//Cannot read property 'smell' of undefined
```
----

## What's the difference between `.call` and `.apply`? ###

Call and apply are both used to call a function, providing it a new object to use as 'this'.

*call* uses commas for its function params C --> comma

(The apply() method calls a function with a given this value, and arguments provided as an array)

*apply* uses arrays for its function params A --> array

```js
hello = 'window';
function pie (name, username) {
	console.log(name + username + ' ' + this.hello);
}

const myObject = {
	hello: 'objects hello'
}

pie("jenny", "jangles");// jennyjangles window
pie.call(myObject, "jenny", "jangles");//jennyjangles objects hello
pie.apply(myObject, ["jenny", "jangles"]);//jennyjangles objects hello
```

---

## Explain `Function.prototype.bind`. ###

Creates a new function for which 'this' is the passed in parameter. So its like 'call' and 'apply', but it just makes a new function and doesnt call it.

SO you can do call and apply without calling the function at the same time!

```js

hello = 'window';
function pie (name, username) {
	console.log(name + username + ' ' + this.hello);
}

const myObject = {
	hello: 'objects hello'
}

pie("jenny", "jangles");// jennyjangles window
pie.call(myObject, "jenny", "jangles");//jennyjangles objects hello
pie.apply(myObject, ["jenny", "jangles"]);//jennyjangles objects hello

pie.bind(myObject);
pie("glum", "burger");

```

---

## What's the difference between feature detection, feature inference, and using the UA string?

UA means user agent string. It tells you which browser you're in.

Feature detection is where you detect if a feature exists explicity,
Feature inference is where you assume a feature exists based on other things, e.g. if I don't have this feature I must be in IE.



---

## Explain Ajax in as much detail as possible. ###

AJAX stands for Asyncronous javascript and xml

Its used for loading in a resource
You can make a request and wait for it to come back, and then execute a call back when its done


## What are the advantages and disadvantages of using Ajax? ###
## Explain how JSONP works (and how it's not really Ajax). ###

----

## Have you ever used JavaScript templating? ###
   ### If so, what libraries have you used? ###

   I use template strings yes..

----

## Explain "hoisting". ###

Hoisting is where a function declarations are loaded before any code is executed. so even if the function is called above where it sits in the code, it will still work because it is stored in memory. therefore it is like the function declaration has been `hoisted` to the top of the file

----

## Describe event bubbling. ###

Where events, like clicks, bubble up from child to parent and so on. Like an onclick in a dom for example. It comes after event delegation, which is where the event is delegated down to the children of a parent.

----

## What's the difference between an "attribute" and a "property"? ###

i thought an attribute was like in HTML where `<a class="attribute">` but a property is something that a javascript object or class can have, which can be accessed with dot notation.

---

## Why is extending built-in JavaScript objects not a good idea? ##

if, in future, a browser decides to implement its own version of your method, your method might get overridden (silently) and the browser’s implementation (which is probably different from yours) would take over. So not extending in the first place is future proofing your code.

On the flip side, if you decide to overwrite the browsers definition, any future developer working on your code won’t know about the change. They'll have a harder time getting up to speed.

---

## Difference between document load event and document DOMContentLoaded event? ###

document *DOMContentLoaded event* is when the initial HTML document has been completely loaded and parsed, *without* waiting for stylesheets, images, and subframes to finish loading

*load* is fired when a resource and its dependent resources have finished loading.

---

## What is the difference between `==` and `===`? ###

`==` will try and convert one type into another type to see if they match, but `===` will not. (checks types)

---

## Explain the same-origin policy with regards to JavaScript. ###

Resources can only be loaded in from what javascript considers to be the 'same' site. It decides it with 3 checks:
* must be same protocol (http vs https)
* must be the same domain and subdomain (blog.jennyrobertson.net is different to jennyrobertson.net)
* must be the same port number

You can get around by setting a domain on the document:

```js
// in the code on subdomain.yoursite.com
document.domain = "yoursite.com";
```
http://lucybain.com/blog/2014/same-origin-policy/

---

## Make this work: ###
```javascript
duplicate([1,2,3,4,5]); // [1,2,3,4,5,1,2,3,4,5]
```

```js
function duplicate(inputArray){
  let duplicatedArray = inputArray;
  inputArray.forEach((element) => {
    duplicatedArray.push(element);
  });
  return duplicatedArray;
}
console.log(duplicate([1,2,3,4,5]));
```
---

## Why is it called a Ternary operator, what does the word "Ternary" indicate? ###

Ternary means theres's 3 parts to it.

---

## What is `"use strict";`? what are the advantages and disadvantages to using it? ##

Use strict turns on strict mode (evaluates the page in strict mode), and it prevents you from creating global variables. This is good because global variables might clash with any other scripts which are running in the same page. 

It gets rid of some 'unadvisable' javascript features, makes more errors and ensures your code is more robust, readable, and accurate.

Disadvantages are:  If a developer used a library that was in strict mode, but the developer was used to working in normal mode, they might call some actions on the library that wouldn’t work as expected.

---

## Create a for loop that iterates up to `100` while outputting **"fizz"** at multiples of `3`, **"buzz"** at multiples of `5` and **"fizzbuzz"** at multiples of `3` and `5` ##


```js
for (let i=0; i<=100; i++){
	let message = '';

  if (i%3 === 0){
    message+='fizz';
  }
  if (i%5 === 0){
    message+='buzz';
  }
  if (message){
    console.log(`${i} ${message}`);
  }

}

```

---
## Why is it, in general, a good idea to leave the global scope of a website as-is and never touch it? ##

If you're writing code that uses global variables, any other script loaded into the page will have access to them. If another script used the same global variable as you, this could break the code. 

---

## Why would you use something like the `load` event? Does this event have disadvantages? Do you know any alternatives, and why would you use those?

If your javascript needs to act upon something in the dom, you need to make sure its loaded in first before you try and find it, or an error will occur.

You could use DOMContentLoad, but this fire when the dom has loaded and parsed, doesnt wait for async things like images

---

## Explain what a single page app is and how to make one SEO-friendly. ###

This is where all the 'pages' are actually controlled with javascript, rather than navigating to a separate file on the server. I dont know about SEO.

Have each page still have an h1?

---

## What is the extent of your experience with Promises and/or their polyfills? ###

The Promise object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.

I have not used a polyfill yet.

Example:

```js

const myPromise = new Promise((resolve, reject) => {
  setTimeout(resolve, 10000);
});

myPromise.then(() => {

	console.log('hello!');
  
});
```

## What are the pros and cons of using Promises instead of callbacks? ###

With a promise, you can do promise.all and promise.then.

I call back does not need a polyfill.

*Example of a callback*

```js
//making crumble
//callback hell version
function cutApples (crumbleInput, callback){
	callback(crumbleInput + ' apple', false);
}

function makeCrumble(crumbleInput, callback) {
	callback(crumbleInput + ' crumble bits', false);
}

function eatCrumble(crumbleInput, callback) {
	callback(crumbleInput + ' yum yum yum!', false);
}

cutApples("plate", function (crumbleOutput, error) {
	if(!error){
  	makeCrumble(crumbleOutput, function (crumbleOutput2, error) {
    	if(!error){
      	eatCrumble(crumbleOutput2, function (crumbleOutput3, error){
        	if(!error){
          	console.log(crumbleOutput3);
          }
        });
      }
    });
  }
});

//PROMISE VERSION

function cutApplesP (crumbleInput){
	return new Promise(function (resolve, reject){
  	resolve(crumbleInput + ' apple');
  });
}

function makeCrumbleP (crumbleInput) {
	return new Promise(function (resolve, reject){
  	resolve(crumbleInput + ' crumble bittys');
  });
}

function eatCrumbleP (crumbleInput, tvShow) {
	return new Promise(function(resolve, reject){
  	resolve(crumbleInput + ' yuuummm!');
  });
}
cutApplesP('plate').then(makeCrumbleP).then(eatCrumbleP).then(function(finishedCrumble){
	console.log(finishedCrumble);
});
```

---

## What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?

There are two obvious advantages:

You don’t have to program in JavaScript.
You can use a much better language, one that is more robust and reliable and safer. For example, Smalltalk is the best OOP language in the world. Another example, Scala is a great FP and OOP language. Then there’s Clojure and Dart.
There are three potential downsides:

It may be harder to find developers for your chosen language. JavaScript developers are dime a dozen, so it’s really easy to hire them.
You have fewer choices of tools and frameworks. JavaScript offers you overwhelming choice: dozens of frameworks that have the lifespan of a fruit fly. The current “hotness” is React, but who knows how long that’ll last.
Generated code size might be an issue (but code generation is continuing to improve).

---

## What tools and techniques do you use debugging JavaScript code? ###
I look for errors in the console.
I do console.logs.
For React and redux, I use their built in tools

---

## What language constructions do you use for iterating over object properties and array items?

```js
// array items:
array.forEach(function (){
  //stuff
});

let iterable = [10, 20, 30];

for (let value of iterable) {
  value += 1;
  console.log(value);
}

//map, reduce, filter

var i;
for (i = 0; i < cars.length; i++) { 
    text += cars[i] + "<br>";
}

//object properties:

for (var property1 in object1) {
  object1[property1];
}
```
---

## Explain the difference between mutable and immutable objects. ###
Immutable means it's value can't be changed once its set.
   ### What is an example of an immutable object in JavaScript? ###
   Examples of native JavaScript values that are immutable are numbers and strings. Examples of native JavaScript values that are mutable include objects, arrays, functions, classes, sets, and maps.

   Something with const?

   So this is like, if you have a = 1 and then you do b = a, if you change a then b wont change

   but for an object, it just makes a reference and it will change
   ### What are the pros and cons of immutability? ###

   ### How can you achieve immutability in your own code? ###

   Using const, object.assign.

   ```js
const object1 = {
  property1: 42
};

const object2 = Object.freeze(object1);

object2.property1 = 33;
// Throws an error in strict mode

console.log(object2.property1);
// expected output: 42

   ```

   ---

## Explain the difference between synchronous and asynchronous functions. ###

With synchronous code, you know that the code will not run until the line before it is finished, it is predicable and runs in order.

Asynchronous code usually is when the code goes to fetch something like an image or a timeout, and the lines after it will run, even if that code hasnt finished.

----


## What is event loop? ###
   ### What is the difference between call stack and task queue? ###

   ----

## Explain the differences on the usage of `foo` between `function foo() {}` and `var foo = function() {}`

The first one is a function definition and the second is a function expression

---

## What are the differences between variables created using `let`, `var` or `const`? ###

let is from ES6 but var is very old, so let will not work on old browsers.
let has block scope but var has function scope
let is not hoisted but var is.

You cannot re-assign a const

Example
```js
(function cheese(){
  if (true){
    console.log(varra);//undefined
    console.log(letter);//error not defined

    var varra = 2;
    let letter = 1;
  }

console.log(varra);//2
console.log(letter);//error not defined

})();
```

---

## What are the differences between ES6 class and ES5 function constructors? ####

In ES6 (ES2015) if you try to call a class constructor without `new`, it will always throw an error.

---

## Can you offer a use case for the new arrow `=>` function syntax? How does this new syntax differ from other functions?

Old functions have their own this, while arrow functions keep the this of their parent. Arrow functions also do not have an arguments variable.

```js
const mookie = {

	firstName: 'jenny',
  lastName: 'bob',
  getName: function(){
  	return this.firstName + ' ' + this.lastName;
  },
  getNameWorks: function(){
  	let addSpace = () => {
    	return this.firstName + ' ' + this.lastName;
    }
    return addSpace();
  },
  getNameNotWorks: function(){
  	let addSpace = function() {
    	return this.firstName + ' ' + this.lastName;
    }
    return addSpace();
  }

}
console.log(mookie.getName());//jenny bob
console.log(mookie.getNameWorks());//jenny bob
console.log(mookie.getNameNotWorks());// undefined undefined

```


## What advantage is there for using the arrow syntax for a method in a constructor? ###

It will keep the this of the parent, so any this.value expressions will be assigned to the parent class.

---

## What is the definition of a higher-order function? ###

A higher-order function is a function that can take another function as an argument, or that returns a function as a result.

---
## Can you give an example for destructuring an object or an array? ###
const {cheese} = objectWithCheeseIn;
const [a, b] = anArray;
## ES6 Template Literals offer a lot of flexibility in generating strings, can you give an example?

console.log(`the variable is ${thing} isnt that coooool!`);

## Can you give an example of a curry function and why this syntax offers an advantage? ###

Example:

```js


curryedMultiply = (n) => (m) => n * m
curryedMultiply(3)(4) === 12 // true

multiply = (n, m) => curryedMultiply(n)(m)
multiply(3, 4) === 12 // true

console.log(multiply(3, 4) === 12);

//my example using actual functions

mycurriedMultiply = function one (n) {
	return function two (m) {
  	return n * m;
  }
}

console.log(mycurriedMultiply(6)(7));

```
---

## What are the benefits of using `spread syntax` and how is it different from `rest syntax`?

When ... is at the end of function parameters, it’s “rest parameters” and gathers the rest of the list into the array. When ... occurs in a function call or alike, it’s called a “spread operator” and expands an array into the list.

## How can you share code between files? ###
module.exports

## Why you might want to create static class members? ###

They are only callable on the class, not an instance of the class. They are useful for utility methods.