# JavaScript Runtime

## 1. Parsing
- **Lexical Analysis (Tokenization)**
  - Converts source code into tokens (keywords, identifiers, operators).
    ```javascript
    let x = 10;
    // Tokens: [let, x, =, 10, ;]
    ```

- **Syntactic Analysis (Parsing)**
  - Converts tokens into an Abstract Syntax Tree (AST).
    ```plaintext
    Program
    ├── VariableDeclaration
    │   └── VariableDeclarator
    │       ├── Identifier: x
    │       └── NumericLiteral: 10
    ```

---

## 2. Execution Context
- #### Global Execution Context
  -  Default execution context is either `window` or, `Global`
  - Whenever we declare anything in `global` / `window` scope is automatically attached with the  `global` / `window` object.
  - Created before any code is executed.
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
  
- #### Function Execution Context
  - Created each time a ***function is called***.
  - Whenever we call a function it will get a brand new context / scope of its own.
  - Includes `local variables`, `arguments`, `this`, and a `reference` to the outer environment.
	  1. **Local Variables**:
        - Local variables are accessible only within the function's scope and cannot be accessed from outside the function.
	   2. **Arguments**:
        - Function arguments can be accessed either through the `arguments` object (applicable in non-strict mode) or directly via named parameters declared within the function.
       3. **`this` Binding**:
		- `this` এর মাধ্যমে ফাংশন কোথায় ও কীভাবে কল হচ্ছে তা নির্ধারণ করা হয়। ফাংশন যে কনটেক্সটে কল হচ্ছে, সে কনটেক্সটের অনুসারে `this` এর মান পরিবর্তিত হয়।
		- Its value depends on how the function is called:
		    - <font color="#00b050">In non-method functions (regular functions)</font>, `this` refers to the  `window` / `global` object in non-strict mode.
			- <font color="#00b050">In strict mode</font>, `this` is `undefined` if the function is not called inside another function.
			- <font color="#00b050">In method functions (functions defined as object properties)</font>, `this` refers to the object that owns the method when the method is called.
	   4. **Reference to the Outer Environment**: This refers to the lexical scope in which the function was declared. It allows functions to access variables from their containing (outer) scope, even after the outer function has finished execution.
	   
    ```javascript
    function multiply(a, b) {
      let result = a * b;
      return result;
    }
    let product = multiply(3, 4);
    ```

---

## 3. Execution Phase ( 2 phases)
- **Creation Phase**
  - **Global Object Setup**: During this phase, JavaScript sets up global variables and functions that are declared in the code. This includes allocating memory for these variables and functions.
  - **Hoisting**: Variables and functions are declared throughout the code but are not yet initialized with values. Instead, JavaScript hoists (moves) these declarations to the top of their respective scopes during compilation.
    ```javascript
    console.log(x); // undefined
    var x = 5;
    console.log(x); // 5
    ```

- **Execution Phase**
  After the Creation Phase in JavaScript's execution, the program moves on to the Execution Phase. Here’s what happens during the Execution Phase:

	1. **Initialization of Variables and Functions**:
        - During the Execution Phase, variables are initialized (assigned values) and functions are executed.
       
	1. **Top-to-Bottom Execution**:
        - JavaScript executes the code line by line from top to bottom. This includes evaluating expressions, invoking functions, and assigning values to variables.

    3. **Function Calls and Stack Management**:
        - When a function is called, a new function execution context is created and pushed onto the Call Stack. This context includes local variables, arguments, and a reference to the outer environment (lexical scope).
    ```javascript
    function foo() {
      console.log("Hello");
    }
    foo(); // Output: "Hello"
    ```


## 4. JavaScript Engine (V8)
### Call Stack
- **Definition**
  - The call stack keeps track of the execution context of functions in JavaScript.
  - Follows Last In, First Out (LIFO) principle.
  - When a function is called, it is added to the top of the stack.
  - The interpreter executes the function at the top of the stack.
  - Functions are removed from the stack when they complete execution.
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

### Heap Memory
- **Definition**
  - Allocates memory for variables and objects.
  - Handles memory allocation and deallocation.
  - Example:
    ```javascript
    let obj = { name: "John", age: 30 };
    ```

- **Garbage Collection**
  - When JavaScript no longer has any references to a particular object or data stored in the heap, it considers that memory as no longer needed. Periodically, the garbage collector runs to identify such unused memory (garbage) and reclaim it, freeing up space in the heap for new allocations.
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

## Complete Example
```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Microtask");
});

console.log("End");
