---
title: "Why Vite is the best? Advanced Features of Vite"

subtitle: "Learn about advanced features of Vite and how it can revolutionize your frontend development."


slug: "why-vite-is-the-best-advanced-features-of-vite"

tags: "vite", "frontend", "javascript", "web-development", "react", "vue", "svelte"

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1709377058240/4D_mjj4y8.webp?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

Vite is revolutionizing the way we approach frontend development with its exceptional speed and efficiency. This blog explores the more sophisticated applications of Vite, highlighting its potential beyond mere app creation.

### Pre-bundling Modules with Vite

A key highlight of Vite is its method of managing `node_modules` during development. By pre-bundling dependencies using esbuild, Vite significantly lightens the browser's workload, thus speeding up development.

#### Optimizing Pre-bundling:

Vite automatically pre-bundles dependencies, but you can fine-tune this process in `vite.config.js`. For instance:

```javascript
// vite.config.js
export default {
  optimizeDeps: {
    exclude: ["dependency-to-exclude"],
    include: ["dependency-to-force-bundle"],
  },
};
```

This configuration allows you to optimize your project's performance by managing dependencies more effectively.

### Developing Libraries with Vite

Vite is also highly efficient for library development, offering quick Hot Module Replacement (HMR) and an easy setup process.

#### Steps for Library Creation with Vite:

1. Start a new project using a library-focused template.
2. Set up your `vite.config.js` to define build options and output formats:
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
3. Benefit from Vite's rapid development feedback loop.
4. Use `vite build --mode lib` to prepare your library for release.

### Boosting SEO and Performance with SSR and SSG

For SEO and performance, SSR and SSG are essential. Vite natively supports these for frameworks like Vue and React.

#### Implementing SSR/SSG in Vite:

- Activate SSR in Vite for server-side rendering, improving load times.
- Utilize VitePress or external plugins for SSG, taking advantage of static site benefits and SEO improvements.

### Expanding Functionality with Vite Plugins

Vite's extensive plugin ecosystem allows for the expansion of its core capabilities, including framework support and CSS preprocessing.

#### Plugin Installation:

1. Add the desired plugin via npm.
2. Include it in your `vite.config.js`:

   ```javascript
   import vue from "@vitejs/plugin-vue";

   // vite.config.js
   export default {
     plugins: [vue()],
   };
   ```

### Incorporating Pre-Processors

Vite seamlessly supports pre-processors like Sass, Less, and Stylus. Installing Sass, for example, is straightforward:

```shell
$ npm install -D sass
```

Then, refactor your `App.jsx` to use a new `Counter` component.

**src/components/Counter.jsx**

```jsx
import { useState } from "react";
import styles from "./counter.module.scss";

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div className={styles.counter}>
      <button onClick={() => setCount((count) => count + 1)}>
        count is: {count}
      </button>
    </div>
  );
};

export default Counter;
```

To use Sass, simply create a `.scss` file and import it into your component. This also demonstrates the use of CSS modules.

**src/components/counter.module.scss**

```css
.counter {
  background-color: bisque;
}
```

And update your `App.jsx`.

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

### Simplifying Imports with Absolute Paths in Vite

Avoiding complex relative paths is a boon, and Vite makes it easy to use absolute imports via a simple `vite.config.js` tweak.

**vite.config.js**

```js
import path from "path";
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
});
```

Also, inform your code editor of this configuration through `jsconfig.json` or `tsconfig.json` for TypeScript.

**src/App.jsx** then becomes simpler:

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

## Managing Environmental Variables

Vite handles environmental variables differently, requiring a `VITE_` prefix for client-side exposure.

**.env**

```js
VITE_MESSAGE = "Hello Vite!";
```

Vite exposes these variables

via `import.meta.env` rather than `process.env`.

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

### Is Vite the Future of Frontend Development?

Vite represents a leap forward in improving the developer experience, scalability, and performance of web applications. Its modern approach positions it as a compelling choice for future projects, underscoring the importance of selecting the right tool for your project's needs and team dynamics.
