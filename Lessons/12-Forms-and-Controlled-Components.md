### Chapter 12: Forms and Controlled Components

- **Building Forms with Controlled Components**:  
  In React, controlled components are form elements whose values are controlled by the component's state. This means that the form data is stored in the component's state, making it easier to manage and validate. Here’s how to create a simple controlled form:

  ```typescript
  import React, { useState } from 'react';

  const UserForm: React.FC = () => {
    const [name, setName] = useState('');
    const [email, setEmail] = useState('');

    const handleNameChange = (event: React.ChangeEvent<HTMLInputElement>) => {
      setName(event.target.value);
    };

    const handleEmailChange = (event: React.ChangeEvent<HTMLInputElement>) => {
      setEmail(event.target.value);
    };

    return (
      <form>
        <div>
          <label htmlFor="name">Name:</label>
          <input
            type="text"
            id="name"
            value={name}
            onChange={handleNameChange}
          />
        </div>
        <div>
          <label htmlFor="email">Email:</label>
          <input
            type="email"
            id="email"
            value={email}
            onChange={handleEmailChange}
          />
        </div>
      </form>
    );
  };

  export default UserForm;
  ```

  In this example:
  - The `UserForm` component contains two controlled inputs: one for the user's name and another for their email.
  - The `value` of each input is tied to the component's state, and changes are handled by the corresponding `onChange` event handlers.

- **Handling Input Changes and Form Submissions**:  
  To handle input changes, you can define event handlers that update the component's state. Additionally, you can handle form submissions by defining a function that processes the form data when the user submits the form.

  Here’s how to add form submission handling:

  ```typescript
  const handleSubmit = (event: React.FormEvent<HTMLFormElement>) => {
    event.preventDefault(); // Prevent the default form submission behavior
    console.log('Name:', name);
    console.log('Email:', email);
    // You can also send the data to an API here
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label htmlFor="name">Name:</label>
        <input
          type="text"
          id="name"
          value={name}
          onChange={handleNameChange}
        />
      </div>
      <div>
        <label htmlFor="email">Email:</label>
        <input
          type="email"
          id="email"
          value={email}
          onChange={handleEmailChange}
        />
      </div>
      <button type="submit">Submit</button>
    </form>
  );
  ```

  In this updated example:
  - The `handleSubmit` function is triggered when the form is submitted. It prevents the default behavior of the form submission (which would refresh the page) and logs the name and email to the console.
  - The `<button>` element is used to submit the form.

By using controlled components and handling input changes and form submissions effectively, you can create dynamic and interactive forms in your React applications.

[Next: 13-Form-Validation-Techniques](13-Form-Validation-Techniques.md)