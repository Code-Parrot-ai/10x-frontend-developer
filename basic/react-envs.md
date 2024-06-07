---
title: Using environment variables in React and Vite
subtitle: Learn how to use environment variables in React and Vite to manage secrets and configuration settings in your applications.
slug: using-environment-variables-in-react-and-vite
tags: react, vite, environment variables, web development
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1717650343290/bXI1QAocx.webp?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---

Environment variables are a powerful way to manage secrets and configuration settings in your applications. They allow you to store sensitive information like API keys, database credentials, and other configuration settings outside of your codebase. This makes it easier to manage your application's configuration and reduces the risk of exposing sensitive information in your code.

This becomes highly useful when you are planning to make your code open-source or share it with others. In this article, we will learn how to use environment variables in React and Vite to manage secrets and configuration settings in your applications.

## Using environment variables in React

- Create a `.env` file in the root of your React project. You can create this file manually or use the `touch` command in your terminal.

```bash
touch .env
```

- Add your environment variables to the `.env` file. Prefix your variables with `REACT_APP_` to make them available in your React application.

```bash
REACT_APP_API_KEY=your-api-key
REACT_APP_API_URL=https://api.example.com
```

- Access your environment variables in your React components using `process.env`.

```jsx
const apiKey = process.env.REACT_APP_API_KEY;
const apiUrl = process.env.REACT_APP_API_URL;

console.log("API Key:", apiKey);
console.log("API URL:", apiUrl);
```

- Remember to restart your development server after adding or updating environment variables in your `.env` file.

## Using environment variables in Vite

Vite provides built-in support for environment variables using the `.env` files. You can create different `.env` files for different environments like development, production, and testing.

- Create a `.env` file in the root of your Vite project. You can create this file manually or use the `touch` command in your terminal.

```bash
touch .env
```

- Add your environment variables to the `.env` file. Prefix your variables with `VITE_` to make them available in your Vite application.

```bash
VITE_API_KEY=your-api-key
VITE_API_URL=https://api.example.com
```

- Access your environment variables in your Vite application using `import.meta.env`.

```jsx
const apiKey = import.meta.env.VITE_API_KEY;
const apiUrl = import.meta.env.VITE_API_URL;

console.log("API Key:", apiKey);
console.log("API URL:", apiUrl);
```

- Remember to restart your development server after adding or updating environment variables in your `.env` file.

## Benefits of using Vite for environment variables

Vite uses `.env` files to load environment variables. You can create different `.env` files for different environments:

- `.env`: Loaded in all cases.
- `.env.local`: Loaded in all cases, ignored by git.
- `.env.[mode]`: Loaded only in the specified mode (e.g., .env.production).
- `.env.[mode]`.local: Loaded only in the specified mode, ignored by git.

### TypeScript Support

For TypeScript projects, you can enhance IntelliSense by defining custom environment variables. Create a `vite-env.d.ts` file in your src directory:

```typescript
/// <reference types="vite/client" />

interface ImportMetaEnv {
  readonly VITE_APP_TITLE: string;
  // more env variables...
}

interface ImportMeta {
  readonly env: ImportMetaEnv;
}
```

If your code relies on types from browser environments such as DOM and WebWorker, you can update the lib field in `tsconfig.json`. 

```json
{
  "lib": ["WebWorker"]
}
```

## Note

- Environment variables prefixed with `REACT_APP_` are automatically embedded into the build by Create React App. You don't need to use a package like `dotenv` to load environment variables in your React application.

- Vite automatically loads environment variables from `.env` files and makes them available in your application using `import.meta.env`. You don't need to use a package like `dotenv` to load environment variables in your Vite application.

- Make sure to add your `.env` files to your `.gitignore` file to prevent them from being committed to your version control system.

Using environment variables in React and Vite is a great way to manage secrets and configuration settings in your applications. It allows you to store sensitive information outside of your codebase and makes it easier to manage your application's configuration. I hope this article helps you understand how to use environment variables in React and Vite. Happy coding! 🚀