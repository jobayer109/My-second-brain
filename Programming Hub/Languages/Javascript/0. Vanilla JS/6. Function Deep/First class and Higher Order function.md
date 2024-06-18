![[First class vs Higher order.png]]




# First-Class Functions

- **Treated as first-class citizens**.

- **Assigning functions to variables**: 

  ```javascript
  const greet = function(name) {
      console.log(`Hello, ${name}!`);
  };
  ```

- **Passing functions as arguments**: 

  ```javascript
  function callFunction(func) {
      func('Alice');
  }

  callFunction(greet); // Output: Hello, Alice!
  ```

- **Returning functions**: 

  ```javascript
  function createGreeting() {
      return function(name) {
          console.log(`Hello, ${name}!`);
      };
  }

  const greetFunction = createGreeting();
  greetFunction('Bob'); // Output: Hello, Bob!
  ```

- **Storing functions in data structures**: 

  ```javascript
  const functionArray = [greet, function(name) { console.log(`Hola, ${name}!`); }];
  functionArray[1]('Carl'); // Output: Hola, Carl!
  ```

---

# Higher-Order Functions

**Higher-order functions** are functions that either:
- Take one or more functions as arguments (like `callFunction` in the example above).
- Return a function as their result (like `createGreeting`).

Sure! Let's create a JavaScript example demonstrating higher-order functions that take one or more functions as arguments and return a function as their result.

### Example

#### 1. Higher-order function that takes functions as arguments

```javascript
function callFunctions(...funcs) {
    return function(...args) {
        return funcs.map(func => func(...args));
    };
}

// Functions to be passed as arguments
function add(a, b) {
    return a + b;
}

function multiply(a, b) {
    return a * b;
}

// Using callFunctions
const combinedFunction = callFunctions(add, multiply);

// Calling the returned function
const result = combinedFunction(3, 4);
console.log(result); // Output: [7, 12]
```



---
