
![[JS runtime pro.png]]

# 1. Parsing
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


# 2. Execution Context
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
  - Created each time a **function is called**.
  - Whenever we call a function it will get a brand new context / scope of its own.
  - Includes `local variables`, `arguments`, `this`, and a `reference` to the outer environment.
	  1. **Local Variables**:
        - Local variables are accessible only within the function's scope and cannot be accessed from outside the function.
	   2. **Arguments**:
        - Function arguments can be accessed either through the `arguments` object (applicable in non-strict mode) or directly via named parameters declared within the function.
       3. **`this` Binding**:
	        - `this` defines where and how the function is being called. The value of `this` varies according to the context in which the function is being called.
	        - Its value depends on how the function is called:
		        - <font color="#00b050">In non-method functions (regular functions)</font>, `this` refers to the  `window` / `global` object in non-strict mode.
		        - <font color="#00b050">In strict mode</font>, `this` is `undefined` if the function is not called inside another function.
		        - <font color="#00b050">In method functions (functions defined as object properties)</font>, `this` refers to the object that owns the method when the method is called.
		
	   4. **Reference to the Outer Environment**: This refers to the lexical scope in which the function was declared. It allows functions to access variables from their containing (outer) scope, even after the outer function has finished execution.


---


# 3. Execution Phase ( 2 phases)
- ##### Creation Phase
  - **Global Object Setup**: During this phase, JavaScript sets up global variables and functions that are declared in the code. This includes allocating memory for these variables and functions.
  - **Hoisting**: Variables and functions are declared throughout the code but are not yet initialized with values. Instead, JavaScript hoists (moves) these declarations to the top of their respective scopes during compilation.
    ```javascript
    console.log(x); // undefined
    var x = 5;
    console.log(x); // 5
    ```

- #####  Execution Phase
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


---


# 4. JavaScript Engine (**V8 and others**)
### Call Stack
  - <span style="background:rgba(5, 117, 197, 0.2)">The call stack keeps track of the execution context of functions in JavaScript and follows the Last In, First Out (LIFO) principle.</span>
  - <span style="background:rgba(240, 200, 0, 0.2)">Primitive values (e.g., numbers, strings, Booleans, null, undefined) are stored directly in the call stack.</span>
  - <span style="background:rgba(5, 117, 197, 0.2)">When a function is called, it is added to the top of the stack, and the interpreter executes the function at the top.</span>
  - <span style="background:rgba(240, 200, 0, 0.2)">Functions are removed from the stack when they complete execution.</span>

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
- <span style="background:rgba(5, 117, 197, 0.2)">The heap is where JavaScript allocates memory for objects and complex data structures like arrays.</span>
- <span style="background:rgba(240, 200, 0, 0.2)">Memory allocation in the heap is less structured compared to the call stack, allowing for more flexible storage.</span>
- <span style="background:rgba(5, 117, 197, 0.2)">When you create an object or array, JavaScript allocates memory in the heap and stores a reference to it in the call stack.</span>

    ```javascript
    let obj = { name: "John", age: 30 };
    ```

##### Garbage Collection
  - JavaScript uses garbage collection to manage memory automatically.
  - When there are no more references to an object or data stored in the heap, JavaScript marks that memory as no longer needed.
  - Periodically, the garbage collector runs to identify and reclaim unused memory, freeing up space in the heap for new allocations.

    ```javascript
    let obj = { name: "John" };
    obj = null; // 'obj' is eligible for garbage collection.
    ```


---


# 5. Web APIs
  - Web APIs are not technically part of the JavaScript language itself.
  - Browser-provided APIs for asynchronous tasks (<font color="#00b0f0">DOM manipulation, timers, Geolocations, fetch, Canvas, Web storage, WebSocket, Notifications, History</font>).
  - Executes tasks outside JavaScript engine.

1. **DOM (Document Object Model) API**
    - Allows interaction with and manipulation of HTML and CSS.
    - Key methods: `getElementById`, `querySelector`, `createElement`, `addEventListener`.
2. **Fetch API**
    - Modern method to make HTTP requests.
3. **Geolocation API**
    - Accesses the geographical location of the user.
4. **Canvas API**
    - Draws graphics via JavaScript and the HTML `<canvas>` element.
5. **Web Storage API**
    - Stores data on the client side with `localStorage` and `sessionStorage`.
6. **WebSocket API**
    - Opens a persistent connection for real-time communication.
7. **Notifications API**
    - Sends notifications displayed outside the browser.
8. **History API**
    - Manipulates the browser session history.

# 6. Queues ( Microtask Queue and MacroTask Queue )
   - JavaScript manages asynchronous operations using two types of queues: the Microtask Queue and the Macrotask Queue. Understanding these queues helps in writing efficient asynchronous code.

#####      Microtask Queue
- **Purpose**: Handles tasks that need to be executed immediately after the current script execution.
- **Common Microtasks**: Promise callbacks, `process.nextTick` (Node.js).
- **Execution Order**: Microtasks are processed before any macrotasks.

  ```javascript
  Promise.resolve().then(() => console.log("Microtask"));
  ```

#####      Macrotask Queue (Task Queue)
- **Purpose**: Handles tasks that can be deferred and executed after the current script and all microtasks are completed.
- **Common Macrotasks**: `setTimeout`, `setInterval`, I/O operations.
- **Execution Order**: Macrotasks are processed after the microtask queue is empty.

  ```javascript
  setTimeout(() => console.log("Macrotask"), 2);
  ```

##### Execution Flow Example
```javascript
console.log("Script start");

setTimeout(() => {
  console.log("Macrotask 1");
}, 0);

Promise.resolve().then(() => {
  console.log("Microtask 1");
});

Promise.resolve().then(() => {
  console.log("Microtask 2");
});

setTimeout(() => {
  console.log("Macrotask 2");
}, 0);

console.log("Script end");
```
**Expected Output**:
```
Script start
Script end
Microtask 1
Microtask 2
Macrotask 1
Macrotask 2
```


---


# 7. Event Loop
- **Definition**
  - Monitors the call stack and queues.
  - Executes tasks from the queue when the call stack is empty.
  
    ```javascript
    console.log("Start");
    setTimeout(() => console.log("Timeout"), 0);
    console.log("End");
    // Output: "Start", "End", "Timeout"
    ```

- **Process**
  - Checks call stack.
  - Processes microtasks before macrotasks.
  
    ```javascript
    console.log("Start");
    setTimeout(() => console.log("Timeout"), 0);
    console.log("End");
    // Output: "Start", "End", "Timeout"
    ```

