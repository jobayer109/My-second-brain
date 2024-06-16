# JS Code Execution Process

## 1. Parsing
- **Lexical Analysis (Tokenization)**
  - Converts source code into tokens (keywords, identifiers, operators).
  - Example:
    ```javascript
    let x = 10;
    // Tokens: [let, x, =, 10, ;]
    ```

- **Syntactic Analysis (Parsing)**
  - Converts tokens into an Abstract Syntax Tree (AST).
  - Example:
    ```plaintext
    Program
    ├── VariableDeclaration
    │   └── VariableDeclarator
    │       ├── Identifier: x
    │       └── NumericLiteral: 10
    ```

## 2. Execution Context
- **Global Execution Context**
  - Created <font color="#ffff00">before</font> any code is executed.
  - Includes global object 
	  - `window` in browsers, `global` in Node.js, 
	  - `scope chain` and 
	  - `this` binding.
    ```javascript
    let x = 10;
    function foo() {
      console.log("Hello");
    }
    foo();
    ```
  
- **Function Execution Context**
  - Created each time a function is called.
  - Includes local variables, arguments, `this`, and a reference to the outer environment.
  - Example:
    ```javascript
    function multiply(a, b) {
      let result = a * b;
      return result;
    }
    let product = multiply(3, 4);
    ```

## 3. Execution Phase
- **Creation Phase**
  - **Global Object Setup**: Sets up global variables and functions.
  - **Hoisting**: Variables are declared but not initialized until runtime.
  - Example:
    ```javascript
    console.log(x); // undefined
    var x = 5;
    console.log(x); // 5
    ```

- **Execution Phase**
  - Executes code line by line within function contexts.
  - Manages the call stack and updates variable values.
  - Example:
    ```javascript
    function foo() {
      console.log("Hello");
    }
    foo(); // Output: "Hello"
    ```

## 4. Call Stack
- **Definition**
  - A stack data structure that stores function calls.
  - Follows Last In, First Out (LIFO) principle.
  - Example:
    ```javascript
    function first() {
      console.log("First");
      second();
    }
    function second() {
      console.log("Second");
    }
    first(); // Output: "First", "Second"
    // Call Stack: [first()] -> [first(), second()] -> [first()] -> []
    ```

## 5. Memory Heap
- **Definition**
  - Allocates memory for variables and objects.
  - Handles memory allocation and deallocation.
  - Example:
    ```javascript
    let obj = { name: "John", age: 30 };
    ```

- **Garbage Collection**
  - Automatically frees memory no longer in use.
  - Uses algorithms like Mark-and-Sweep.
  - Example:
    ```javascript
    let obj = { name: "John" };
    obj = null; // 'obj' is eligible for garbage collection.
    ```

## 6. Web APIs
- **Definition**
  - Browser-provided APIs for asynchronous tasks (DOM manipulation, timers).
  - Executes tasks outside JavaScript engine.
  - Example:
    ```javascript
    setTimeout(() => {
      console.log("Timeout");
    }, 1000);
    ```

## 7. Queues (Microtask Queue and Macrotask Queue)
- **Microtask Queue**
  - Stores microtasks (Promise callbacks, `process.nextTick`).
  - Executes before the next macrotask.
  - Example:
    ```javascript
    Promise.resolve().then(() => console.log("Microtask"));
    ```

- **Macrotask Queue (Task Queue)**
  - Stores macrotasks (setTimeout, setInterval, I/O operations).
  - Executes after the microtask queue is empty.
  - Example:
    ```javascript
    setTimeout(() => console.log("Macrotask"), 0);
    ```

## 8. Event Loop
- **Definition**
  - Monitors the call stack and queues.
  - Executes tasks from the queue when the call stack is empty.
  - Example:
    ```javascript
    console.log("Start");
    setTimeout(() => console.log("Timeout"), 0);
    console.log("End");
    // Output: "Start", "End", "Timeout"
    ```

- **Process**
  - Checks call stack.
  - Processes microtasks before macrotasks.
  - Example:
    ```javascript
    console.log("Start");
    setTimeout(() => console.log("Timeout"), 0);
    console.log("End");
    // Output: "Start", "End", "Timeout"
    ```

### Complete Example
```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Microtask");
});

console.log("End");
