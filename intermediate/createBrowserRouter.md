---
title: "createBrowserRouter A step up from Switch"

subtitle: "Learn the limitations of Switch and how createBrowserRouter offers a more flexible and efficient routing solution."

slug: "createBrowserRouter"

tags: web-development, react, react-router, routing, react-router-v6

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1716040937117/DI0ZfBPs-.webp?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

## What is Routing? Why Do We Need It? 🧭

Routing is how you navigate in a web application. It allows you to map URL paths to specific components, enabling users to access various parts of your app without needing to reload the page.
Routing is important because it ensures a seamless user experience, making your app feel similar to a desktop application. It helps in organizing and managing different views, maintaining a clean and efficient codebase, and enabling features like deep linking and dynamic content loading.

## The Good Ol' Days of `Switch`

Back in the day, we used the `Switch` component to handle routing in React. It was straightforward and did the job well by rendering only the first child `<Route>` that matched the location.

Here’s a simple example using `Switch`:

```javascript
import React from "react";
import { BrowserRouter as Router, Route, Switch } from "react-router-dom";
import Home from "./components/Home";
import About from "./components/About";
import Contact from "./components/Contact";

function App() {
  return (
    <Router>
      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
        <Route path="/contact" component={Contact} />
      </Switch>
    </Router>
  );
}

export default App;
```

Pretty neat, right? But as our apps grew more complex, `Switch` started to show its limitations.

## Problems and Limitations of `Switch` 😬

### 1. Lack of Nested Routes

One major limitation of `Switch` was its lack of built-in support for nested routes. In complex applications, it's common to have layouts where some components remain constant (like headers or sidebars) while others change based on the route. With `Switch`, achieving this required cumbersome workarounds and additional code, making the routing setup harder to manage and maintain.

### 2. Limited Error Handling

Error handling was another area where `Switch` fell short. If a user navigated to a non-existent route, handling this gracefully required extra effort. Typically, developers had to add a catch-all route at the end of the `Switch` component, which wasn't always intuitive or straightforward.

```javascript
<Switch>
  <Route exact path="/" component={Home} />
  <Route path="/about" component={About} />
  <Route path="/contact" component={Contact} />
  <Route component={NotFound} /> {/* Catch-all route for 404 errors */}
</Switch>
```

### 3. Verbose and Repetitive Code

For larger applications, the `Switch` setup could become quite verbose and repetitive. Each route had to be defined explicitly within the `Switch` block, leading to cluttered and less maintainable code. This verbosity made it harder to manage and refactor routes, especially as the application grew.

### 4. Limited Data Fetching Capabilities

Handling data fetching and route-based data loading wasn't straightforward with `Switch`. Developers often had to rely on external libraries or custom hooks to fetch data before rendering a component, leading to fragmented code and a less cohesive approach to routing and data management.

### 5. Poor Integration with Modern React Features

As React evolved with new features like hooks and concurrent rendering, `Switch` didn't keep pace. Integrating these modern features into the routing logic required additional effort and custom solutions, making it harder to leverage the full power of React's latest advancements.

## Say Hello to `createBrowserRouter` 👋

With the release of React Router version 6, we got `createBrowserRouter`. It’s packed with powerful features that make routing in React apps easier and more efficient.

## Setting Up `createBrowserRouter`

```bash
npm install react-router-dom
# or
yarn add react-router-dom
```

Now, let’s get into setting up `createBrowserRouter`.

### Basic Setup

1. **Import Necessary Functions:**

Start by importing the required functions from `react-router-dom`:

```javascript
import { createBrowserRouter, RouterProvider } from "react-router-dom";
```

2. **Define Routes:**

Next, define the routes for your application. Here’s a simple example:

```javascript
const router = createBrowserRouter([
  {
    path: "/",
    element: <Home />,
  },
  {
    path: "about",
    element: <About />,
  },
  {
    path: "contact",
    element: <Contact />,
  },
]);
```

In this setup, we have three routes: `/`, `/about`, and `/contact`, each rendering a different component.

### Rendering the Router

To render the router, use the `RouterProvider` component and pass in the router object:

```javascript
function App() {
  return <RouterProvider router={router} />;
}

export default App;
```

