---
title: Beyond Redux - Navigating the World of State Management

subtitle: A Comparative Guide to MobX and Zustand for Modern JavaScript Applications.

slug: "state-management-with-mobx-zustand"

tags: javascript, statemanagement, reduxalternatives, mobx, zustand, webdevelopment, frontenddevelopment, reactjs, softwareengineering, programming

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705069331226/ZEnr9aHDE.png?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

## Introduction

State management is a critical component of JavaScript application development, and Redux has been a dominant player in this arena. However, with the evolution of the JavaScript ecosystem, alternatives like MobX and Zustand have emerged, offering different approaches and philosophies. This blog aims to explore these alternatives, shedding light on their features and appropriate use cases.

## Brief about Redux

Redux is a state management library that combines Flux architecture with functional programming concepts. Its main feature is the use of a single store as a source of truth, with a state that is immutable. It enforces unidirectional data flow, where state is read-only and changes are made through pure functions called reducers. Changes to the state are done through actions and reducers. Redux is well-suited for complex applications due to its predictable state management, but it often requires more boilerplate code​. For more information visit [this blog](https://10xdev.codeparrot.ai/react-state-secrets-unveiling-the-power-of-context-and-redux).

## MobX

MobX uses transparent functional reactive programming (TFRP) to make state management simple and scalable. Unlike Redux, it allows for multiple stores and employs mutable state, which can lead to more straightforward state updates but might complicate debugging and testing. Reactions in MobX automatically track changes in observables and update the UI or other parts of the application accordingly. MobX is efficient and performs well, particularly in scenarios where fine-grained event listeners are beneficial.

**Internal Structure:**

- **Observables:** The core of MobX, these are the data structures that store the application's state.
- **Actions:** Functions that modify observables. In MobX, actions are not as rigidly structured as in Redux.
- **Computed Values:** Derived values that automatically update when their dependencies change.
- **Reactions:** Automatic processes that run when observables they depend on change (e.g., re-rendering UI components).

**MobX Example:**
First, let's set up a basic MobX store for managing a to-do list:

```javascript
import { makeAutoObservable } from "mobx";

class TodoStore {
  todos = [];

  constructor() {
    makeAutoObservable(this);
  }

  addTodo = (todo) => {
    this.todos.push({ text: todo, completed: false });
  };

  toggleTodo = (index) => {
    this.todos[index].completed = !this.todos[index].completed;
  };
}

export const todoStore = new TodoStore();
```

Now, we'll use this store in a React component:

```jsx
import React, { useState } from "react";
import { observer } from "mobx-react-lite";
import { todoStore } from "./TodoStore";

const TodoList = observer(() => {
  const [newTodo, setNewTodo] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault();
    todoStore.addTodo(newTodo);
    setNewTodo("");
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          value={newTodo}
          onChange={(e) => setNewTodo(e.target.value)}
        />
        <button type="submit">Add Todo</button>
      </form>
      <ul>
        {todoStore.todos.map((todo, index) => (
          <li key={index} onClick={() => todoStore.toggleTodo(index)}>
            {todo.text} {todo.completed ? "(completed)" : ""}
          </li>
        ))}
      </ul>
    </div>
  );
});

export default TodoList;
```

For more code examples visit the documentation [here](https://mobx.js.org/README.html).

## Zustand

Zustand is a minimalistic state management solution known for its simplicity and ease of use. It's lightweight and performs well in smaller projects or for developers who prefer a more straightforward solution. While it lacks the extensive ecosystem and community support of Redux, Zustand's simplicity makes it a good choice for projects where a more structured and opinionated approach like Redux is not necessary​

**Internal Structure:**

- **Store:** A small, flexible state container. Each store is a hook itself.
- **Set Function:** Used to update the state directly, without the need for actions or reducers.
- **Selectors:** Functions to select a part of the state and subscribe components to changes in that part.

**Zustand Example:**
First, let's create a Zustand store:

```javascript
import create from "zustand";

const useStore = create((set) => ({
  todos: [],
  addTodo: (todo) =>
    set((state) => ({
      todos: [...state.todos, { text: todo, completed: false }],
    })),
  toggleTodo: (index) =>
    set((state) => {
      const newTodos = [...state.todos];
      newTodos[index].completed = !newTodos[index].completed;
      return { todos: newTodos };
    }),
}));

export default useStore;
```

Now, we'll use the Zustand store in a React component:

```jsx
import React, { useState } from "react";
import useStore from "./TodoStore";

const TodoList = () => {
  const [newTodo, setNewTodo] = useState("");
  const { todos, addTodo, toggleTodo } = useStore();

  const handleSubmit = (e) => {
    e.preventDefault();
    addTodo(newTodo);
    setNewTodo("");
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          value={newTodo}
          onChange={(e) => setNewTodo(e.target.value)}
        />
        <button type="submit">Add Todo</button>
      </form>
      <ul>
        {todos.map((todo, index) => (
          <li key={index} onClick={() => toggleTodo(index)}>
            {todo.text} {todo.completed ? "(completed)" : ""}
          </li>
        ))}
      </ul>
    </div>
  );
};

export default TodoList;
```

For more code examples visit the documentation [here](https://github.com/pmndrs/zustand)

## Section 4: Comparison and Use Cases

| Feature / Aspect        | Redux                                 | MobX                                     | Zustand                                |
| ----------------------- | ------------------------------------- | ---------------------------------------- | -------------------------------------- |
| **Philosophy**          | Predictable state container           | Reactive state management                | Minimalistic state management          |
| **State Management**    | Unidirectional, centralized           | Observable, decentralized                | Simplistic, decentralized              |
| **Boilerplate**         | High (actions, reducers, middleware)  | Low (automatic reactions)                | Very Low                               |
| **Learning Curve**      | Steep                                 | Moderate                                 | Easy                                   |
| **Performance**         | Good for large-scale apps             | Optimized for individual components      | Fast for small to medium apps          |
| **Scalability**         | Highly scalable                       | Scalable with complexity                 | Best for small to medium projects      |
| **Flexibility**         | Structured, less flexible             | Highly flexible                          | Extremely flexible                     |
| **Integration**         | Primarily with React, but adaptable   | Broad (React, Angular, Vue, etc.)        | Mainly React                           |
| **Community & Support** | Very large and established            | Large and growing                        | Smaller but active                     |
| **Use Case**            | Large applications with complex state | Projects needing fine-grained reactivity | Small to medium apps with simple state |

## Conclusion

- **Use Redux** when working on large-scale projects where predictability, maintainability, and scalability are critical. Its structured approach is beneficial for teams needing a robust framework for managing complex state.
- **Use MobX** for projects where you need a more straightforward and less boilerplate-heavy approach. It's suitable for applications with complex state changes but where the scale does not justify the overhead of Redux.
- **Use Zustand** for smaller projects or when development speed and simplicity are priorities. It's ideal for cases where a lightweight state management solution is sufficient.

Redux is a robust, scalable solution for complex applications, MobX offers simplicity and efficiency for moderate complexity, and Zustand provides minimalism and ease of use for smaller, less complex projects.
