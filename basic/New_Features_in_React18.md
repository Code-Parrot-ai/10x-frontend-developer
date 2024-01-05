---
title: New Features in React 18
subtitle: React 18 brings transformative enhancements and optimizations, significantly boosting application performance for developers using this leading JavaScript library.
slug: new-features-in-react18
tags: new features, react, javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704442009349/h6uMl00eI.webp?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---

# WHAT'S NEW IN REACT 18?

In this blog, we will delve into the exciting new features that React 18 brings to the table. We'll take a closer look at how these enhancements, including concurrent rendering, automatic batching, and the new useId hook, are set to revolutionize the way developers build and optimize their applications. This deep dive will not only highlight the technical aspects but also discuss the practical implications of these advancements, offering insights into how they can be effectively utilized in real-world projects. Join us as we explore the cutting-edge developments in React 18, a significant leap forward for this widely-used JavaScript library.

# WHAT IS CONCURRENT REACT?

React 18 introduces Concurrent React, a significant update to its core rendering model. This new feature offers interruptible rendering, allowing React to manage UI updates more efficiently. Unlike previous synchronous models, Concurrent React can pause, resume, or abandon ongoing renders while ensuring UI consistency. This leads to a responsive UI, capable of handling user input smoothly even during complex rendering tasks.

Concurrent React also manages reusable state effectively. For instance, it can remember and restore UI states, even when sections are removed and later added back. The upcoming <Offscreen> component will further enhance this, enabling background preparation of new UI elements.

Key features built on this new model include Suspense, transitions, and streaming server rendering. With React 18, developers can immediately use concurrent features like startTransition for smoother screen navigation and useDeferredValue for controlling re-renders.

The long-term goal is to integrate concurrency more seamlessly into applications, mainly through libraries and frameworks. As the ecosystem evolves, new APIs are provided for libraries to adapt to these concurrent features. This transition may take time, and patience is advised as library maintainers work to update their tools.

## SUSPENSE IN REACT 18

React 18 introduces Suspense, a feature utilizing the new concurrent rendering engine, designed to create more responsive user interfaces and optimize browser resources. This advancement changes how React handles rendering decisions based on component state changes, allowing for efficient UI updates without full server-induced page rerenders.

Suspense particularly improves scenarios like updating lists amid user interactions, such as typing in a filter box. Traditional React might lead to sluggish experiences and high resource usage due to multiple list item updates. In contrast, Concurrent React with Suspense ensures smoother, more resource-efficient performance.

This is how we write Suspense in our code:

```
<Suspense fallback={<Loading />}>
 <SomeComponent />
</Suspense>
```

### Without Suspense:

n a scenario without Suspense and Concurrent Rendering, fetching external data involves programmatically managing loading states. The typical approach includes fetching data, checking loading state, and displaying it in the UI once fully retrieved. An example code snippet illustrates this process for a CityList component.

```
function CityList() {
  const [data, setData] = useState();
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    setIsLoading(true);
    fetchCities().then((records) => {
      setData(records);
      setIsLoading(false);
    });
  }, []);

  if (isLoading) return <div>Loading cities...</div>;

  return (
    <ul>
      {data.map(({ id, name }) => (
        <li key={id}>{name}</li>
      ))}
    </ul>
  );
}
```

### With Suspense:

React 18's Suspense and Concurrent Rendering simplifies data fetching by using a Suspense wrapper with a fallback UI for loading states. The data-fetching component uses a special promise resource, enabling the Concurrent rendering engine to optimize re-rendering based on completed external calls. This approach, exemplified in a CityList component, eliminates complex loading state tracking, particularly useful in scenarios involving multiple external data sources.

## AUTOMATIC BATCHING

Automatic batching in React groups multiple state updates from various sources like promises, setTimeout, and native event handlers into a single re-render, enhancing performance. This extends beyond the previously limited batching within React event handlers.

```
// Before: only React events were batched.
setTimeout(() => {
 setCount(c => c + 1);
 setFlag(f => !f);
 // React will render twice, once for each state update (no batching)
}, 1000);

// After: updates inside of timeouts, promises,
// native event handlers or any other event are batched.
setTimeout(() => {
 setCount(c => c + 1); // Does not re-render yet
 setFlag(f => !f); // Does not re-render yet
 // React will only re-render once at the end (that's batching!)
}, 1000);

```

This is great for performance because it avoids unnecessary re-renders. It also prevents your component from rendering “half-finished” states where only one state variable was updated, which may cause bugs. This might remind you of how a restaurant waiter doesn’t run to the kitchen when you choose the first dish, but waits for you to finish your order.

## TRANSITIONS

We have 2 types of transitions. Urgent transitions and non-urgent transitions.

### Urgent Transitions:

Urgent transitions are transitions that the user needs to see instantly. For example, if the user changes their profile name and saves it, they should be able to see the change in the displayed profile name in the navigation bar.
Urgent transitions are done the same way you've been setting a state before:

```
const [name, setName] = useState('');

function handleChange (e) {
	setName(e.target.value); //urgent transition
}
```

### Non-Urgent Transitions:

Non-urgent transitions are transitions that are ok to be delayed a little. For example, if the user is performing a search, it's ok for the results to appear not so instantly.

There are 2 ways to start a non-urgent transition. The first one is using the hook useTransition:

