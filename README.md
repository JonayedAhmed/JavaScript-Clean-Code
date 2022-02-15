# JavaScript Clean Code

## Table of Contents

1. [Variables](#1.variables)
2. [Functions](#functions)
3. [Conditionals](#conditionals)
4. [ES Classes](#es-Classes)
5. [Avoid Using Eval](#avoid-using-eval)
6. [Objects and Data Structures](#objects-and-data-structures)
7. [Template Literals](#template-literals)
8. [Avoid Callbacks](#avoid-callbacks)
9. [Comments](#comments)
10. [Reference](#reference)


## Variables
It is a good coding practice to put all declarations at the top of each script or function. We should try to provide a single place to look for local variables 
and reduce the possibility of unwanted re-declarations.
### Keywords

We can declare variables in JS using three keywords:
- var (most commonly used keyword to declare a variable. Variables declared without var keyword works as a global variable. Works as private variable if declared inside a function)
- const (used while using a constant value which may not change further)
- let (used when there is high change of changing the value continuously)

### Meaningful Variable

- It's good practice to declare meaningful, pronounceable and searchable names as variables. 
- It’s better to use explanatory variables and use camelCase for variable and function names.
- We should Try to use the same type of vocabulary for similar functions and variables.(getUseInfo(), getClientData(), getCustomerRecord() => getUserInfo())

### Use Default argument 

This will help to get less error as faulty value or null or NaN will not replace default value in the second scenario.

**Bad:**

```javascript
function createMicrobrewery(name) {
  const breweryName = name || "Hipster Brew Co.";
  // ...
}
```

**Good**

```javascript
function createMicrobrewery(name = "Hipster Brew Co.") {
  // ...
}
```

**[⬆ back to top](#table-of-contents)**

## Functions

### Function Arguments

- We should try to use minimum arguments. It’s best to use 2 arguments as standard. 
- We should try to make an object of all the information and pass them as a single argument.

### In General About Function

- Function should do only one thing (either answer something or do something but not both). So, we should try to avoid conditional if possible.
- Function names must match what is done inside the function.
- Function should ensure reusability of code and avoid duplication.
- Favor functional programming over imperative programming.
- Avoid negative conditioning.
- Skip Over optimization.

### Encapsulate Conditionals
**Bad:**
```javascript
if (fsm.state === "fetching" && isEmpty(listNode)) {
  // ...
}
```
**Good:**
```javascript
function shouldShowSpinner(fsm, listNode) {
  return fsm.state === "fetching" && isEmpty(listNode);
}

if (shouldShowSpinner(fsmInstance, listNodeInstance)) {
  // ...
}
```

### Avoid Flags

It's better to avoid flag names because it's telling that a method is doing more than one task.

**Bad:**
```javascript
function createFile(name, isPublic) {
  if (isPublic) {
    fs.create(`./public/${name}`);
  } else {
    fs.create(name);
  }
}
```
**Good:**
```javascript
function createFile(name) {
  fs.create(name);
}

function createPublicFile(name) {
  createFile(`./public/${name}`);
}
```

### Global Pollution

We should try not to pollute the globals i.e try to extend existing object using ES6 classes or inheritance, instead of creating the function on the prototype chain of the native object.

**Bad**
```javascript
Array.prototype.myFunction = function myFunction() {
 // implementation
};
```

**Good**
```javascript
class SuperArray extends Array {
 myFunc() {
   // implementation
 }
}
```

**[⬆ back to top](#table-of-contents)**

## Conditionals

### Type Checking

Since JS is untyped it’s better to avoid type checking. If Type checking is done it’s better to use strong type check === instead of using ==

### Conditional shorthand

**Bad**
```javascript
if (isValid === true) {
  // do something...
}
if (isValid === false) {
  // do something...
}
```

**Good**
```javascript
if (isValid) {
  // do something...
}
if (!isValid) {
  // do something...
}
```

**[⬆ back to top](#table-of-contents)**

## ES Classes

- Preferable to use 2015 class / ES6 over ES5.
- Try to use method chaining.

**[⬆ back to top](#table-of-contents)**

## Avoid Using Eval

Eval function should be avoided as it's not safe and it opens a potential thread vector for miscellaneous programmers.

**Bad**
```javascript
var x = 100
var userInput =  "1.573*Math.pow(10,-10)*Math.pow(x,3) - 2.558*Math.pow(10,-07)*Math.pow(x,2) + 1.375*Math.pow(10,-04)*x - 2.166*Math.pow(10,-02)"
console.log(eval(userInput))
```

**Good**
```javascript
var x = 100
var userInput =  "1.573*Math.pow(10,-10)*Math.pow(x,3) - 2.558*Math.pow(10,-07)*Math.pow(x,2) + 1.375*Math.pow(10,-04)*x - 2.166*Math.pow(10,-02)"
userInput = userInput.replace(/x/g, x)

let result = Function("return " + userInput)(); 
console.log(result)
```

**[⬆ back to top](#table-of-contents)**

## Objects and Data Structures
- It's better to use getters and setters (helps in encapsulation, makes adding validation simple, easy to add logging and error handling)
- We should try to make the object have private members (Can be achieved with ES5)
- Composition is more prefer over inheritance

### Don't Use new Object()
- Use **""** instead of **new String()**
- Use **0** instead of **new Number()**
- Use **false** instead of **new Boolean()**
- Use **{}** instead of **new Object()**
- Use **[]** instead of **new Array()**
- Use **/()/** instead of **new RegExp()**
- Use **function (){}** instead of **new Function()**

**[⬆ back to top](#table-of-contents)**

## Template Literals

Back tickles ` ` is an easy way for concatenation and we can define a placeholder ${} in to set any value inside that string.

**Bad**
```javascript
var name = 'Peter';
var message = 'Hi'+ name + ',';
```

**Good**
```javascript
var name = 'Peter';
var message = `Hi ${name},`
```

**[⬆ back to top](#table-of-contents)**

## Avoid Callbacks
It is a popular way of handling asynchronous methods in JS but it becomes very complicated as the code starts to grow and there are multiple nested callbacks.

**Bad**
```javascript
const makeBurger = nextStep => {
  getBeef(function (beef) {
    cookBeef(beef, function (cookedBeef) {
      getBuns(function (buns) {
        putBeefBetweenBuns(buns, cookedBeef, function(burger) {
          // nextStep(burger)
        })
      })
    })
  })
}

// Make and serve the burger
makeBurger(function (burger) {
  serve(burger)
})
```


**Good 1**
```javascript
const makeBurger = () => {
  return getBeef()
    .then(beef => cookBeef(beef))
    .then(cookedBeef => getBuns(cookedBeef))
    .then(bunsAndBeef => putBeefBetweenBuns(bunsAndBeef))
}

// Make and serve burger
makeBurger()
  .then(burger => serve(burger))
```

**Good 2**

We can take advantage of the single-argument style with promises and make the functions look more readable.

```javascript
const makeBurger = () => {
  return getBeef()
    .then(cookBeef)
    .then(getBuns)
    .then(putBeefBetweenBuns)
}

// Make and serve burger
makeBurger()
  .then(serve)
```

**[⬆ back to top](#table-of-contents)**


## Comments

- We should Avoid Unnecessary comments and try not make it redundant and too descriptive.
- It should be used just as a clarification of code.
- Commented out code should be removed from codebase.

**[⬆ back to top](#table-of-contents)**

## Reference:
1. [Clean Code Javascript Github](https://github.com/ryanmcdermott/clean-code-javascript)
2. [Writing Clean Code](https://blog.bitsrc.io/writing-clean-code-in-javascript-dd584bbe1874)
3. [Clean Code Best Practices](https://javascript.plainenglish.io/javascript-clean-code-best-practices-461c24c53cae)
4. [JavaScript Variables](https://www.tutorialsteacher.com/javascript/javascript-variable#:~:text=Variable%20means%20anything%20that%20can,declare%20a%20variable%20in%20JavaScript.)
5. [Difference of var let and const](https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/)
6. [SOLID](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#single-responsibility-principle)
7. [Nested Callbacks](https://zellwk.com/blog/nested-callbacks/)

**[⬆ back to top](#table-of-contents)**
