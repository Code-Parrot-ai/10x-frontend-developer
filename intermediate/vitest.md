---
title: "Test your React Apps with Vitest"

subtitle: "Unlock Faster, More Efficient Testing in Your React Projects with Vitest."

slug: "test-react-apps-vitest"

tags: web development, react, testing, vitest, jest, enzyme, react-testing-library

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711086016516/2Y-hgrmMQ.webp?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

### What is React Testing? 🤔

React testing refers to the process of verifying the functionality and performance of React components and applications. It involves simulating user interactions, validating component outputs, and ensuring that the application behaves as expected under various conditions.

### Testing Frameworks in the React Ecosystem 🛠️

- **Jest**: A comprehensive testing solution developed by Facebook that provides built-in test runners, assertion libraries, and mocking support. Jest is widely used for its simplicity and support for snapshot testing.
- **Mocha**: Another powerful testing framework that is flexible and configurable, with a rich plugin ecosystem. Mocha requires an assertion library like Chai to be fully functional.
- **Enzyme**: A testing utility developed by Airbnb for React applications. Enzyme makes it easier to assert, manipulate, and traverse your React Components' output.
- **React Testing Library**: Part of the Testing Library family, it provides light utility functions on top of React DOM and React DOM Test Utils, encouraging better testing practices by focusing on component outputs rather than implementation details.

### Why Vitest? 🚀

#### Speed and Efficiency

Vitest is designed from the ground up to take advantage of Vite's fast module reloading, resulting in significantly quicker test runs. This speed is further enhanced by parallel test execution and efficient caching, making Vitest an excellent choice for large projects.

#### Jest Compatibility

For teams already familiar with Jest, Vitest offers an easy transition path. Its API is compatible with Jest, meaning that in many cases, tests can be migrated with minimal changes. This compatibility allows teams to leverage Vitest’s performance benefits without a steep learning curve.

#### Modern JavaScript Support

Vitest is built with modern JavaScript frameworks in mind. It supports ES modules natively, allowing for straightforward configuration and integration into projects that use modern JavaScript features and syntax. This makes it particularly well-suited for projects using Vite as their build tool.

#### Rich Feature Set

Vitest doesn’t compromise on features for the sake of speed. It includes a full suite of testing utilities, including snapshot testing, test coverage, mocking, and assertions.

### Getting Started with Vitest in a React Project

To integrate Vitest into your React project, you’ll first need to ensure that your project is set up with Vite. Once that’s in place, follow these steps to add Vitest:

1.  **Installation**: Begin by installing Vitest along with the required testing libraries. You can do so by running:

```bash

npm  install  vitest  react-testing-library  @testing-library/jest-dom  --save-dev

```

2.  **Configuration**: Next, configure Vitest to work with your React components. Create a `vite.config.ts` file (or modify the existing one) to include Vitest’s plugin:

```javascript
import { defineConfig } from "vite";

import react from "@vitejs/plugin-react";

import { viteSingleFile } from "vite-plugin-singlefile";

import { visualizer } from "rollup-plugin-visualizer";

import { defineConfig } from "vitest/config";

export default defineConfig({
  plugins: [react(), viteSingleFile(), visualizer()],

  test: {
    // Vitest configuration options

    globals: true,

    environment: "jsdom",
  },
});
```

3.  **Writing Your First Test**: With Vitest configured, it’s time to write your first test. For example, if you have a simple `Button` component, you can test it like this:

```javascript
import { describe, it, expect } from "vitest";

import { render, screen } from "@testing-library/react";

import Button from "../Button";

describe("Button", () => {
  it("renders correctly", () => {
    render(<Button>Click me</Button>);

    expect(screen.getByRole("button")).toHaveTextContent("Click me");
  });
});
```

This test renders the `Button` component and asserts that it contains the correct text.

4.  **Running Tests**: To run your tests, add a script to your `package.json`:

```json

"scripts": {

"test":  "vitest"

}

```

Then, execute `npm run test` in your terminal. Vitest will run the tests and provide you with instant feedback.

### Component Testing with Vitest

Component testing focuses on testing the behavior of React components in isolation. Let's test a `TodoItem` component that displays a todo's text and a checkbox to mark the todo as completed.

**TodoItem Component:**

```jsx
function TodoItem({ todo, onToggle }) {
  return (
    <div>
      <input
        type="checkbox"
        checked={todo.completed}
        onChange={() => onToggle(todo.id)}
      />
      <span>{todo.text}</span>
    </div>
  );
}
```

**Test for TodoItem Component:**

```javascript
import { describe, it, expect } from "vitest";
import { render, fireEvent, screen } from "@testing-library/react";
import TodoItem from "../components/TodoItem";

describe("TodoItem", () => {
  it("displays the todo and reacts to the checkbox toggle", async () => {
    const mockToggle = vitest.fn();
    const todo = { id: 1, text: "Learn Vitest", completed: false };

    render(<TodoItem todo={todo} onToggle={mockToggle} />);

    // Check if the todo text is displayed
    expect(screen.getByText("Learn Vitest")).toBeInTheDocument();

    // Toggle the checkbox
    fireEvent.click(screen.getByRole("checkbox"));
    expect(mockToggle).toHaveBeenCalledWith(1);
  });
});
```

### Unit Testing with Vitest

Unit testing involves testing the smallest parts of an application in isolation (e.g., functions). Let's test a simple utility function that filters completed todos.

**filterCompletedTodos Function:**

```javascript
function filterCompletedTodos(todos) {
  return todos.filter((todo) => todo.completed);
}
```

**Test for filterCompletedTodos Function:**

```javascript
import { describe, it, expect } from "vitest";
import { filterCompletedTodos } from "../utils/todoUtils";

describe("filterCompletedTodos", () => {
  it("filters completed todos correctly", () => {
    const todos = [
      { id: 1, text: "Learn React", completed: false },
      { id: 2, text: "Learn Vitest", completed: true },
    ];

    const filtered = filterCompletedTodos(todos);
    expect(filtered).toHaveLength(1);
    expect(filtered[0].id).toBe(2);
  });
});
```

### Testing Hooks with Vitest

Testing React hooks allows you to ensure your custom hooks behave as expected. Let's test a custom hook `useCounter` that provides functionality to increment, decrement, and reset a counter.

**useCounter Hook:**

```javascript
import { useState } from "react";

function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);

  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);
  const reset = () => setCount(initialValue);

  return { count, increment, decrement, reset };
}
```

**Test for useCounter Hook:**

To test custom hooks, we can use the `@testing-library/react-hooks` library, which enables you to render hooks in a testing environment.

```javascript
import { describe, it, expect } from "vitest";
import { renderHook, act } from "@testing-library/react-hooks";
import useCounter from "../hooks/useCounter";

describe("useCounter", () => {
  it("should use counter", () => {
    const { result } = renderHook(() => useCounter());

    expect(result.current.count).toBe(0);

    act(() => {
      result.current.increment();
    });

    expect(result.current.count).toBe(1);

    act(() => {
      result.current.decrement();
    });

    expect(result.current.count).toBe(0);

    act(() => {
      result.current.reset();
    });

    expect(result.current.count).toBe(0);
  });

  it("should accept initial count", () => {
    const { result } = renderHook(() => useCounter(10));

    expect(result.current.count).toBe(10);
  });
});
```

For more detailed information on Vitest, refer to the [official documentation](https://vitest.dev/).