```
import {useTransition, useState} from 'react';

export default function MyApp() {
    const [results, setResults] = useState([]);
    const [pending, startTransition] = useTransition();

    function handleChange(e) {
        let tempResults = [];
        ... // set results from APIs
        startTransition(() => {
            setResults(tempResults);
        });
    }
}
```

In React, urgent updates are immediate responses to direct interactions like typing or clicking. Transition updates, on the other hand, are for transitioning the UI between views, like loading new filter results. For optimal user experience, user inputs often trigger both urgent and non-urgent updates. The startTransition API helps differentiate these, marking non-urgent updates as "transitions" to manage rendering priorities effectively.

```
import { startTransition } from 'react';
// Urgent: Show what was typed
setInputValue(input);
// Mark any state updates inside as transitions
startTransition(() => {
 // Transition: Show the results
 setSearchQuery(input);
});
```

In React, updates within startTransition are treated as non-urgent and can be interrupted by urgent updates, like clicks or key presses. React discards incomplete rendering work if interrupted, rendering only the latest update. The useTransition hook initiates transitions and tracks pending states, while startTransition is a method used when hooks aren't applicable. These transitions enable concurrent rendering, allowing updates to be interrupted. During a transition, if content re-suspends, React keeps displaying the current content while rendering the new one in the background.

## NEW HOOKS:

### useId Hook

The useId Hook in React 18 generates unique IDs for both client and server, crucial for accessibility and avoiding hydration mismatches. Previously, React lacked a reliable method to synchronize IDs between server and client, leading to hydration errors. An example is generating a unique ID for a form input, where mismatched IDs could cause issues. React 18's useId Hook addresses this, especially with its new streaming server renderer that outputs HTML non-sequentially.

Here’s a situation in which it could happen: Let’s say we have a form with an input field for which we need to generate a unique id.

```
const Comp = props => {
  const uid = uuid()
  return (
  	<form>
    	<label htmlFor={uid}>Name</label>
<input id={uid} type="text" />
    </form>
  )
}
```

The component above would have ids generated once on the server, and new ones would be generated on the client-side. This would result in a mismatch in the DOM. That’s where the useId hook comes into play.

```import { useId } from 'react'
const Comp = props => {
  const uid = useId()
  return (
  	<form>
    	<label htmlFor={uid}>Name</label>
<input id={uid} type="text" />
    </form>
  )
}
```

The useId hook can be used to generate unique IDs that will be the same on the server- and client-side and thus help to avoid the mismatch error.

### useTransition:

The `useTransition` and `startTransition` functions provide a mechanism to designate certain state updates as non-urgent. By default, React treats state updates as urgent. This means that urgent updates, such as modifying a text input, can interrupt non-urgent updates, like rendering a list of search results.

```
function TabContainer() {
  const [isPending, startTransition] = useTransition();
  const [tab, setTab] = useState('about');

  function selectTab(nextTab) {
    startTransition(() => {
      setTab(nextTab);
    });
  }

}
```

### useDeferredValue:

With `useDeferredValue`, you can postpone the re-rendering of a non-urgent section in the tree. This functionality bears similarities to debouncing but offers distinct advantages. Notably, there is no predefined time delay; React strives to execute the deferred render immediately after the initial render appears on the screen. Moreover, the deferred render is interruptible, ensuring it doesn't impede user input and responsiveness.

```
export default function App() {
  const [query, setQuery] = useState('');
  const deferredQuery = useDeferredValue(query);
  return (
    <>
      <label>
        Search albums:
        <input value={query} onChange={e => setQuery(e.target.value)} />
      </label>
      <Suspense fallback={<h2>Loading...</h2>}>
        <SearchResults query={deferredQuery} />
      </Suspense>
    </>
  );
}
```

### useSyncExternalStore:

The `useSyncExternalStore` Hook is a recent addition facilitating external stores to handle concurrent reads by enforcing synchronous updates to the store. This eliminates the necessity for using `useEffect` when implementing subscriptions to external data sources. It is advisable for any library that interacts with a state external to React to leverage this Hook.

```
import { useSyncExternalStore } from 'react';
import { todosStore } from './todoStore.js';

export default function TodosApp() {
  const todos = useSyncExternalStore(todosStore.subscribe, todosStore.getSnapshot);
  return (
    <>
      <button onClick={() => todosStore.addTodo()}>Add todo</button>
      <hr />
      <ul>
        {todos.map(todo => (
          <li key={todo.id}>{todo.text}</li>
        ))}
      </ul>
    </>
  );
}
```

### useInsertionEffect:

Introducing the `useInsertionEffect` Hook, which specifically caters to CSS-in-JS libraries to tackle performance concerns related to injecting styles during rendering. It's worth noting that unless you've developed a CSS-in-JS library, the likelihood of using this Hook is minimal. This Hook executes after DOM mutation but precedes layout effects that read the updated layout. While addressing a pre-existing problem in React versions 17 and below, its significance is amplified in React 18, where concurrent rendering allows React to yield to the browser, providing an opportunity for layout recalculation.

```
let isInserted = new Set();
function useCSS(rule) {
  useInsertionEffect(() => {
    // As explained earlier, we don't recommend runtime injection of <style> tags.
    // But if you have to do it, then it's important to do it in useInsertionEffect.
    if (!isInserted.has(rule)) {
      isInserted.add(rule);
      document.head.appendChild(getStyleForRule(rule));
    }
  });
  return rule;
}

function Button() {
  const className = useCSS('...');
  return <div className={className} />;
}
```
