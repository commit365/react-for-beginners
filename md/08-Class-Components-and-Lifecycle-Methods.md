### Chapter 8: Class Components and Lifecycle Methods

- **Creating Class Components**:  
  Class components are a way to define components in React using ES6 class syntax. They can hold and manage their own state and have access to lifecycle methods. Here’s how to create a simple class component:

  ```typescript
  import React, { Component } from 'react';

  interface CounterProps {
    initialCount?: number; // Optional prop
  }

  interface CounterState {
    count: number;
  }

  class Counter extends Component<CounterProps, CounterState> {
    constructor(props: CounterProps) {
      super(props);
      // Initialize state
      this.state = {
        count: props.initialCount || 0, // Default to 0 if no initialCount is provided
      };
    }

    render() {
      return (
        <div>
          <p>Current Count: {this.state.count}</p>
          <button onClick={() => this.setState({ count: this.state.count + 1 })}>
            Increment
          </button>
        </div>
      );
    }
  }

  export default Counter;
  ```

  In this example:
  - We define a `Counter` class component that extends `React.Component`.
  - The component has props of type `CounterProps` and state of type `CounterState`.
  - The constructor initializes the state using the `initialCount` prop.

- **Understanding Lifecycle Methods and Their Use Cases**:  
  Lifecycle methods are special methods in class components that allow you to run code at specific points in a component's lifecycle. Here are some key lifecycle methods:

  - **componentDidMount**: Invoked immediately after a component is mounted. This is a good place to initiate API calls or set up subscriptions.
    ```typescript
    componentDidMount() {
      console.log('Component has mounted.');
    }
    ```

  - **componentDidUpdate**: Invoked immediately after updating occurs. This method can be used to respond to prop or state changes.
    ```typescript
    componentDidUpdate(prevProps: CounterProps, prevState: CounterState) {
      if (prevState.count !== this.state.count) {
        console.log('Count has changed:', this.state.count);
      }
    }
    ```

  - **componentWillUnmount**: Invoked immediately before a component is unmounted and destroyed. This is where you can clean up resources, like canceling network requests or removing event listeners.
    ```typescript
    componentWillUnmount() {
      console.log('Component will unmount.');
    }
    ```

By understanding how to create class components and utilize lifecycle methods, you can effectively manage the behavior and state of your React applications, especially when dealing with complex interactions and data fetching.