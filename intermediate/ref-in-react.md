---
title: Use Ref in React - the right way
subtitle:
slug: ref-in-react
tags: ref, react
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704188938555/r24RCXG2P.png?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---

React offers a powerful feature called 'ref.' Understanding how to use ref correctly is essential for React developers. In this article, we will explore the basics of ref, common pitfalls to avoid, and advanced use cases

## Basics of Ref in React

### What is Ref?

A ref in React provides a way to access the DOM nodes or React elements created in the render method. It's used when you need direct access to a DOM node, for things like managing focus, text selection, or media playback.

### Creating Refs

Refs are created using React.createRef() and attached to React elements via the ref attribute. Refs are commonly used in class components, but with the advent of React Hooks, you can also use them in functional components using useRef.

**Example in Class Component**

```
class MyComponent extends React.Component {
constructor(props) {
    super(props);
    this.myRef = React.createRef();
}

render() {
    return <div ref={this.myRef} />;
}
}

```


**Example in Functional Component**

### Accessing Refs

Once assigned to a component, you can access the ref's current property to get the DOM node.

```
componentDidMount() {
  const node = this.myRef.current;
  // You can now directly access the DOM element.
}
```

## Common Pitfalls and How to Avoid Them

1. Overusing Refs for Tasks that Should Be Handled by React's State Management

Pitfall: Using refs to manipulate the DOM for tasks like updating the UI, which should ideally be handled by React's state and props.

**Example:**

```
class BadExample extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();
  }

  updateText() {
    // Directly manipulating the DOM — not recommended!
    this.myRef.current.textContent = "Updated text!";
  }

  render() {
    return (
      <div>
        <div ref={this.myRef}>Initial text</div>
        <button onClick={() => this.updateText()}>Update Text</button>
      </div>
    );
  }
}

```

Why It's a Pitfall: This approach bypasses React's state management and rendering lifecycle, potentially leading to unsynchronized states and unpredictable UI behaviours.

2. Using Refs with Functional Components Incorrectly

Pitfall: Trying to attach refs to functional components without using React.forwardRef.

**Example:**

```
function MyFunctionalComponent() {
  return <div>Content</div>;
}

class ParentComponent extends React.Component {
  constructor(props) {
    super(props);
    this.myRef = React.createRef();
  }

  componentDidMount() {
    console.log(this.myRef.current); // Will be null
  }

  render() {
    // Incorrectly trying to attach ref to a functional component
    return <MyFunctionalComponent ref={this.myRef} />;
  }
}

```

Why It's a Pitfall: Functional components don't have instances, so the ref will be null. It leads to errors or unexpected behaviors.

3. Updating State on Ref Callbacks

Pitfall: Updating component state within a ref callback, causing potential re-renders or performance issues.

**Example:**

```
class BadRefUsage extends React.Component {
  constructor(props) {
    super(props);
    this.state = { height: 0 };
    this.myRef = (element) => {
      if (element) {
        // Incorrectly setting state in a ref callback
        this.setState({ height: element.clientHeight });
      }
    };
  }

  render() {
    return <div ref={this.myRef}>Content</div>;
  }
}

```

Why It's a Pitfall: The ref callback is not the right place to update the state, as it can be called multiple times before a component mounts and may lead to redundant re-renders or unexpected behaviour.

## Use Cases

### Integrating with Third-Party DOM Libraries

When integrating with libraries that manipulate the DOM, such as jQuery plugins, refs provide a way to give the library direct access to a DOM node.

```
componentDidMount() {
  $(this.myRef.current).pluginMethod();
}
```

### Managing Focus, Text Selection, or Media Playback

Refs are ideal for managing focus, text selection, or controlling media playback, as these actions often require direct manipulation of the DOM.

```
focusTextInput() {
  this.textInput.current.focus();
}
```

### Measuring DOM Node

Sometimes you need to measure a node's size or position. Refs make this straightforward:

```
measureNode() {
  const dimensions = this.nodeRef.current.getBoundingClientRect();
  // You can now access size and position of the node.
}
```

