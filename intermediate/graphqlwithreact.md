---
title: "Connect GraphQL with React - 2 ways"

subtitle: "Learn how to connect GraphQL with react using Apollo Client and Axios"

slug: "connect-graphql-with-react"

tags: web-development, frontend, react, graphql, apollo-server, axios, react query

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1713008652382/lrfb685fU.webp?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

## What is GraphQL?

GraphQL is a query language designed for APIs, as well as a server-side runtime for executing queries. It differs significantly from REST in that it allows clients to precisely define the data they need, which can minimize data over-fetching and under-fetching issues.

### What is a Query?

In GraphQL, a "query" is used to fetch data. Unlike REST where you would typically retrieve data from a specific endpoint, GraphQL queries are sent to a single endpoint and are crafted to specify exactly what data is needed, no more, no less. This is one of the core features of GraphQL that eliminates the inefficiency of downloading unnecessary data.

### What is a Mutation?

In GraphQL, a "mutation" is used to insert, update, or delete data. This is analogous to POST, PUT, DELETE in REST. Mutations ensure that you can manage your data effectively, providing clear patterns for client-server interaction.

## Fetch and Mutate Data with Apollo Client

### Install Apollo Client

```bash
npm install @apollo/client graphql
```

### Connect Your React App with Apollo

In your main React file (usually `index.js`), import the necessary Apollo Client libraries to initialize the client and wrap your React app:

```javascript
import React from "react";
import ReactDOM from "react-dom";
import { ApolloClient, InMemoryCache, ApolloProvider } from "@apollo/client";
import App from "./App";

// Initialize Apollo Client
const client = new ApolloClient({
  uri: "YOUR_GRAPHQL_API_ENDPOINT",
  cache: new InMemoryCache(),
});

// Wrap your React app with ApolloProvider
ReactDOM.render(
  <ApolloProvider client={client}>
    <App />
  </ApolloProvider>,
  document.getElementById("root")
);
```

- **ApolloClient** is the core mechanism for interacting with a GraphQL server, handling data fetching, caching, and state management of GraphQL queries.
- **InMemoryCache** is a cache implementation used by Apollo Client to store and manage the results of GraphQL queries efficiently, enhancing performance by reusing data.
- **ApolloProvider** is a React component that leverages React's Context API to provide the Apollo Client instance to all components within an application, enabling any component to access and operate GraphQL data.

### Fetching Data with GraphQL in React

### Install Apollo Client

```bash
npm install @apollo/client graphql
```

#### Step 1: Define a Query

```graphql
query GetUsers {
  users {
    id
    name
    email
  }
}
```

#### Step 2: Use the Query

You can use the `useQuery` hook from Apollo Client to execute this query in your component:

```javascript
import { useQuery, gql } from "@apollo/client";

const GET_USERS = gql`
  query GetUsers {
    users {
      id
      name
      email
    }
  }
`;

function Users() {
  const { loading, error, data } = useQuery(GET_USERS);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error :(</p>;

  return data.users.map(({ id, name, email }) => (
    <div key={id}>
      <p>{`${name}: ${email}`}</p>
    </div>
  ));
}

export default Users;
```

- **useQuery** is a React hook from Apollo Client used to execute a GraphQL query and manage the response lifecycle, including loading, error handling, and data retrieval.
- **loading** is a boolean flag indicating whether the query is actively fetching data, useful for displaying loading indicators in your UI.
- **error** contains an error object if an error occurred during the query, enabling error handling and user notifications in the UI.
- **data** holds the actual data returned by the GraphQL query, structured as per your query, which you use to render results in your UI.

### Adding Data with GraphQL Mutations

#### Step 1: Define a Mutation

```graphql
mutation AddUser($name: String!, $email: String!) {
  addUser(name: $name, email: $email) {
    id
    name
    email
  }
}
```

#### Step 2: Use the Mutation

In React, you can use the `useMutation` hook from Apollo Client to handle this mutation.

```javascript
import { useMutation, gql } from "@apollo/client";

const ADD_USER = gql`
  mutation AddUser($name: String!, $email: String!) {
    addUser(name: $name, email: $email) {
      id
      name
      email
    }
  }
