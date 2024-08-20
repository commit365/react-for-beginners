### Chapter 13: Form Validation Techniques

- **Implementing Validation with Libraries Like Formik and Yup**:  
  Formik is a popular library for managing forms in React, and Yup is a schema validation library that works well with Formik. Together, they simplify form handling and validation. Here’s how to implement validation using Formik and Yup:

  1. **Install Formik and Yup**:
     ```bash
     npm install formik yup
     ```

  2. **Create a Form with Validation**:

  ```typescript
  import React from 'react';
  import { Formik, Form, Field, ErrorMessage } from 'formik';
  import * as Yup from 'yup';

  const validationSchema = Yup.object().shape({
    name: Yup.string()
      .required('Name is required')
      .min(2, 'Name must be at least 2 characters'),
    email: Yup.string()
      .required('Email is required')
      .email('Invalid email format'),
  });

  const UserForm: React.FC = () => {
    return (
      <Formik
        initialValues={{ name: '', email: '' }}
        validationSchema={validationSchema}
        onSubmit={(values) => {
          console.log('Form data:', values);
        }}
      >
        {() => (
          <Form>
            <div>
              <label htmlFor="name">Name:</label>
              <Field type="text" id="name" name="name" />
              <ErrorMessage name="name" component="div" style={{ color: 'red' }} />
            </div>
            <div>
              <label htmlFor="email">Email:</label>
              <Field type="email" id="email" name="email" />
              <ErrorMessage name="email" component="div" style={{ color: 'red' }} />
            </div>
            <button type="submit">Submit</button>
          </Form>
        )}
      </Formik>
    );
  };

  export default UserForm;
  ```

  In this example:
  - We define a validation schema using Yup to specify the rules for the `name` and `email` fields.
  - The Formik component manages the form state, handles validation, and submits the form data.
  - The `ErrorMessage` component displays validation errors below each field.

- **Custom Validation Logic in Forms**:  
  In addition to using libraries, you can implement custom validation logic directly in your form. This can be useful for more complex validation scenarios. Here’s how to create a form with custom validation:

  ```typescript
  import React, { useState } from 'react';

  const CustomValidationForm: React.FC = () => {
    const [name, setName] = useState('');
    const [email, setEmail] = useState('');
    const [errors, setErrors] = useState<{ name?: string; email?: string }>({});

    const validate = () => {
      const newErrors: { name?: string; email?: string } = {};
      if (!name) {
        newErrors.name = 'Name is required';
      } else if (name.length < 2) {
        newErrors.name = 'Name must be at least 2 characters';
      }

      if (!email) {
        newErrors.email = 'Email is required';
      } else if (!/\S+@\S+\.\S+/.test(email)) {
        newErrors.email = 'Invalid email format';
      }

      setErrors(newErrors);
      return Object.keys(newErrors).length === 0; // Return true if no errors
    };

    const handleSubmit = (event: React.FormEvent<HTMLFormElement>) => {
      event.preventDefault();
      if (validate()) {
        console.log('Form data:', { name, email });
        // Reset form or perform other actions
      }
    };

    return (
      <form onSubmit={handleSubmit}>
        <div>
          <label htmlFor="name">Name:</label>
          <input
            type="text"
            id="name"
            value={name}
            onChange={(e) => setName(e.target.value)}
          />
          {errors.name && <div style={{ color: 'red' }}>{errors.name}</div>}
        </div>
        <div>
          <label htmlFor="email">Email:</label>
          <input
            type="email"
            id="email"
            value={email}
            onChange={(e) => setEmail(e.target.value)}
          />
          {errors.email && <div style={{ color: 'red' }}>{errors.email}</div>}
        </div>
        <button type="submit">Submit</button>
      </form>
    );
  };

  export default CustomValidationForm;
  ```

  In this custom validation example:
  - We define a `validate` function that checks for errors in the `name` and `email` fields.
  - The `handleSubmit` function calls the `validate` function before logging the form data.
  - Error messages are displayed conditionally based on the validation results.

By implementing form validation techniques using libraries like Formik and Yup or through custom logic, you can ensure that your forms are user-friendly and robust, providing immediate feedback to users.