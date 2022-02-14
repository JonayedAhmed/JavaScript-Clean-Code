# JavaScript-Clean-Code 

## Table of Contents

1. [Variables](#variables)
2. [Functions](#functions)
3. [Conditionals](#conditionals)
4. [ES Classes](#es-Classes)
5. [Avoid Using Eval](#avoid-using-eval)
6. [Objects and Data Structures](#objects-and-data-structures)
7. [Template Literals](#template-literals)
8. [Avoid Callbacks](#avoid-callbacks)
9. [SOLID](#solid)
10. [10. Comments](#10.-comments)
11. [Reference](#reference)


## 1. Variables

### 1.1 Keywords

We can declare variables in JS using three keywords:
- var (most commonly used keyword to declare a variable. Available globally if declared outside the function and works as local variable if declared inside a function)
- const (used while using a constant value which may not change further)
- let (used when there is high change of changing the value continuously)

### 1.2 Meaningful Variable

- It's good practice to declare meaningful, pronounceable and searchable names as variables. 
- It’s better to use explanatory variables and use camelCase for variable and function names.
- We should Try to use the same type of vocabulary for similar functions and variables.(getUseInfo(), getClientData(), getCustomerRecord() => getUserInfo())

### 1.3 Use Default argument 

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

## 2. Functions

### 2.1 Function Arguments

- We should try to use minimum arguments. It’s best to use 2 arguments as standard. 
- We should try to make an object of all the information and pass them as a single argument.

### 2.2 In General About Function

- Function should do only one thing (either answer something or do something but not both). So, we should try to avoid conditional if possible.
- Function names must match what is done inside the function.
- Function should ensure reusability of code and avoid duplication.
- Favor functional programming over imperative programming.
- Avoid negative conditioning.
- Skip Over optimization.

### 2.3 Encapsulate Conditionals
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

### 2.4 Avoid Flags

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

### 2.5 Global Pollution

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

## 3. Conditionals

### 3.1 Type Checking

Since JS is untyped it’s better to avoid type checking. If Type checking is done it’s better to use strong type check === instead of using ==

### 3.2 Conditional shorthand

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

## 4. ES Classes

- Preferable to use 2015 class / ES6 over ES5.
- Try to use method chaining.

## 5. Avoid Using Eval

Eval function should be avoided as it's not safe and it opens a potential thread vector for miscellaneous programmers.

## 6. Objects and Data Structures
- It's better to use getters and setters (helps in encapsulation, makes adding validation simple, easy to add logging and error handling)
- We should try to make the object have private members (Can be achieved with ES5)
- Composition is more prefer over inheritance


## 7. Template Literals

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

## 8. Avoid Callbacks
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


## 9. SOLID

A good design pattern makes a software system felixible. Without a good design pattern software becomes rigid and fragile. The SOLID design pattern was introduced 
to solve these problems. 
  
  - **S** - Single-responsiblity Principle
  - **O** - Open-closed Principle
  - **L** - Liskov Substitution Principle
  - **I** - Interface Segregation Principle
  - **D** - Dependency Inversion Principle


## 10. Comments

- We should Avoid Unnecessary comments and try not make it redundant and too descriptive.
- It should be used just as a clarification of code.
- Commented out code should be removed from codebase.


## Reference:
1. https://github.com/ryanmcdermott/clean-code-javascript
2. https://blog.bitsrc.io/writing-clean-code-in-javascript-dd584bbe1874
3. https://javascript.plainenglish.io/javascript-clean-code-best-practices-461c24c53cae
4. https://www.tutorialsteacher.com/javascript/javascript-variable#:~:text=Variable%20means%20anything%20that%20can,declare%20a%20variable%20in%20JavaScript.
5. https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/
6. https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#single-responsibility-principle
7. https://zellwk.com/blog/nested-callbacks/
