
**Syntax:**
There are **two** common ways to write an IIFE:

1. **Using the traditional function expression**:
   ```javascript
   (function() {
       // Code to be executed immediately
   })();
   ```

2. **Using the arrow function expression (ES6+)**:
   ```javascript
   (() => {
       // Code to be executed immediately
   })();
   ```

**Key Characteristics:**
- **Encapsulation:** IIFEs help to encapsulate variables and functions within their scope, preventing them from polluting the global scope.
- **Execution:** They are executed immediately after they are created, without needing to be called separately.

### Practical Use Cases

**1. Avoiding Global Variable Pollution:**
IIFEs are useful for avoiding global variable pollution. By wrapping code in an IIFE, variables declared inside it won't be accessible from the global scope, thus preventing conflicts with other scripts.

   ```javascript
   (function() {
       var localVariable = "I am local";
       console.log(localVariable); // Output: I am local
   })();
   console.log(localVariable); // ReferenceError: localVariable is not defined
   ```

---
**2. Creating Module Pattern:**
IIFEs are often used to create modules in JavaScript. This pattern allows you to create private and public variables and methods, emulating the concept of classes and encapsulation.

   ```javascript
   var myModule = (function() {
       var privateVar = "I am private";
       var publicVar = "I am public";

       function privateMethod() {
           console.log(privateVar);
       }

       function publicMethod() {
           console.log(publicVar);
       }

       return {
           publicMethod: publicMethod
       };
   })();

   myModule.publicMethod(); // Output: I am public
   console.log(myModule.privateVar); // undefined
   ```

**3. Loop Iteration Variables:**
IIFEs are handy in loops to create a new scope for each iteration variable, avoiding unexpected behaviors caused by closures.

   ```javascript
   for (var i = 0; i < 3; i++) {
       (function(i) {
           setTimeout(function() {
               console.log(i);
           }, 1000);
       })(i);
   }
   // Output after 1 second: 0, 1, 2
   ```

**4. Initializing Code:**
IIFEs can be used to initialize code that needs to run immediately and only once.

   ```javascript
   (function() {
       console.log("Initialization code running");
       // Additional initialization code here
   })();
   // Output: Initialization code running
   ```

