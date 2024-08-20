### Chapter 25: Advanced Patterns in React

- **Understanding Higher-Order Components (HOCs)**:  
  Higher-order components (HOCs) are a powerful pattern in React that allow you to reuse component logic. An HOC is a function that takes a component as an argument and returns a new component with enhanced functionality. HOCs are often used for cross-cutting concerns, such as authentication, data fetching, or logging.

  Here’s a simple example of an HOC that adds loading functionality to a component:

  ```typescript
  import React, { ComponentType } from 'react';

  // HOC that adds loading functionality
  const withLoading = <P extends object>(WrappedComponent: ComponentType<P>) => {
    return (props: P & { isLoading: boolean }) => {
      if (props.isLoading) {
        return <div>Loading...</div>;
      }
      return <WrappedComponent {...props} />;
    };
  };

  // Example usage of the HOC
  interface UserProps {
    name: string;
  }

  const User: React.FC<UserProps> = ({ name }) => {
    return <div>User: {name}</div>;
  };

  const UserWithLoading = withLoading(User);

  // Usage in a component
  const App: React.FC = () => {
    const isLoading = true; // Simulate loading state

    return <UserWithLoading name="Alice" isLoading={isLoading} />;
  };

  export default App;
  ```

  In this example:
  - The `withLoading` HOC takes a component (`WrappedComponent`) and returns a new component that conditionally renders a loading message or the wrapped component based on the `isLoading` prop.

- **Render Props and Compound Components**:  
  Render props is another advanced pattern that allows you to share code between components using a prop that is a function. This function returns a React element and can be used to pass data and behavior to the child component.

  Here’s an example of the render props pattern:

  ```typescript
  import React, { useState } from 'react';

  interface ToggleProps {
    children: (isToggled: boolean, toggle: () => void) => React.ReactNode;
  }

  const Toggle: React.FC<ToggleProps> = ({ children }) => {
    const [isToggled, setIsToggled] = useState(false);

    const toggle = () => {
      setIsToggled(prev => !prev);
    };

    return <>{children(isToggled, toggle)}</>;
  };

  // Usage of the Toggle component with render props
  const App: React.FC = () => {
    return (
      <Toggle>
        {(isToggled, toggle) => (
          <div>
            <button onClick={toggle}>
              {isToggled ? 'Hide' : 'Show'} Content
            </button>
            {isToggled && <div>This is the toggled content!</div>}
          </div>
        )}
      </Toggle>
    );
  };

  export default App;
  ```

  In this example:
  - The `Toggle` component uses the render props pattern to provide the toggling functionality to its children.
  - The `children` prop is a function that receives the current toggle state and the toggle function, allowing the parent component to control the rendering based on the state.

  **Compound Components**:  
  Compound components are another advanced pattern where a parent component manages state and allows child components to communicate with it. This pattern is useful for creating flexible and reusable components.

  Here’s a simple example of compound components:

  ```typescript
  import React, { useState } from 'react';

  interface TabsProps {
    children: React.ReactNode;
  }

  const Tabs: React.FC<TabsProps> = ({ children }) => {
    const [activeIndex, setActiveIndex] = useState(0);

    const handleTabClick = (index: number) => {
      setActiveIndex(index);
    };

    return (
      <div>
        <div className="tab-titles">
          {React.Children.map(children, (child, index) =>
            React.cloneElement(child as React.ReactElement<any>, {
              isActive: index === activeIndex,
              onClick: () => handleTabClick(index),
            })
          )}
        </div>
        <div className="tab-content">
          {React.Children.toArray(children)[activeIndex]}
        </div>
      </div>
    );
  };

  interface TabProps {
    isActive: boolean;
    onClick: () => void;
    children: React.ReactNode;
  }

  const Tab: React.FC<TabProps> = ({ isActive, onClick, children }) => {
    return (
      <button onClick={onClick} style={{ fontWeight: isActive ? 'bold' : 'normal' }}>
        {children}
      </button>
    );
  };

  // Usage of Tabs and Tab components
  const App: React.FC = () => {
    return (
      <Tabs>
        <Tab>Tab 1</Tab>
        <Tab>Tab 2</Tab>
        <Tab>Tab 3</Tab>
      </Tabs>
    );
  };

  export default App;
  ```

  In this example:
  - The `Tabs` component manages the active tab state and renders the appropriate content based on the selected tab.
  - The `Tab` component receives props from the parent to determine its active state and handle clicks.

By understanding and implementing higher-order components, render props, and compound components, you can create more flexible and reusable React components that enhance the functionality and maintainability of your applications.