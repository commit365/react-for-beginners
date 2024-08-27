### Chapter 14: Context API for State Management

- **Introduction to the Context API**:  
  The Context API in React provides a way to share values (like state) between components without having to pass props manually at every level of the component tree. This is especially useful for global state management, such as user authentication, theme settings, or language preferences. The Context API consists of two main components: `React.createContext()` and the `Provider` component.

- **Creating a Global State with Context and `useContext` Hook**:  
  To create a global state using the Context API, follow these steps:

  1. **Create a Context**:
     First, create a context using `React.createContext()`. This will be used to provide and consume the global state.

     ```typescript
     import React, { createContext, useState, ReactNode } from 'react';

     interface AppContextType {
       user: string;
       setUser: (user: string) => void;
     }

     export const AppContext = createContext<AppContextType | undefined>(undefined);
     ```

  2. **Create a Provider Component**:
     Next, create a provider component that will hold the global state and provide it to its children.

     ```typescript
     const AppProvider: React.FC<{ children: ReactNode }> = ({ children }) => {
       const [user, setUser] = useState<string>('Guest');

       return (
         <AppContext.Provider value={{ user, setUser }}>
           {children}
         </AppContext.Provider>
       );
     };

     export default AppProvider;
     ```

  3. **Wrap Your Application with the Provider**:
     Use the provider component to wrap your application, allowing any child component to access the context.

     ```typescript
     import React from 'react';
     import ReactDOM from 'react-dom';
     import App from './App';
     import AppProvider from './AppProvider';

     ReactDOM.render(
       <AppProvider>
         <App />
       </AppProvider>,
       document.getElementById('root')
     );
     ```

  4. **Consume the Context in Child Components**:
     Finally, use the `useContext` hook to access the global state in any child component.

     ```typescript
     import React, { useContext } from 'react';
     import { AppContext } from './AppProvider';

     const UserProfile: React.FC = () => {
       const context = useContext(AppContext);

       if (!context) {
         throw new Error('UserProfile must be used within an AppProvider');
       }

       const { user, setUser } = context;

       return (
         <div>
           <h1>User: {user}</h1>
           <button onClick={() => setUser('Alice')}>Set User to Alice</button>
         </div>
       );
     };

     export default UserProfile;
     ```

In this example:
- The `AppContext` is created to hold a global user state.
- The `AppProvider` component maintains the user state and provides it to its children through the `Provider`.
- The `UserProfile` component consumes the context using the `useContext` hook, allowing it to read and update the user state.

By using the Context API for state management, you can easily share data across your React application without the need for prop drilling, making your code cleaner and more maintainable.

[Next: 15-Custom-Hooks-in-React](15-Custom-Hooks-in-React.md)