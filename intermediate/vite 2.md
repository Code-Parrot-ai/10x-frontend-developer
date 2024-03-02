---
title: ""

subtitle: "Learn about the key differences and complimentary nature of npm and npx"

slug: "npm-vs-npx-package-management"

tags: web development, frontend, javascript, reactjs, npm, npx

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706941937960/0D57g4zj9.png?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

Certainly! Below is the enhanced version of your blog, incorporating the suggestions for improvement:

---

## Advanced Use Cases of Vite

Vite is transforming the landscape of frontend development with its unparalleled speed and efficiency. This blog delves into the advanced use cases of Vite, showcasing its capabilities beyond simple application development.

### Module Pre-bundling with Vite

One of Vite's standout features is its approach to handling `node_modules` during development. By pre-bundling dependencies with esbuild, Vite significantly reduces the browser's load, enhancing development speed.

#### How to Leverage Pre-bundling:

Vite's pre-bundling is automatic, but you can tailor it in `vite.config.js`. For example:

```javascript
// vite.config.js
export default {
  optimizeDeps: {
    exclude: ["dependency-to-exclude"],
    include: ["dependency-to-force-bundle"],
  },
};
```

This customization ensures your project runs optimally by precisely controlling dependency handling.

### Leveraging Vite for Library Development

Vite excels in library development, thanks to its fast Hot Module Replacement (HMR) and simple setup.

#### Steps to Create a Library with Vite:

1. Initialize a new project with a library template.
2. In `vite.config.js`, configure the build options for desired output formats:
   ```javascript
   export default {
     build: {
       lib: {
         entry: "src/mylib.js",
         name: "MyLib",
         formats: ["es", "umd"],
       },
     },
   };
   ```
3. Enjoy Vite's instant feedback loop during development.
4. Build your library for publication with `vite build --mode lib`.

### Enhancing SEO and Performance with SSR and SSG

SSR and SSG are vital for SEO and performance. Vite supports these out of the box for frameworks like Vue and React.

#### Implementing SSR/SSG with Vite:

- Use Vite's SSR mode for server pre-rendering, enhancing initial load time.
- Leverage tools like VitePress or third-party plugins for SSG, benefiting from static site speed and SEO.

### Building with Vite Plugins

Vite's plugin ecosystem allows for extending its core functionality, from framework support to CSS preprocessing.

#### How to Add a Plugin:

1. Install your chosen plugin via npm.
2. Configure it in `vite.config.js`:

   ```javascript
   import vue from "@vitejs/plugin-vue";

   // vite.config.js
   export default {
     plugins: [vue()],
   };
   ```

## Comparing with Create-React-App

### Flexibility and Configuration

Vite offers more flexibility and easier configuration without the need to eject. This can be particularly beneficial in projects requiring custom build processes or integration with other tools.

#### Comparative Insight:

A project might need to integrate with a CMS, requiring custom webpack configurations. With CRA, this would mean ejecting and potentially complicating future upgrades. Vite, on the other hand, allows for easy customization through its `vite.config.js` file.

### Development Speed

Vite's speed in development, through its instant server start and fast HMR, presents a clear advantage, especially in projects where developer efficiency is paramount.

#### Comparative Insight:

In a team environment, where multiple developers are working on a complex application, Vite's rapid feedback loop can significantly enhance productivity compared to the slower start-up and refresh times associated with CRA.

## Conclusion: Is Vite the Future of Frontend Development?

Vite is more than a tool for speeding up development; it's a comprehensive solution for enhancing the developer experience, scalability, and performance of web applications. As the web development landscape continues to evolve, Vite stands out as a forward-thinking choice for developers aiming to stay ahead of the curve.

Remember, the best tool is the one that fits your project's needs and team dynamics. With its modern approach and developer-friendly features, Vite is undoubtedly worth considering for your next project or to enhance your development workflow.

## Scaffolding a React Project With Vite

Vite can be used to scaffold projects for multiple frameworks, such as React, Vue, Svelte, etc. For this example, let’s create a React application. Run one of the commands below in your terminal.

