### Chapter 15: Custom Hooks in React

- **Understanding the Purpose of Custom Hooks**:  
  Custom hooks in React allow you to extract and reuse logic across multiple components. They provide a way to encapsulate stateful logic and side effects, making your components cleaner and more focused on rendering. Custom hooks follow the naming convention of starting with the word "use" (e.g., `useFetch`, `useForm`) and can use other hooks internally. This promotes code reusability and helps keep your components DRY (Don't Repeat Yourself).

- **Creating and Using Custom Hooks for Shared Logic**:  
  Here’s how to create a custom hook and use it in a component.

  1. **Create a Custom Hook**:  
     Let's create a custom hook called `useCounter` that manages a simple counter.

     ```typescript
     import { useState } from 'react';

     const useCounter = (initialValue: number = 0) => {
       const [count, setCount] = useState(initialValue);

       const increment = () => setCount(count + 1);
       const decrement = () => setCount(count - 1);
       const reset = () => setCount(initialValue);

       return { count, increment, decrement, reset };
     };

     export default useCounter;
     ```

     In this custom hook:
     - We define a state variable `count` and provide functions to increment, decrement, and reset the counter.
     - The hook returns the current count and the functions for use in components.

  2. **Using the Custom Hook in a Component**:  
     Now, let’s use the `useCounter` hook in a functional component.

     ```typescript
     import React from 'react';
     import useCounter from './useCounter';

     const CounterComponent: React.FC = () => {
       const { count, increment, decrement, reset } = useCounter(0);

       return (
         <div>
           <h1>Count: {count}</h1>
           <button onClick={increment}>Increment</button>
           <button onClick={decrement}>Decrement</button>
           <button onClick={reset}>Reset</button>
         </div>
       );
     };

     export default CounterComponent;
     ```

     In this `CounterComponent`:
     - We call the `useCounter` hook to get the current count and the control functions.
     - The component renders the count and buttons to increment, decrement, and reset the counter.

By creating and using custom hooks, you can encapsulate complex logic and share it across multiple components, leading to cleaner, more maintainable code in your React applications.

[Next: 16-TypeScript-Generics-in-React](16-TypeScript-Generics-in-React.md)