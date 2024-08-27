### Chapter 26: Working with TypeScript and React Router

- **Introduction to React Router for Navigation**:  
  React Router is a powerful library for managing navigation and routing in React applications. It allows you to create single-page applications with multiple views, enabling users to navigate between different components seamlessly without reloading the page. Here’s a brief overview of how to set up and use React Router:

  1. **Installation**:  
     To get started, you need to install React Router. If you’re using React Router v6, you can install it using npm:

     ```bash
     npm install react-router-dom
     ```

  2. **Basic Setup**:  
     After installing, you can set up routing in your application. Here’s a simple example:

     ```typescript
     import React from 'react';
     import { BrowserRouter as Router, Route, Routes, Link } from 'react-router-dom';

     const Home: React.FC = () => <h2>Home Page</h2>;
     const About: React.FC = () => <h2>About Page</h2>;
     const NotFound: React.FC = () => <h2>404 Not Found</h2>;

     const App: React.FC = () => {
       return (
         <Router>
           <nav>
             <ul>
               <li>
                 <Link to="/">Home</Link>
               </li>
               <li>
                 <Link to="/about">About</Link>
               </li>
             </ul>
           </nav>

           <Routes>
             <Route path="/" element={<Home />} />
             <Route path="/about" element={<About />} />
             <Route path="*" element={<NotFound />} />
           </Routes>
         </Router>
       );
     };

     export default App;
     ```

     In this example:
     - The `BrowserRouter` component wraps the application to enable routing.
     - The `Link` component is used to create navigation links.
     - The `Routes` component contains `Route` elements that define the paths and corresponding components.

- **TypeScript Integration with React Router**:  
  Integrating TypeScript with React Router enhances type safety and autocompletion, making it easier to manage routes and their parameters. Here’s how to work with TypeScript in React Router:

  1. **Defining Route Parameters**:  
     You can define routes with parameters and access them using the `useParams` hook. Here’s an example of a route with a parameter:

     ```typescript
     import React from 'react';
     import { BrowserRouter as Router, Route, Routes, Link, useParams } from 'react-router-dom';

     const UserProfile: React.FC = () => {
       const { userId } = useParams<{ userId: string }>();
       return <h2>User Profile for User ID: {userId}</h2>;
     };

     const App: React.FC = () => {
       return (
         <Router>
           <nav>
             <ul>
               <li>
                 <Link to="/">Home</Link>
               </li>
               <li>
                 <Link to="/user/1">User 1</Link>
               </li>
               <li>
                 <Link to="/user/2">User 2</Link>
               </li>
             </ul>
           </nav>

           <Routes>
             <Route path="/" element={<Home />} />
             <Route path="/user/:userId" element={<UserProfile />} />
           </Routes>
         </Router>
       );
     };

     export default App;
     ```

     In this example:
     - The `UserProfile` component uses the `useParams` hook to extract the `userId` parameter from the URL.
     - The route is defined with a parameter using the syntax `:userId`.

  2. **Type Safety for Route Props**:  
     If you have components that need to receive props from routes, you can define the types for those props as follows:

     ```typescript
     interface UserProfileProps {
       userId: string;
     }

     const UserProfile: React.FC<UserProfileProps> = ({ userId }) => {
       return <h2>User Profile for User ID: {userId}</h2>;
     };

     const App: React.FC = () => {
       return (
         <Router>
           <Routes>
             <Route path="/user/:userId" element={<UserProfile userId="1" />} />
           </Routes>
         </Router>
       );
     };
     ```

     In this case, you would pass the `userId` prop directly to the `UserProfile` component. However, when using `useParams`, you typically extract the parameter directly from the URL.

  3. **Redirects and Nested Routes**:  
     You can also handle redirects and nested routes using TypeScript. Here’s an example of a nested route:

     ```typescript
     const Dashboard: React.FC = () => {
       return (
         <div>
           <h2>Dashboard</h2>
           <Routes>
             <Route path="stats" element={<Stats />} />
             <Route path="reports" element={<Reports />} />
           </Routes>
         </div>
       );
     };

     const App: React.FC = () => {
       return (
         <Router>
           <Routes>
             <Route path="/dashboard/*" element={<Dashboard />} />
           </Routes>
         </Router>
       );
     };
     ```

By integrating TypeScript with React Router, you can create a robust and type-safe navigation system in your React applications, enhancing both developer experience and application reliability. This setup allows you to manage routes, parameters, and navigation effectively while leveraging TypeScript's type-checking capabilities.

[Next: 27-State-Management-with-Redux](27-State-Management-with-Redux.md)