```shell
# npm 6.x
npm init vite@latest my-vite-react-app --template react

# npm 7+, extra double-dash is needed:
npm init vite@latest my-vite-react-app -- --template react

# yarn
yarn create vite my-vite-react-app --template react

# pnpm
pnpm create vite my-vite-react-app -- --template react

```

Shell

After the project is scaffolded, cd into it, install all dependencies and start the development server.

```shell
$ cd my-vite-react-app
$ npm install // or yarn
$ npm run dev // or yarn dev

```

Shell

By default, the dev server starts on port 3000, so head to http://localhost:3000 in your browser. You should see something like:

![Vite React](https://d585tldpucybw.cloudfront.net/sfimages/default-source/blogs/2022/2022-01/vite-react-start.png?sfvrsn=199fe148_2 "Vite React")

That’s it for scaffolding the project. Let’s have a look at how we can add a pre-processor, such as SCSS, to a Vite project.

---

## Using Pre-Processors

Vite has built-in support for Sass, Less and Stylus. They can be added to the project simply by installing them as dependencies. For this example, let’s install Sass.

```shell
$ npm install -D sass

```

Shell

Next, let’s move the counter logic from the `App.jsx` file to a new component called `Counter`.

**src/components/Counter.jsx**

```jsx
import { useState } from "react";
import styles from "./counter.module.scss";

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div className={styles.counter}>
      <button type="button" onClick={() => setCount((count) => count + 1)}>
        count is: {count}
      </button>
    </div>
  );
};

export default Counter;
```

React JSX

Using Sass is as simple as creating a new file with `.scss` extension and then importing it in a component. Besides Sass, we will also use CSS modules. They can be used by simply adding `.module` before the file extension in the file name. For example, `styles.module.css` or `styles.module.scss` if you are using a CSS pre-processor.

**src/components/counter.module.scss**

```css
.counter {
  background-color: bisque;
}
```

CSS

Finally, update the `App.jsx` file.

**src/App.jsx**

```jsx
import "./App.css";
import Counter from "./components/Counter";

function App() {
  return (
    <div className="App">
      <Counter />
    </div>
  );
}

export default App;
```

React JSX

## Path Resolving and Absolute Imports With Vite

One thing I really find cumbersome is having to import components using relative paths. While our example is simple, I worked on projects that had a lot of nested files, and sometimes imports looked like this:

```js
import FancyModal from "../../../../components/modal/FancyModal/FancyModal.jsx";
```

JavaScript

Wouldn’t it be great if, instead, we could do something like this?

```js
import FancyModal from "@/components/modal/FancyModal/FancyModal.jsx";
```

JavaScript

Personally, I prefer to use absolute imports as they are much cleaner. We can configure Vite to support them by modifying the `vite.config.js` file. Below, you can see the code for adding the `@` alias that will resolve to the `src` directory.

**vite.config.js**

```js
import path from "path";
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
});
```

JavaScript

Besides configuring Vite to resolve the `@` alias, we also need to tell our code editor about it. We can do so by creating the `jsconfig.json` file with the contents below.

**jsconfig.json**

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}
```

JSON

If you’re using TypeScript, then you would do it in a `tsconfig.json` file.

Finally, we can update the `Counter` import.

**src/App.jsx**

```jsx
import "./App.css";
import Counter from "@/components/Counter";

function App() {
  return (
    <div className="App">
      <Counter />
    </div>
  );
}

export default App;
```

React JSX

## Environmental Variables

There is a slight difference when it comes to using environmental variables in applications scaffolded with Vite. First of all, any environmental variables defined in the `.env` file that should be exposed to the client-side code need to be prefixed with `VITE_`word. Create a new `.env` file in the root directory and add `VITE_MESSAGE` variable as shown below.

**.env**

```js
VITE_MESSAGE = "Hello Vite!";
```

JavaScript

Another difference is how we access this environmental variable in the application. Most CLIs, such as Create React App, expose environmental variables on the `process.env` object. However, Vite exposes them on `import.meta.env` instead.

Let’s update the `App` component to display the `Hello Vite!` message.

**src/App.jsx**

```jsx
import "./App.css";
import Counter from "./components/Counter.jsx";

function App() {
  return (
    <div className="App">
      <Counter />
      {import.meta.env.VITE_MESSAGE}
    </div>
  );
}

export default App;
```
