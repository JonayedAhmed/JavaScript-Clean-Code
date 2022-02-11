# JavaScript-Clean-Code

## 1. Variables

### 1.1 Keywords

We can declare variables in JS using three keywords:
- var (most commonly used keyword to declare a variable. Available globally if declared outside the function and works as local variable if declared inside a function)
- const (used while using a constant value which may not change further)
- let (used when there is high change of changing the value continuously)

### 1.2 Meaningful Variable

- It's good practice to declare meaningful, pronounceable and searchable names as variables. 
- It’s better to use explanatory variables and use camelCase for variable and function names.
- Try to use the same type of vocabulary for similar functions and variables.(getUseInfo(), getClientData(), getCustomerRecord() => getUserInfo())

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

- Try using minimum arguments. It’s best to use 2 arguments as standard. 
- Make an object of all the information and pass them as a single argument.

### 2.2 In General About Function

- Function should do only one thing (either answer something or do something but not both). So, Avoid conditional if possible.
- Function names must match what is done inside the function.
- Function should ensure reusability of code and avoid duplication.
- Favor functional programming over imperative programming.
- Avoid negative conditioning
- Skip Over optimization.
- 

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

Try not to pollute the globals i.e if it's necessary to extend existing object use ES6 classes or inheritance instead of creating the function on the prototype chain of the native object.

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

Since JS is untypes it’s better to avoid type checking. If Type checking is done it’s better to use strong type check === instead of using ==

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

### 4.1 General Suggestions 

- Prefer 2015 class / ES6 over ES5
- Try to use method chaining

## 5. Avoid Using Eval

Trying to avoid eval function should be avoided as it's not safe and it opens a potential thread vector for miscellaneous programmers.

## 6. Objects & Data Structures
- Use getters and setters (helps in encapsulation, makes adding validation simple, easy to add logging and error handling)
- Make the object have private members (Can be achieved with ES5)
- Prefer composition over inheritance


## 7. User Template Literals for Concatenation

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


## 9. SOLID

This is the convention that should be taken to consideration most for clean code. Since this needs a detail understanding.
[Solid] https://github.com/ryanmcdermott/clean-code-javascript#solid


## 10. Comments

- Avoid Unnecessary comments. Don’t make it redundant and too descriptive.
- Use as a clarification of code.
- Remove commented out code from codebase.


## Reference:
1. https://github.com/ryanmcdermott/clean-code-javascript
2. https://blog.bitsrc.io/writing-clean-code-in-javascript-dd584bbe1874
3. https://javascript.plainenglish.io/javascript-clean-code-best-practices-461c24c53cae
4. https://www.tutorialsteacher.com/javascript/javascript-variable#:~:text=Variable%20means%20anything%20that%20can,declare%20a%20variable%20in%20JavaScript.
5. https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/
