### Chapter 7: State Management in React

- **Introduction to State in React**:  
  State is a built-in object in React that allows components to maintain and manage their own data. Unlike props, which are passed from parent to child components, state is local to the component and can change over time. When the state of a component changes, React re-renders the component to reflect the new state.

  Here’s a simple example of a component with state:

  ```typescript
  import React from 'react';

  const Counter: React.FC = () => {
    // State is initialized to 0
    const [count, setCount] = React.useState(0);

    return (
      <div>
        <p>Current Count: {count}</p>
        <button onClick={() => setCount(count + 1)}>Increment</button>
      </div>
    );
  };

  export default Counter;
  ```

- **Using the useState Hook for State Management**:  
  The `useState` hook is a special function that allows you to add state to functional components. It returns an array with two elements: the current state value and a function to update that state.

  Here’s how to use the `useState` hook:

  1. **Import the Hook**: Import `useState` from React.
  2. **Initialize State**: Call `useState` with the initial state value. It returns an array containing the current state and a function to update it.
  3. **Update State**: Use the updater function to change the state. When the state is updated, the component re-renders to reflect the new state.

  In the `Counter` example:
  - `const [count, setCount] = React.useState(0);` initializes the state variable `count` to `0`.
  - `setCount(count + 1)` updates the state when the button is clicked, incrementing the count by 1.

Using state effectively allows you to create dynamic and interactive components in your React applications.