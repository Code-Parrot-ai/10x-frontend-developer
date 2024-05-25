---
title: "Optimize React Components with the React Profiler 🚀"

subtitle: "Discover how to use React Profiler to find and fix performance issues in your React applications."

slug: "optimize-react-components-with-the-react-profiler"

tags: react, performance, optimization, react-profiler, react-memo, usecallback

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1716613534464/I38p952Do.png?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

Imagine you're working on a complex React application that feels sluggish and unresponsive. Users are complaining about slow load times and laggy interactions. You suspect that some components are rendering more frequently than they should, but pinpointing the exact problem is challenging. This is where the React Profiler comes in handy.

## A Real-World Example

Let's consider a simple application that displays a list of items and allows users to add new items. Here's the initial implementation:

```jsx
import React, { useState } from "react";

function App() {
  const [items, setItems] = useState([]);
  const [newItem, setNewItem] = useState("");

  const addItem = () => {
    setItems([...items, newItem]);
    setNewItem("");
  };

  return (
    <div>
      <input
        type="text"
        value={newItem}
        onChange={(e) => setNewItem(e.target.value)}
      />
      <button onClick={addItem}>Add Item</button>
      <ItemList items={items} />
    </div>
  );
}

function ItemList({ items }) {
  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
}

export default App;
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716604568729/fnYHCuAAG.png?auto=format)

The application works, but as the number of items grows, you notice that it becomes slow, especially when adding new items. The issue is that the `ItemList` component re-renders every time a new item is added, even if the list of items hasn't changed.

## Introducing React Profiler

To diagnose and fix this issue, we can use the React Profiler to measure the performance of our components.

### Adding the Profiler to Your Code

First, let's wrap the `ItemList` component with the `<Profiler>` component:

```jsx
import React, { Profiler, useState } from "react";

function App() {
  const [items, setItems] = useState([]);
  const [newItem, setNewItem] = useState("");

  const addItem = () => {
    setItems([...items, newItem]);
    setNewItem("");
  };

  const onRenderCallback = (
    id,
    phase,
    actualDuration,
    baseDuration,
    startTime,
    commitTime,
    interactions
  ) => {
    console.log(`Profiling ${id}:`, {
      phase,
      actualDuration,
      baseDuration,
      startTime,
      commitTime,
      interactions,
    });
  };

  return (
    <div>
      <input
        type="text"
        value={newItem}
        onChange={(e) => setNewItem(e.target.value)}
      />
      <button onClick={addItem}>Add Item</button>
      <Profiler id="ItemList" onRenderCallback={onRenderCallback}>
        <ItemList items={items} />
      </Profiler>
    </div>
  );
}

function ItemList({ items }) {
  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
}

export default App;
```

### Analyzing the Results

After adding the Profiler, interact with your application by adding new items. Open the Profiler tab in the React Developer Tools to see a timeline of your component renders. You'll likely see that the `ItemList` component is re-rendering more often than necessary.

## Optimizing with React.memo

To prevent unnecessary re-renders, we can use `React.memo` to memoize the `ItemList` component:

```jsx
import React, { Profiler, useState, memo } from "react";

function App() {
  const [items, setItems] = useState([]);
  const [newItem, setNewItem] = useState("");

  const addItem = () => {
    setItems([...items, newItem]);
    setNewItem("");
  };

  const onRenderCallback = (
    id,
    phase,
    actualDuration,
    baseDuration,
    startTime,
    commitTime,
    interactions
  ) => {
    console.log(`Profiling ${id}:`, {
      phase,
      actualDuration,
      baseDuration,
      startTime,
      commitTime,
      interactions,
    });
  };

  return (
    <div>
      <input
        type="text"
        value={newItem}
        onChange={(e) => setNewItem(e.target.value)}
      />
      <button onClick={addItem}>Add Item</button>
      <Profiler id="ItemList" onRenderCallback={onRenderCallback}>
        <MemoizedItemList items={items} />
      </Profiler>
    </div>
  );
}

const ItemList = ({ items }) => {
  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
};

const MemoizedItemList = memo(ItemList);

export default App;
```

### Using `useCallback` to Memoize Functions

To further optimize, avoid passing anonymous functions as props, which can cause components to re-render. Use `useCallback` to memoize functions:

```jsx
import React, { Profiler, useState, useCallback, memo } from "react";

function App() {
  const [items, setItems] = useState([]);
  const [newItem, setNewItem] = useState("");

  const addItem = useCallback(() => {
    setItems((prevItems) => [...prevItems, newItem]);
    setNewItem("");
  }, [newItem]);

  const onRenderCallback = (
    id,
    phase,
    actualDuration,
    baseDuration,
    startTime,
    commitTime,
    interactions
  ) => {
    console.log(`Profiling ${id}:`, {
      phase,
      actualDuration,
      baseDuration,
      startTime,
      commitTime,
      interactions,
    });
  };

  return (
    <div>
      <input
        type="text"
        value={newItem}
        onChange={(e) => setNewItem(e.target.value)}
      />
      <button onClick={addItem}>Add Item</button>
      <Profiler id="ItemList" onRenderCallback={onRenderCallback}>
        <MemoizedItemList items={items} />
      </Profiler>
    </div>
  );
}

const ItemList = ({ items }) => {
  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
};

const MemoizedItemList = memo(ItemList);

export default App;
```

## Conclusion

The React Profiler helps you find and fix performance issues in your React apps. By using `React.memo` and `useCallback`, you can optimize components and create a smoother user experience. Happy coding!

For more details, visit the [official React Profiler documentation](https://reactjs.org/docs/profiler.html).
