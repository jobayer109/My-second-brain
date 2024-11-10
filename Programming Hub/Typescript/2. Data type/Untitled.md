**Any (super type)**
    - built in types: number, string, boolean, void, null, undefined, never
    - user-defined types: Arrays, Enums, Classes, interfaces etc.
    - for avoiding typescript in entire file: `// @ts-nocheck`

In TypeScript, you can use basic types to specify the type of variables, function parameters, and return values. Here are some of the basic types in TypeScript:

1. **number**: Represents both integer and floating-point numbers.
    
    ```ts
    let age: number = 25;
    let price: number = 9.99;
    ```
    
2. **string**: Represents a sequence of characters.
    
    ```ts
    let name: string = 'John';
    ```
    
3. **boolean**: Represents a true or false value.
    
    ```ts
    let isDone: boolean = false;
    ```
    
4. **any**: Represents a dynamic or untyped value. Avoid using this when possible, as it bypasses type checking. if you have no knowledge about the variable type use any type: user input values
    
    ```ts
    let data: any = 42;
    data = 'Hello';
    
    let password: any;
    let passwords: any[];
    ```
    
5. **void**: Represents the absence of a value, typically used as the return type of functions that don't return anything.
    
    ```ts
    function logMessage(): void {
      console.log('This is a log message.');
    }
    ```
    
6. **null** and **undefined**: Represent null and undefined values, respectively.
    
    ```ts
    let n: null = null;
    let u: undefined = undefined;
    ```
    
7. **never**: Represents a value that never occurs, such as a function that throws an error or an infinite loop.
    
    ```ts
    function throwError(message: string): never {
      throw new Error(message);
    }
    ```
    

These basic types provide a foundation for specifying the types of variables and data in TypeScript. You can use them to ensure type safety in your code and catch type-related errors at compile time.

- inferred Typing
    
    ```js
    let userName = 'anis'; // data type inferred as string
    ```
    