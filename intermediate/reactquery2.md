### What is React Query?

React Query is a powerful data-fetching library for React applications. It simplifies the process of fetching, caching, synchronizing, and updating server state in your React applications. Instead of managing data fetching manually, it provides a set of tools and hooks that make these tasks easier and more efficient.

### Key Features

- **Data Fetching**: This library uses hooks to fetch data, making the process straightforward. You can fetch and push data using the `useQuery` and `useMutation` hooks, which abstract away the complexities of manual data fetching.
- **Caching**: It automatically caches the fetched data, reducing the need for redundant network requests. This improves performance and reduces load times.
- **Synchronization**: Ensures that your data is always synchronized with the server. It automatically refetches data when necessary, such as when the user revisits a page.
- **Background Updates**: Can refresh stale data in the background without blocking the UI. This ensures that your users always see the most recent information.
- **Query Invalidation**: You can invalidate and refetch queries as needed, such as after a mutation. This ensures that your data remains consistent with the server state.
- **Optimistic Updates**: Allow your UI to update before the server responds. This makes the application feel more responsive and reduces perceived latency.

### Basic Usage

To get started with this library, you need to install it:

```bash
npm install @tanstack/react-query
```

Next, wrap your application with the `QueryClientProvider` and create a `QueryClient` instance:

```jsx
import React from "react";
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

import PostsComponent from "./PostsComponent";

const queryClient = new QueryClient();

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <PostsComponent />
    </QueryClientProvider>
  );
}

export default App;
```

In your component, use the `useQuery` hook to fetch data:

```jsx
import React from "react";
import { useQuery } from "@tanstack/react-query";

function PostsComponent() {
  const { data, error, isFetching, refetch } = useQuery({
    queryKey: ["posts"],
    queryFn: () =>
      fetch("https://jsonplaceholder.typicode.com/posts").then((res) =>
        res.json()
      ),
    enabled: false,
  });

  return (
    <div>
      <button onClick={refetch}>Load Posts</button>
      <div>
        {isFetching && <div>Loading posts...</div>}
        {error && <div>Error fetching posts!</div>}
        {data &&
          data.map((post) => (
            <div key={post.id}>
              <h4>{post.title}</h4>
              <p>{post.body}</p>
            </div>
          ))}
      </div>
    </div>
  );
}

export default PostsComponent;
```

In this example, the `useQuery` hook fetches data from the specified URL. The `isLoading` flag indicates whether the data is being fetched, while the `error` object contains any errors that may occur during the fetch. Once the data is loaded, it is displayed in the component.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721977325474/9F-s1d_da.gif?auto=format)

### Advanced Usage

#### Query Invalidation

Query invalidation is useful when you need to refetch data based on certain events, like after a mutation. This ensures that your data stays up-to-date. Here's an example:

```jsx
import React from "react";
import { useQuery, useQueryClient } from "@tanstack/react-query";

function MyComponent() {
  const queryClient = useQueryClient();

  const { data, error, isLoading } = useQuery("dataKey", fetchData);

  const invalidateData = () => {
    queryClient.invalidateQueries("dataKey");
  };

  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>An error occurred: {error.message}</p>;

  return (
    <div>
      {data.map((item) => (
        <p key={item.id}>{item.name}</p>
      ))}
      <button onClick={invalidateData}>Refresh Data</button>
    </div>
  );
}

async function fetchData() {
  const response = await fetch("https://api.example.com/data");
  if (!response.ok) {
    throw new Error("Network response was not ok");
  }
  return response.json();
}
```

In this example, the `invalidateData` function invalidates the query with the key "dataKey", causing it to refetch the data. This ensures that the data is always up-to-date with the server.

#### Mutations

Mutations handle creating, updating, or deleting data. You can use the `useMutation` hook to perform these actions. Here’s an example of updating data:

```jsx
import React from "react";
import { useMutation, useQueryClient } from "@tanstack/react-query";

function UpdateDataComponent() {
  const queryClient = useQueryClient();
  const mutation = useMutation(updateData, {
    onSuccess: () => {
      queryClient.invalidateQueries("dataKey");
    },
  });

  const handleUpdate = () => {
    mutation.mutate({ id: 1, name: "Updated Item" });
  };

  return <button onClick={handleUpdate}>Update Data</button>;
}

async function updateData(updatedItem) {
  const response = await fetch(`/api/data/${updatedItem.id}`, {
    method: "PUT",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(updatedItem),
  });
  if (!response.ok) {
    throw new Error("Network response was not ok");
  }
  return response.json();
}
```

In this example, the `useMutation` hook updates the data by calling the `updateData` function. If the mutation is successful, the query with the key "dataKey" is invalidated, causing it to refetch the data.

#### Optimistic Updates

