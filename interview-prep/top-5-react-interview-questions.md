---
title: Top 5 React Interview Questions
subtitle:
slug: top-5-react-interview-questions
tags: react, interview-prep
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704197518828/0e-OdBSXE.png?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---

Most frontend Engineering interviews tend to focus on react. Here are most common React Interview Questions

## Explain the Virtual DOM.

The Virtual DOM is a lightweight copy of the actual DOM. React creates a virtual DOM to track changes in the UI in a more efficient way. When a component's state changes, React first updates the virtual DOM. Then, it compares the virtual DOM with the real DOM and updates the real DOM with only the necessary changes, not the entire tree. This selective rendering boosts performance, especially in complex applications.

## Explain Higher-Order Components (HOCs) in React.

Higher-Order Components (HOCs) are advanced techniques in React for reusing component logic. Essentially, a HOC is a function that takes a component and returns a new component. They are used to enhance the functionality of a component and can be used for a variety of tasks like data fetching, rendering conditional UI, etc.

```
import React from 'react';

function withLogging(WrappedComponent) {
  return class extends React.Component {
    componentDidMount() {
      console.log(`Logged: ${WrappedComponent.name}`);
    }

    render() {
      return <WrappedComponent {...this.props} />;
    }
  };
}

class MyComponent extends React.Component {
  render() {
    // Render something based on props
  }
}

export default withLogging(MyComponent);
```

## Explain the concept of Context in React.

The Context API in React is a way to pass data through the component tree without having to pass props down manually at every level. It's used for sharing data that can be considered “global” for a tree of React components, like authenticated user, theme, or preferred language.


```
import React, { useContext } from 'react';

const ThemeContext = React.createContext('light');

function ThemedButton() {
  const theme = useContext(ThemeContext);
  return <button className={theme}>I am styled by theme context!</button>;
}

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <ThemedButton />
    </ThemeContext.Provider>

```
## How do you optimize performance in a React application?

Performance optimization in React can involve various strategies like using React.memo() for memoizing components, implementing lazy loading with React.lazy() and Suspense, avoiding unnecessary re-renders by using shouldComponentUpdate or React.PureComponent, optimizing state and props to minimize component updates, using code splitting to reduce the size of the initial load, and efficiently managing state for global state management.

## How would you implement error boundaries in React?

Error boundaries are React components that catch JavaScript errors in their child component tree, log those errors, and display a fallback UI. They are a way to gracefully handle errors in the UI.

```
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // Log or handle the error
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong.</h1>;
    }
    return this.props.children;
  }
}

// Usage
<ErrorBoundary>
  <MyComponent />
</ErrorBoundary>
```


Happy coding and good luck with your interview! 