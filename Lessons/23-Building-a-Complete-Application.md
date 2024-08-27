### Chapter 23: Building a Complete Application

- **Project Setup and Architecture for a Full Application**:  
  Building a complete application involves careful planning and organization. Here’s a step-by-step guide to setting up your project and defining its architecture:

  1. **Create a New React Project**:  
     Use Create React App to quickly set up a new project with TypeScript support.

     ```bash
     npx create-react-app my-app --template typescript
     cd my-app
     ```

  2. **Project Structure**:  
     Organize your project files for maintainability. A common structure might look like this:

     ```
     my-app/
     ├── public/
     ├── src/
     │   ├── components/      # Reusable components
     │   ├── hooks/           # Custom hooks
     │   ├── pages/           # Page components
     │   ├── context/         # Context API files
     │   ├── services/        # API calls and services
     │   ├── styles/          # CSS or styled components
     │   ├── App.tsx          # Main application component
     │   ├── index.tsx        # Entry point
     ├── package.json
     └── tsconfig.json
     ```

  3. **Routing Setup**:  
     Use `react-router-dom` for navigation between different pages in your application. Install it using:

     ```bash
     npm install react-router-dom
     ```

     Set up your routes in `App.tsx`:

     ```typescript
     import React from 'react';
     import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
     import Home from './pages/Home';
     import About from './pages/About';
     import NotFound from './pages/NotFound';

     const App: React.FC = () => {
       return (
         <Router>
           <Switch>
             <Route path="/" exact component={Home} />
             <Route path="/about" component={About} />
             <Route component={NotFound} />
           </Switch>
         </Router>
       );
     };

     export default App;
     ```

- **Integrating Learned Concepts into a Cohesive Project**:  
  Now that you have your project set up, it’s time to integrate the concepts you’ve learned throughout this guide into a cohesive application.

  1. **State Management with Context API**:  
     Use the Context API to manage global state. Create a context file in the `context` directory:

     ```typescript
     import React, { createContext, useState, ReactNode } from 'react';

     interface AppContextType {
       user: string;
       setUser: (user: string) => void;
     }

     export const AppContext = createContext<AppContextType | undefined>(undefined);

     export const AppProvider: React.FC<{ children: ReactNode }> = ({ children }) => {
       const [user, setUser] = useState<string>('Guest');

       return (
         <AppContext.Provider value={{ user, setUser }}>
           {children}
         </AppContext.Provider>
       );
     };
     ```

     Wrap your application in the `AppProvider` in `index.tsx`:

     ```typescript
     import React from 'react';
     import ReactDOM from 'react-dom';
     import App from './App';
     import { AppProvider } from './context/AppContext';

     ReactDOM.render(
       <AppProvider>
         <App />
       </AppProvider>,
       document.getElementById('root')
     );
     ```

  2. **Fetching Data with Hooks**:  
     Create a custom hook for fetching data from an API in the `hooks` directory:

     ```typescript
     import { useEffect, useState } from 'react';

     const useFetch = (url: string) => {
       const [data, setData] = useState<any[]>([]);
       const [loading, setLoading] = useState<boolean>(true);
       const [error, setError] = useState<string | null>(null);

       useEffect(() => {
         const fetchData = async () => {
           try {
             const response = await fetch(url);
             if (!response.ok) throw new Error('Network response was not ok');
             const result = await response.json();
             setData(result);
           } catch (error) {
             setError(error instanceof Error ? error.message : 'An error occurred');
           } finally {
             setLoading(false);
           }
         };

         fetchData();
       }, [url]);

       return { data, loading, error };
     };

     export default useFetch;
     ```

     Use this hook in your page components to fetch and display data.

  3. **Testing Your Application**:  
     Write tests for your components and hooks using Jest and React Testing Library to ensure everything works as expected.

  4. **Styling Your Application**:  
     Use CSS modules, styled-components, or any preferred styling method to style your components.

By following these steps, you can integrate all the concepts you've learned into a complete React application. This approach not only reinforces your understanding but also prepares you to build real-world applications using React and TypeScript.

[Next: 24-Deploying-React-Applications](24-Deploying-React-Applications.md)