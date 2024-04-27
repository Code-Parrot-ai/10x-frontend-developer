---
title: "Is Waku a new NextJS?"

subtitle: "Comparing Waku and NextJS for server-side rendering with React Server Components"

slug: "waku-vs-nextjs"

tags: web-development, frontend, react, waku, nextjs, server-side-rendering

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1713538526996/vlhNIZvrM.png?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

Waku is a cutting-edge framework designed specifically to harness the full potential of React Server Components (RSCs). Its primary goal is to provide a simplified, streamlined environment for developers looking to focus exclusively on server-side rendering capabilities within the React ecosystem.

## What is React Server Components (RSCs) ? 🤔

React Server Components allow UI components to be rendered directly on the server, differing from traditional React components that render on the client side after the initial page load. This server-side execution offers several benefits:

- **Improved Load Performance:** Since the server handles the rendering, the client has less processing to do, which speeds up the initial page load.
- **Better SEO:** Content rendered on the server is more readily indexed by search engines, potentially boosting search rankings.
- **Simplified Data Fetching:** Direct server access to databases and APIs simplifies data management, avoiding common data-fetching complexities in React.

However, RSCs come with limitations such as the inability to access the DOM or use client-side APIs like `useState` and `useEffect`.
For more info: [Is server side rendering always good?](https://dev.to/codeparrot/is-server-side-rendering-always-good-5g9f)

## Key Features of Waku 🥷

### Weaving Patterns in Waku

Weaving patterns refer to the methodology used to intertwine server components and client components within the same application architecture. This feature is particularly beneficial in applications that require both heavy server-side processing and dynamic client-side interactions. By structuring components in a way that they can be interwoven, Waku allows developers to optimize performance while maintaining clarity and separation of server and client logic.

#### Example:

Consider a web application that displays user profiles with data fetched from a database and includes an interactive map showing user locations. In this scenario, the profile details should be rendered on the server to benefit from faster initial load times and SEO, while the interactive map should be handled on the client due to its dynamic nature and dependency on the DOM and browser APIs.

### Simplified Data Fetching with Server Component 🖥️

This component is responsible for fetching and displaying user data. Since it involves database access—a server-side operation—it's defined as a server component. By default components are server components in Waku.

#### Code Example:

```javascript
// UserProfile.js - A server component
import db from "server-db";

export async function UserProfile({ userId }) {
  const userData = await db.query(`SELECT * FROM users WHERE id = ${userId}`);
  const user = userData[0]; // Assume we get one user

  return (
    <div>
      <h1>{user.name}</h1>
      <p>Email: {user.email}</p>
      <p>Location: {user.location}</p>
      <InteractiveMap location={user.location} />
    </div>
  );
}
```

### Interactive Client Component 🧑‍💻

To integrate client-specific functionalities (like interactions or animations that require browser APIs), Waku uses the `use client` directive. You can't use `useState`,`useEffect` and event handlers etc. react features in server components, for that you need client component.

#### Code Example:

```javascript
// InteractiveMap.js - A client component marked with useClient
import { useClient } from "waku";

const InteractiveMap = useClient(({ location }) => {
  // Logic to render a map based on the location
  return <div id="map">{/* Map library and initialization code here */}</div>;
});
```

## Routing in Waku 🧭

Waku adopts a file-based routing system, which is similar to that of Next.js. This approach automatically maps files in the project's `pages` directory to corresponding routes. For example, a file located at `/pages/about.js` would automatically correspond to the `/about` URL path. This simplicity is one of Waku's core principles, making it easy for developers to manage routes without the need for additional routing libraries or configurations.

### Key Features of Waku's Routing:

- **Server Component Integration:** Each route is inherently a server component, leveraging React Server Components to render directly from the server. This integration allows routes to handle server-side logic, such as database interactions and API calls, before sending the final HTML to the client.
- **Direct and Simple Setup:** Creating a new route is as simple as adding a new file in the appropriate directory. There’s no need for route declarations or configurations.

### Example:

```javascript
// File: /pages/contact.js

import React from "server";

export default function Contact() {
  return (
    <div>
      <h1>Contact Us</h1>
      <p>Send us your feedback!</p>
    </div>
  );
}
```

This will create a new route `/contact` in the web app.

### Router Functions:

```javascript
// File: /pages/api/login.js

export async function loginUser(req) {
  const { username, password } = req.body;
  // Authentication logic here
  return { status: 'success', message: 'Logged in successfully' };
}

export default async function handler(req, res) {
  the result = await

 loginUser(req);
  res.json(result);
}
```

In this setup, `loginUser` is a router function that processes the login credentials. The `handler` function uses this router function to respond to the client, illustrating how router functions can streamline API route implementations.

## Waku Vs Next ⚔️

### Focus and Philosophy

**Waku:** Simplicity at its core! Waku is designed specifically for server-side rendering with React Server Components. It's perfect if you're looking for a streamlined, efficient framework that keeps server-side complexity to a minimum. Ideal for smaller projects where server performance is crucial without the need for frills.

**Next.js:** A powerhouse of features! Next.js is your go-to if you need a comprehensive solution that handles everything from static site generation (SSG) to dynamic server-side rendering (SSR). It's built for larger, more complex applications and comes packed with functionalities like API routes, automatic code splitting, and much more.

### Routing Capabilities

#### Waku:

- **Simple, File-based Routing:** Waku utilizes a straightforward file-based routing system, where the creation of a file in the `pages` directory automatically sets up a corresponding route. This system is incredibly intuitive and requires minimal configuration, aligning with Waku’s goal of simplicity.
- **Server-Side Focus:** Each route in Waku is optimized for server-side rendering, ensuring that data fetching and computations are handled efficiently before being sent to the client.

#### Next.js:

- **Dynamic and Nested Routing:** Next.js supports dynamic routes, which allow developers to create routes that adapt based on the data being passed, such as user IDs or product names. Nested routes can also be configured, allowing for complex application structures.
- **API Routes:** Next.js can handle API requests with its API routes feature, enabling the server to deal with API calls directly within the framework. This is particularly useful for handling form submissions, database interactions, and more, directly from within Next.js without the need for a separate backend.
- **Middleware Support:** Next.js introduced middleware capabilities that can run before a request is completed. Middleware in Next.js can be used for tasks like authentication, redirects, and more, directly on the server before reaching the React application.

### Extra Features in Next.js

- **Plugin Ecosystem:** Next.js has a rich plugin ecosystem that allows developers to easily integrate with other tools and services. Plugins can cover a wide range of functionalities, from SEO enhancements to advanced analytics integrations.
- **Built-In CSS Support:** Next.js supports CSS-in-JS libraries out of the box, as well as global CSS and component-level CSS modules. This built-in support simplifies the process of styling applications.
- **Optimized Image Handling:** Next.js includes an Image component that automatically optimizes images for performance, such as resizing, optimizing, and serving images in modern formats.
- **Community and Support:** Being developed and maintained by Vercel, Next.js has a large community of users and a comprehensive documentation library, making it easier to find solutions and get support for development issues.

## What's best? 💪

Think about your project's requirements and answer these questions:

1. Do you need a simple, server-focused framework primarily for server-side rendering?
   **Yes** (Go Waku) | **No** (Consider Next.js)
2. Is your project complex, requiring features like static site generation, API handling, or middleware?
   **Yes** (Next.js is better suited) | **No** (Waku might be enough)
3. Do you prefer having a large community and extensive plugins?
   **Yes** (Next.js is ideal) | **No** (Waku keeps it simpler)

Choosing the right framework doesn't have to be a daunting task. By understanding the unique offerings of Waku and Next.js, you can align your project's needs with the framework that best supports your goals.
