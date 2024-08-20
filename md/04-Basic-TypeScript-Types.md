### Chapter 4: Basic TypeScript Types

- **Primitive Types**:  
  TypeScript provides several basic types to represent simple values. The three most commonly used primitive types are:
  - **String**: Represents textual data. You can define a string type using single or double quotes.
    ```typescript
    let name: string = "Alice";
    ```
  - **Number**: Represents numeric values, including integers and floating-point numbers.
    ```typescript
    let age: number = 30;
    ```
  - **Boolean**: Represents a logical value that can be either `true` or `false`.
    ```typescript
    let isActive: boolean = true;
    ```

- **Arrays, Tuples, and Objects**:  
  TypeScript also allows you to define more complex types such as arrays, tuples, and objects.

  - **Arrays**: You can define an array type by specifying the type of its elements followed by `[]`.
    ```typescript
    let scores: number[] = [90, 85, 88];
    let names: string[] = ["Alice", "Bob", "Charlie"];
    ```

  - **Tuples**: A tuple is a fixed-length array where each element can have a different type. You define a tuple by specifying the types of each element in square brackets.
    ```typescript
    let person: [string, number] = ["Alice", 30]; // [name, age]
    ```

  - **Objects**: You can define an object type by specifying the shape of the object using an interface or inline type definition.
    ```typescript
    interface User {
      name: string;
      age: number;
      isActive: boolean;
    }

    let user: User = {
      name: "Alice",
      age: 30,
      isActive: true,
    };
    ```

Understanding these basic types is essential for effectively using TypeScript in your React applications, as they help ensure type safety and improve code clarity.