## Cool New Features in `createBrowserRouter` 🤩

### Nested Routes

Nested routes are super handy for managing complex applications. They let you define routes within other routes, which is great for layouts where some components are always visible (like a navigation bar) while others change based on the route.

Here’s how you can define nested routes:

```javascript
const router = createBrowserRouter([
  {
    path: "/",
    element: <Home />,
    children: [
      {
        path: "about",
        element: <About />,
      },
      {
        path: "contact",
        element: <Contact />,
      },
    ],
  },
]);
```

In this example, `About` and `Contact` are nested within the `Home` route.

### Route Parameters

Need to capture values from the URL? Route parameters have got you covered. This is especially useful for dynamic routing, like displaying user profiles or articles based on an ID.

```javascript
import UserProfile from "./components/UserProfile";

const router = createBrowserRouter([
  {
    path: "/user/:userId",
    element: <UserProfile />,
  },
]);
```

In this setup, the `UserProfile` component will receive a `userId` parameter from the URL, which can be accessed within the component using hooks like `useParams`.

### Error Handling

You can define error handling routes to display custom error pages for specific conditions:

```javascript
const router = createBrowserRouter([
  {
    path: "/",
    element: <Home />,
    errorElement: <NotFound />,
    children: [
      {
        path: "about",
        element: <About />,
      },
      {
        path: "contact",
        element: <Contact />,
      },
    ],
  },
]);
```

In this example, if a route is not found, the `NotFound` component will be rendered.

### Data Fetching

React Router 6 introduces the ability to define loaders and actions for routes, which can handle data fetching and mutations. This ensures data is loaded before a component is rendered:

```javascript
import { createBrowserRouter } from "react-router-dom";
import Home from "./components/Home";

const router = createBrowserRouter([
  {
    path: "/",
    element: <Home />,
    loader: async () => {
      const data = await fetchData();
      return { data };
    },
  },
]);

async function fetchData() {
  // Fetch your data here
  return fetch("/api/data").then((res) => res.json());
}
```

In this example, `fetchData` is called before rendering the `Home` component, ensuring the component has the necessary data.

## Best Practices

### Organize Routes

Organize your routes in a separate file to keep your code clean and maintainable. For example, create a `routes.js` file:

```javascript
// routes.js
import Home from "./components/Home";
import About from "./components/About";
import Contact from "./components/Contact";

const routes = [
  {
    path: "/",
    element: <Home />,
    children: [
      {
        path: "about",
        element: <About />,
      },
      {
        path: "contact",
        element: <Contact />,
      },
    ],
  },
];

export default routes;
```

Then, import and use this in your main file:

```javascript
import { createBrowserRouter, RouterProvider } from "react-router-dom";
import routes from "./routes";

const router = createBrowserRouter(routes);

function App() {
  return <RouterProvider router={router} />;
}

export default App;
```

### Use Lazy Loading

For better performance, use lazy loading to load components only when needed. React’s `lazy` and `Suspense` can help with this:

```javascript
import React, { lazy, Suspense } from "react";
import { createBrowserRouter, RouterProvider } from "react-router-dom";

const Home = lazy(() => import("./components/Home"));
const About = lazy(() => import("./components/About"));
const Contact = lazy(() => import("./components/Contact"));

const router = createBrowserRouter([
  {
    path: "/",
    element: (
      <Suspense fallback={<div>Loading...</div>}>
        <Home />
      </Suspense>
    ),
    children: [
      {
        path: "about",
        element: (
          <Suspense fallback={<div>Loading...</div>}>
            <About />
          </Suspense>
        ),
      },
      {
        path: "contact",
        element: (
          <Suspense fallback={<div>Loading...</div>}>
            <Contact />
          </Suspense>
        ),
      },
    ],
  },
]);

function App() {
  return <RouterProvider router={router} />;
}

export default App;
```

## Conclusion

`createBrowserRouter` is a big step up from the traditional `Switch` component, offering enhanced flexibility and functionality. With features like nested routes, route parameters, error handling, and data fetching, you can create dynamic and efficient routes for your projects.

For more info refer the [documentation](https://reactrouter.com/en/6.23.1/start/overview)