Optimistic updates allow your UI to update before the server responds, providing a faster and smoother user experience. Here’s how you can implement it:

```jsx
import React from "react";
import { useMutation, useQueryClient } from "@tanstack/react-query";

function OptimisticUpdateComponent() {
  const queryClient = useQueryClient();
  const mutation = useMutation(updateData, {
    onMutate: async (newData) => {
      await queryClient.cancelQueries("dataKey");

      const previousData = queryClient.getQueryData("dataKey");

      queryClient.setQueryData("dataKey", (oldData) =>
        oldData.map((item) =>
          item.id === newData.id ? { ...item, ...newData } : item
        )
      );

      return { previousData };
    },
    onError: (err, newData, context) => {
      queryClient.setQueryData("dataKey", context.previousData);
    },
    onSettled: () => {
      queryClient.invalidateQueries("dataKey");
    },
  });

  const handleUpdate = () => {
    mutation.mutate({ id: 1, name: "Optimistically Updated Item" });
  };

  return <button onClick={handleUpdate}>Optimistic Update</button>;
}

async function updateData(updatedItem) {
  const response = await fetch(`/api/data/${updatedItem.id}`, {
    method: "PUT",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(updatedItem),
  });
  if (!response.ok) {
    throw new Error("Network response was not ok");
  }
  return response.json();
}
```

In this example, the `onMutate` function updates the UI optimistically by setting the query data before the server responds. If an error occurs, the `onError` function reverts the data to its previous state. The `onSettled` function invalidates the query after the mutation is complete.

#### Dependent Queries

Sometimes, you might need to fetch data that depends on the result of a previous query. This library handles dependent queries easily:

```jsx
import React from "react";
import { useQuery } from "@tanstack/react-query";

function DependentQueriesComponent() {
  const { data: user } = useQuery("user", fetchUser);
  const userId = user?.id;

  const { data: projects } = useQuery(["projects", userId], fetchProjects, {
    enabled: !!userId,
  });

  return (
    <div>
      <h1>{user?.name}'s Projects</h1>
      <ul>
        {projects?.map((project) => (
          <li key={project.id}>{project.name}</li>
        ))}
      </ul>
    </div>
  );
}

async function fetchUser() {
  const response = await fetch("/api/user");
  if (!response.ok) {
    throw new Error("Network response was not ok");
  }
  return response.json();
}

async function fetchProjects({ queryKey }) {
  const [, userId] = queryKey;
  const response = await fetch(`/api/projects?userId=${userId}`);
  if (!response.ok) {
    throw new Error("Network response was not ok");
  }
  return response.json();
}
```

In this example, the projects query depends on the user query. The userId is extracted from the user data and used to fetch the projects. The `enabled` option ensures that the projects query is only executed when the userId is available.

#### Paginated and Infinite Queries

The library

supports paginated and infinite queries, making it easier to work with large sets of data. Here’s an example of an infinite query:

```jsx
import React from "react";
import { useInfiniteQuery } from "@tanstack/react-query";

function InfiniteQueryComponent() {
  const { data, fetchNextPage, hasNextPage, isFetchingNextPage } =
    useInfiniteQuery("projects", fetchProjects, {
      getNextPageParam: (lastPage, pages) => lastPage.nextCursor,
    });

  return (
    <div>
      {data.pages.map((page, index) => (
        <div key={index}>
          {page.data.map((project) => (
            <p key={project.id}>{project.name}</p>
          ))}
        </div>
      ))}
      <button
        onClick={() => fetchNextPage()}
        disabled={!hasNextPage || isFetchingNextPage}
      >
        {isFetchingNextPage
          ? "Loading more..."
          : hasNextPage
          ? "Load More"
          : "No More Data"}
      </button>
    </div>
  );
}

async function fetchProjects({ pageParam = 0 }) {
  const response = await fetch(`/api/projects?cursor=${pageParam}`);
  if (!response.ok) {
    throw new Error("Network response was not ok");
  }
  return response.json();
}
```

In this example, the `useInfiniteQuery` hook fetches projects in pages, using the `getNextPageParam` function to determine the next cursor for pagination. The `fetchNextPage` function fetches the next page of data, and the `hasNextPage` flag indicates whether there is more data to fetch.

### Benefits

- **Improved Performance**: Optimizes data fetching and caching, resulting in faster load times.
- **Better User Experience**: With background updates and optimistic updates, users experience smoother interactions.
- **Reduced Boilerplate**: Less code to write and maintain for data fetching logic.
- **Enhanced Developer Experience**: DevTools and built-in features streamline development and debugging.

This library is a must-have tool for modern React applications, providing a robust solution for data fetching and state management. Whether you're building simple apps or complex systems, it can help you manage your data more effectively.

For more detailed documentation, visit the [React Query Documentation](https://react-query.tanstack.com/).
