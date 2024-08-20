### Chapter 2: Setting Up Your Development Environment

- **Installing Node.js and npm**:  
  1. **Download Node.js**: Visit the [Node.js official website](https://nodejs.org/) and download the LTS (Long Term Support) version suitable for your operating system.
  2. **Install Node.js**: Run the installer and follow the prompts. This will also install npm (Node Package Manager) automatically.
  3. **Verify Installation**: Open your terminal or command prompt and run the following commands to ensure Node.js and npm are installed correctly:
     ```bash
     node -v
     npm -v
     ```

- **Creating a New React Project Using Create React App**:  
  1. **Open Terminal**: Navigate to the directory where you want to create your new project.
  2. **Run Create React App**: Use the following command to create a new React project. Replace `my-app` with your desired project name:
     ```bash
     npx create-react-app my-app --template typescript
     ```
     This command sets up a new React project with TypeScript support.
  3. **Navigate to Your Project Directory**: 
     ```bash
     cd my-app
     ```
  4. **Start the Development Server**: Run the following command to start your React application:
     ```bash
     npm start
     ```
     Your new React app will open in your default web browser at `http://localhost:3000`.

Now your development environment is set up, and you're ready to start building your React application!