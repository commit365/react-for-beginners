### Chapter 29: Building Responsive UIs

- **Techniques for Building Responsive User Interfaces**:  
  Building responsive user interfaces (UIs) is essential for providing a seamless experience across different devices and screen sizes. Here are some techniques to achieve responsive design in your React applications:

  1. **Fluid Layouts**:  
     Use relative units like percentages (`%`), `vw` (viewport width), and `vh` (viewport height) instead of fixed units like pixels. This allows elements to resize based on the viewport size.

     ```css
     .container {
       width: 80%; /* Fluid width */
       padding: 20px;
       margin: auto;
     }
     ```

  2. **Media Queries**:  
     Use CSS media queries to apply different styles based on the screen size. This allows you to adjust layouts, font sizes, and other styles for various devices.

     ```css
     @media (max-width: 768px) {
       .container {
         flex-direction: column; /* Stack elements on smaller screens */
       }
     }
     ```

  3. **Flexbox and Grid Layouts**:  
     Utilize CSS Flexbox and Grid to create flexible and adaptive layouts. These layout models allow you to distribute space and align items within a container effectively.

     ```css
     .flex-container {
       display: flex;
       justify-content: space-between;
       flex-wrap: wrap; /* Allow items to wrap */
     }

     .grid-container {
       display: grid;
       grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); /* Responsive grid */
       gap: 16px;
     }
     ```

  4. **Responsive Images**:  
     Use the `srcset` attribute or CSS properties like `max-width: 100%` to ensure images scale properly on different devices.

     ```html
     <img src="image.jpg" srcset="image-small.jpg 600w, image-medium.jpg 1200w, image-large.jpg 1800w" alt="Responsive" style="max-width: 100%;">
     ```

  5. **Viewport Units**:  
     Use viewport units (`vw`, `vh`) for font sizes and spacing to ensure they scale with the viewport.

     ```css
     h1 {
       font-size: 5vw; /* Font size scales with viewport width */
     }
     ```

- **Using CSS-in-JS Libraries (e.g., styled-components)**:  
  CSS-in-JS libraries like `styled-components` allow you to write CSS directly within your JavaScript files, enabling dynamic styling based on props and state. This approach can enhance the maintainability of your styles in React applications.

  1. **Installation**:  
     To get started with `styled-components`, install it using npm:

     ```bash
     npm install styled-components
     ```

  2. **Creating Styled Components**:  
     You can create styled components by defining a styled version of a regular HTML element.

     ```typescript
     import styled from 'styled-components';

     const Container = styled.div`
       display: flex;
       flex-direction: column;
       align-items: center;
       padding: 20px;
       max-width: 800px;
       margin: auto;
     `;

     const Button = styled.button<{ primary?: boolean }>`
       background-color: ${(props) => (props.primary ? 'blue' : 'gray')};
       color: white;
       padding: 10px 20px;
       border: none;
       border-radius: 5px;
       cursor: pointer;

       &:hover {
         background-color: ${(props) => (props.primary ? 'darkblue' : 'darkgray')};
       }
     `;
     ```

  3. **Using Styled Components in Your Application**:  
     You can use the styled components in your React components like regular JSX elements.

     ```typescript
     import React from 'react';
     import { Container, Button } from './StyledComponents'; // Import your styled components

     const App: React.FC = () => {
       return (
         <Container>
           <h1>Responsive UI with Styled Components</h1>
           <Button primary onClick={() => alert('Primary Button Clicked!')}>
             Primary Button
           </Button>
           <Button onClick={() => alert('Secondary Button Clicked!')}>
             Secondary Button
           </Button>
         </Container>
       );
     };

     export default App;
     ```

  4. **Dynamic Styling**:  
     Styled-components allow you to style components dynamically based on props, making it easier to create responsive designs.

     ```typescript
     const ResponsiveText = styled.h1<{ isMobile: boolean }>`
       font-size: ${(props) => (props.isMobile ? '24px' : '48px')};
       color: ${(props) => (props.isMobile ? 'blue' : 'black')};
     `;

     const App: React.FC = () => {
       const isMobile = window.innerWidth < 768;

       return <ResponsiveText isMobile={isMobile}>Hello, World!</ResponsiveText>;
     };
     ```

By employing these techniques for building responsive user interfaces and utilizing CSS-in-JS libraries like `styled-components`, you can create modern, flexible, and maintainable React applications that provide a great user experience across various devices and screen sizes.