### Chapter 5: Functions and Type Annotations in TypeScript

- **Defining Functions and Using Type Annotations**:  
  In TypeScript, you can define functions with type annotations to specify the types of parameters and the return type. This helps catch errors and improves code readability. Here’s how to define a function with type annotations:

  ```typescript
  function greet(name: string): string {
    return `Hello, ${name}!`;
  }

  const message = greet("Alice"); // "Hello, Alice!"
  ```

  In this example:
  - The parameter `name` is of type `string`.
  - The return type of the function is also `string`.

- **Understanding Void and Return Types**:  
  - **Void**: If a function does not return a value, you can use the `void` type as the return type. This indicates that the function is intended to perform an action but does not return anything.
    ```typescript
    function logMessage(message: string): void {
      console.log(message);
    }

    logMessage("This is a log message."); // Logs: This is a log message.
    ```

  - **Return Types**: If a function returns a value, you should specify the return type explicitly. If the return type is not specified, TypeScript will infer it based on the return statements within the function.
    ```typescript
    function add(a: number, b: number): number {
      return a + b;
    }

    const sum = add(5, 10); // sum is of type number
    ```

Using type annotations for functions helps ensure that the correct types are passed and returned, making your code more robust and easier to understand.

[Next: 06-Creating-Your-First-React-Component](06-Creating-Your-First-React-Component.md)