* An `IIFE` stands for `Immediately invoking function expression`.
* A `function declaration` is a where the line begins with `function`, e.g. 
`function cheese() {}`. It is loaded by the compiler (like all declarations) before any any code is executed, so you can call the function on line 1, even if its declared on line 2. This is because of `function hoisting`
* A `function expression` is where it is assigned to a variable like `const cheese = function (){}` (anonymous function expression) or `const ham = function ham (){}` (named function expression). Must be called in a line after it is defined.
* A `variable` is a storage location that contains a value.
* `null` is an object. You can use when creating variables when you don't have a value yet.
* `undefined` is a type. It is when a variable does not exist. All assigned (no value assigned to it yet) variables have a value of undefined.
* `undeclared` means the variable was declared without the `var` keyword, e.g. `cheese = 2;` It is in the global scope.
* `AJAX` Asyncronous javascript and xml
* The `Promise` object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.
* There is a way to reduce functions of more than one argument to functions of one argument, a way called `currying` after Haskell B. Curry.