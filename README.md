# JavaScript-Clean-Code

## Variables

### Keywords

We can declare variables in JS using three keywords:
- var (most commonly used keyword to declare a variable. Available globally if declared outside the function and works as local variable if declared inside a function)
- const (used while using a constant value which may not change further)
- let (used when there is high change of changing the value continuously)

### Meaningful Variable

- It's good practice to declare meaningful, pronounceable and searchable names as variables. 
- It’s better to use explanatory variables and use camelCase for variable and function names.
- Try to use the same type of vocabulary for similar functions and variables.(getUseInfo(), getClientData(), getCustomerRecord() => getUserInfo())

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


