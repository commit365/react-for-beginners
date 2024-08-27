### Chapter 6: Creating Your First React Component

- **Building a Simple Functional Component**:  
  In React, a functional component is a JavaScript function that returns JSX. Here’s how to create a simple functional component:

  ```typescript
  import React from 'react';

  const Greeting: React.FC<{ name: string }> = ({ name }) => {
    return <h1>Hello, {name}!</h1>;
  };

  export default Greeting;
  ```

  In this example:
  - We import React to use JSX.
  - The `Greeting` component takes a `name` prop of type `string` and returns an `<h1>` element displaying a greeting message.

- **Understanding Props and Default Props**:  
  Props (short for properties) are used to pass data from a parent component to a child component. You can define the types of props using TypeScript interfaces or inline type annotations.

  - **Using Props**: Here’s how to use the `Greeting` component and pass a prop to it:

  ```typescript
  import React from 'react';
  import Greeting from './Greeting';

  const App: React.FC = () => {
    return (
      <div>
        <Greeting name="Alice" />
      </div>
    );
  };

  export default App;
  ```

  - **Default Props**: You can define default values for props using the `defaultProps` property. This is useful when you want to provide fallback values if no props are passed.

  ```typescript
  Greeting.defaultProps = {
    name: 'Guest',
  };
  ```

  In this example, if the `name` prop is not provided when using the `Greeting` component, it will default to "Guest".

By understanding how to create functional components and work with props, you can build reusable UI elements in your React applications.

[Next: 07-State-Management-in-React](07-State-Management-in-React.md)