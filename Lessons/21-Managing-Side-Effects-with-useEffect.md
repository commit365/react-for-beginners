### Chapter 21: Managing Side Effects with `useEffect`

- **Understanding the `useEffect` Hook**:  
  The `useEffect` hook is a fundamental part of React's functional components, allowing you to perform side effects in your components. Side effects can include data fetching, subscriptions, timers, and manually changing the DOM. The `useEffect` hook runs after the render phase and can be configured to run on specific conditions, making it a powerful tool for managing component behavior.

  The basic syntax of `useEffect` is as follows:

  ```typescript
  useEffect(() => {
    // Your side effect code here
    return () => {
      // Cleanup code (optional)
    };
  }, [dependencies]);
  ```

  - The first argument is a function that contains the side effect logic.
  - The second argument is an array of dependencies. The effect will run after the initial render and whenever any of the dependencies change. If the array is empty, the effect runs only once when the component mounts.

- **Managing Side Effects in Functional Components**:  
  Here’s how to use the `useEffect` hook to manage side effects in a functional component.

  1. **Fetching Data**:  
     You can use `useEffect` to fetch data when the component mounts:

     ```typescript
     import React, { useEffect, useState } from 'react';

     interface User {
       id: number;
       name: string;
       email: string;
     }

     const UserList: React.FC = () => {
       const [users, setUsers] = useState<User[]>([]);
       const [loading, setLoading] = useState<boolean>(true);
       const [error, setError] = useState<string | null>(null);

       useEffect(() => {
         const fetchUsers = async () => {
           try {
             const response = await fetch('https://jsonplaceholder.typicode.com/users');
             if (!response.ok) {
               throw new Error('Network response was not ok');
             }
             const data: User[] = await response.json();
             setUsers(data);
           } catch (error) {
             setError(error instanceof Error ? error.message : 'An error occurred');
           } finally {
             setLoading(false);
           }
         };

         fetchUsers();
       }, []); // Empty dependency array means this runs once when the component mounts

       if (loading) return <div>Loading...</div>;
       if (error) return <div>Error: {error}</div>;

       return (
         <ul>
           {users.map(user => (
             <li key={user.id}>
               {user.name} - {user.email}
             </li>
           ))}
         </ul>
       );
     };

     export default UserList;
     ```

     In this example:
     - The `fetchUsers` function is called inside `useEffect`, which runs once when the component mounts.
     - The loading state and error handling are managed within the effect.

  2. **Setting Up Subscriptions**:  
     You can also use `useEffect` to set up subscriptions or event listeners. Here’s an example of adding and cleaning up an event listener:

     ```typescript
     import React, { useEffect, useState } from 'react';

     const WindowSize: React.FC = () => {
       const [windowSize, setWindowSize] = useState({ width: window.innerWidth, height: window.innerHeight });

       useEffect(() => {
         const handleResize = () => {
           setWindowSize({ width: window.innerWidth, height: window.innerHeight });
         };

         window.addEventListener('resize', handleResize);

         // Cleanup function to remove the event listener
         return () => {
           window.removeEventListener('resize', handleResize);
         };
       }, []); // Empty dependency array ensures this runs once on mount

       return (
         <div>
           <h1>Window Size</h1>
           <p>Width: {windowSize.width}px</p>
           <p>Height: {windowSize.height}px</p>
         </div>
       );
     };

     export default WindowSize;
     ```

     In this example:
     - The `handleResize` function updates the state with the current window size whenever the window is resized.
     - The cleanup function removes the event listener when the component unmounts or before the effect runs again.

By effectively using the `useEffect` hook, you can manage side effects in your functional components, ensuring that your application behaves as expected while maintaining a clean and organized code structure.

[Next: 22-Performance-Optimization-Techniques](22-Performance-Optimization-Techniques.md)