`;

function AddUserForm() {
  let inputName, inputEmail;
  const [addUser, { data, loading, error }] = useMutation(ADD_USER);

  if (loading) return "Submitting...";
  if (error) return `Submission error! ${error.message}`;

  return (
    <div>
      <form
        onSubmit={(e) => {
          e.preventDefault();
          addUser({
            variables: { name: inputName.value, email: inputEmail.value },
          });
          inputName.value = "";
          inputEmail.value = "";
        }}
      >
        <input
          ref={(node) => {
            inputName = node;
          }}
          placeholder="Name"
        />
        <input
          ref={(node) => {
            inputEmail = node;
          }}
          placeholder="Email"
        />
        <button type="submit">Add User</button>
      </form>
      {data && <p>Saved! User {data.addUser.name} created.</p>}
    </div>
  );
}

export default AddUserForm;
```

- **`useMutation`** is a React hook from Apollo Client used for executing GraphQL mutations such as `ADD_USER`, managing the mutation lifecycle including state changes like loading, success, and error states.
- **`addUser`** is the function returned by `useMutation` for invoking the `ADD_USER` mutation, allowing you to send the mutation to your GraphQL server with appropriate variables, such as user input data

## Fetch and Mutate Data with Axios + React Query

### Install Axios and React Query

```bash
npm install axios react-query
```

### Fetching Data with Axios and React Query

To fetch data using Axios within React Query, you define a query using the `useQuery` hook, where the query function utilizes Axios to send a POST request to your GraphQL server. Here's an example setup:

```javascript
import { useQuery } from "react-query";
import axios from "axios";

const getGraphQLData = async () => {
  const query = `
    query GetUsers {
      users {
        id
        name
        email
      }
    }
  `;
  const { data } = await axios.post(
    "https://your-graphql-endpoint.com/graphql",
    {
      query,
    }
  );
  return data.data; // Note: Axios nests the response in 'data' property
};

function UsersComponent() {
  const { data, error, isLoading } = useQuery("users", getGraphQLData);

  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>An error occurred: {error.message}</div>;

  return (
    <ul>
      {data.users.map((user) => (
        <li key={user.id}>
          {user.name} - {user.email}
        </li>
      ))}
    </ul>
  );
}
```

In this example, `useQuery` manages the fetching, caching, and state of the query. Axios handles the API call, while React Query provides the hooks to integrate the fetched data into your React component with support for loading and error states.

### Mutating Data with Axios and React Query

For mutations, you can use the `useMutation` hook from React Query. This allows you to execute mutation operations triggered by user actions, such as form submissions. Here is how you might set up a mutation to add a user:

```javascript
import { useMutation } from "react-query";
import axios from "axios";

const addUser = async (userData) => {
  const mutation = `
    mutation AddUser($name: String!, $email: String!) {
      addUser(name: $name, email: $email) {
        id
        name
        email
      }
    }
  `;
  const { data } = await axios.post(
    "https://your-graphql-endpoint.com/graphql",
    {
      query: mutation,
      variables: userData,
    }
  );
  return data.data.addUser;
};

function AddUserForm() {
  const mutation = useMutation(addUser);

  const handleSubmit = (event) => {
    event.preventDefault();
    const formData = new FormData(event.target);
    const userData = {
      name: formData.get("name"),
      email: formData.get("email"),
    };
    mutation.mutate(userData);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="name" required placeholder="Name" />
      <input name="email" required placeholder="Email" />
      <button type="submit">Add User</button>
      {mutation.isLoading && <p>Adding user...</p>}
      {mutation.isError && <p>Error: {mutation.error.message}</p>}
      {mutation.isSuccess && <p>User added!</p>}
    </form>
  );
}
```

In this setup, `useMutation` is used to define a mutation operation. The `mutate` method from the `useMutation` hook triggers the actual mutation call with the necessary user data, managed by Axios. React Query then handles the asynchronous state of the mutation, providing feedback on the mutation's progress and outcome.

## What to choose ?

- **Choose Axios + React Query** if you need a flexible solution that handles more than just GraphQL, require precise control over HTTP requests, or you’re integrating GraphQL in a project that already uses React Query for data fetching.
- **Choose Apollo Client** if your project is heavily based on GraphQL, benefits from built-in state management features, and you prefer a more integrated, less boilerplate solution that is optimized for complex GraphQL operations and real-time updates.
