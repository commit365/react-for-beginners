### Chapter 28: Advanced TypeScript Features

- **Exploring Advanced TypeScript Features: Intersection Types, Union Types, and Mapped Types**:  
  TypeScript provides several advanced features that enhance type safety and flexibility in your applications. Here’s an overview of intersection types, union types, and mapped types:

  1. **Intersection Types**:  
     Intersection types allow you to combine multiple types into one. This is useful when you want to create a type that has the properties of multiple types. You can use the `&` operator to define an intersection type.

     ```typescript
     interface User {
       id: number;
       name: string;
     }

     interface Admin {
       role: string;
     }

     type AdminUser = User & Admin;

     const admin: AdminUser = {
       id: 1,
       name: 'Alice',
       role: 'Administrator',
     };
     ```

     In this example, `AdminUser` is an intersection type that combines the properties of `User` and `Admin`.

  2. **Union Types**:  
     Union types allow a variable to hold values of multiple types. You can use the `|` operator to define a union type.

     ```typescript
     type StringOrNumber = string | number;

     const value1: StringOrNumber = 'Hello';
     const value2: StringOrNumber = 42;
     ```

     In this example, `StringOrNumber` can be either a string or a number.

  3. **Mapped Types**:  
     Mapped types allow you to create new types by transforming properties of existing types. This is useful for creating variations of types based on existing structures.

     ```typescript
     interface User {
       id: number;
       name: string;
     }

     type ReadonlyUser = {
       readonly [K in keyof User]: User[K];
     };

     const user: ReadonlyUser = {
       id: 1,
       name: 'Alice',
     };

     // user.id = 2; // Error: Cannot assign to 'id' because it is a read-only property.
     ```

     In this example, `ReadonlyUser` is a mapped type that makes all properties of `User` read-only.

- **Applying Advanced Types in React Components**:  
  You can leverage these advanced TypeScript features in your React components to improve type safety and flexibility. Here are some examples:

  1. **Using Intersection Types in Props**:  
     You can define component props using intersection types to combine multiple interfaces.

     ```typescript
     interface User {
       id: number;
       name: string;
     }

     interface Profile {
       age: number;
       bio: string;
     }

     type UserProfileProps = User & Profile;

     const UserProfile: React.FC<UserProfileProps> = ({ id, name, age, bio }) => {
       return (
         <div>
           <h2>{name} (ID: {id})</h2>
           <p>Age: {age}</p>
           <p>Bio: {bio}</p>
         </div>
       );
     };

     const App: React.FC = () => {
       return (
         <UserProfile
           id={1}
           name="Alice"
           age={30}
           bio="Software Developer"
         />
       );
     };

     export default App;
     ```

  2. **Using Union Types for Props**:  
     You can use union types to allow a prop to accept multiple types.

     ```typescript
     interface ButtonProps {
       label: string;
       onClick: () => void;
       color?: 'primary' | 'secondary' | 'danger'; // Union type
     }

     const Button: React.FC<ButtonProps> = ({ label, onClick, color = 'primary' }) => {
       return (
         <button className={`btn btn-${color}`} onClick={onClick}>
           {label}
         </button>
       );
     };

     const App: React.FC = () => {
       return (
         <div>
           <Button label="Submit" onClick={() => alert('Submitted!')} color="primary" />
           <Button label="Cancel" onClick={() => alert('Cancelled!')} color="secondary" />
         </div>
       );
     };

     export default App;
     ```

  3. **Using Mapped Types for State Management**:  
     You can create a mapped type for managing state in a component.

     ```typescript
     interface FormFields {
       username: string;
       email: string;
       password: string;
     }

     type FormState = {
       [K in keyof FormFields]: string; // Mapped type to define state
     };

     const FormComponent: React.FC = () => {
       const [formState, setFormState] = useState<FormState>({
         username: '',
         email: '',
         password: '',
       });

       const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
         const { name, value } = e.target;
         setFormState((prev) => ({ ...prev, [name]: value }));
       };

       return (
         <form>
           <input name="username" value={formState.username} onChange={handleChange} placeholder="Username" />
           <input name="email" value={formState.email} onChange={handleChange} placeholder="Email" />
           <input name="password" type="password" value={formState.password} onChange={handleChange} placeholder="Password" />
         </form>
       );
     };

     export default FormComponent;
     ```

By exploring and applying these advanced TypeScript features in your React components, you can enhance type safety, improve code readability, and create more flexible and maintainable applications.

[Next: 29-Building-Responsive-UIs](29-Building-Responsive-UIs.md)