---
title: "RxJs and Redux-Observable"

subtitle: "A Comprehensive Guide to Handling Asynchronous Actions in Redux with RxJS and Redux-Observable"

slug: "rxjs-and-redux-observable"

tags: RxJs, Redux-Observable, Observables, Observers, Operators, Subjects, Epics, AJAX, WebSocket

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1718638526524/8TVZUG70s.png?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

> Redux-Observable is a middleware for Redux that uses **RxJS** to handle asynchronous actions. It offers an alternative to `redux-thunk` and `redux-saga`, allowing you to work with async actions using observables.

## Understanding the Observer Pattern

Before diving into RxJS and Redux-Observable, let's revisit the **Observer Pattern**. In this pattern, an "Observable" object maintains a list of "Observers". When the Observable's state changes, it notifies all its Observers.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718630158503/8a0dcx2re.png?auto=format)

```javascript
document.addEventListener("click", (event) => {
  console.log("Element clicked:", event);
});
```

In this example, `addEventListener` makes the document an Observable, and the callback function is the Observer.

## Diving into RxJS

**RxJS** (Reactive Extensions for JavaScript) is a library for composing asynchronous and event-based programs using observable sequences. It extends the Observer pattern by providing operators that allow you to compose Observables in a declarative manner.

### Key Concepts in RxJS

- **Observers**: Objects that subscribe to Observables and receive notifications.
- **Observables**: Objects that emit data over time.
- **Operators**: Functions that allow you to manipulate Observables.
- **Subjects**: Special types of Observables that are also Observers.

## Observers and Observables

### Observers

Observers are objects that can subscribe to Observables and receive notifications of three types: `next`, `error`, and `complete`. Here's a basic example of an Observer in action:

```javascript
import { Observable } from "rxjs";

const observable = new Observable((subscriber) => {
  subscriber.next("Hello");
  subscriber.next("World");
  subscriber.complete();
});

const observer = {
  next: (value) => console.log("Received value:", value),
  error: (err) => console.error("Error:", err),
  complete: () => console.log("Completed"),
};

observable.subscribe(observer);
```

**Expected Output:**

```
Received value: Hello
Received value: World
Completed
```

### Observables

Observables emit data over time and can be created using the `new Observable` constructor. Here’s an example where an Observable emits values periodically:

```javascript
const observable = new Observable((subscriber) => {
  let count = 1;
  const intervalId = setInterval(() => {
    subscriber.next(count++);
    if (count > 5) {
      clearInterval(intervalId);
      subscriber.complete();
    }
  }, 1000);
});

observable.subscribe({
  next: (value) => console.log(value),
  complete: () => console.log("Completed"),
});
```

**Expected Output:**

```
1
2
3
4
5
Completed
```

## Subjects

A Subject is a special type of Observable that can multicast to multiple Observers. Here’s an example:

```javascript
import { Subject } from "rxjs";

const subject = new Subject();

subject.subscribe({
  next: (value) => console.log(`Observer 1: ${value}`),
});

subject.subscribe({
  next: (value) => console.log(`Observer 2: ${value}`),
});

subject.next("Hello");
subject.next("World");
```

**Expected Output:**

```
Observer 1: Hello
Observer 2: Hello
Observer 1: World
Observer 2: World
```

**Note:**

- Observables are unicast, meaning each subscription is independent.
- Subjects are multicast, meaning they share the same execution path among all subscribers

## What Are Operators?

Operators are functions that allow you to manipulate and transform Observables. Here are some examples:

### Creation Operators

**from**

Creates an Observable from an array:

```javascript
import { from } from "rxjs";

const observable = from([1, 2, 3, 4]);

observable.subscribe((value) => console.log(value));
```

**Expected Output:**

```
1
2
3
4
```

### Pipeable Operators

**map**

Transforms each value emitted by the source Observable:

```javascript
import { map } from "rxjs/operators";
import { of } from "rxjs";

const observable = of(1, 2, 3, 4).pipe(map((value) => value * 2));

observable.subscribe((value) => console.log(value));
```

**Expected Output:**

```
2
4
6
8
```

**filter**

Filters the emitted values based on a condition:

```javascript
import { filter } from "rxjs/operators";
import { of } from "rxjs";

const observable = of(1, 2, 3, 4, 5).pipe(filter((value) => value % 2 === 0));

observable.subscribe((value) => console.log(value));
```

**Expected Output:**

```
2
4
```

**mergeMap**

Maps each value to an Observable and flattens the inner Observables:

```javascript
import { mergeMap } from "rxjs/operators";
import { of } from "rxjs";

const observable = of("Hello", "World").pipe(
  mergeMap((value) => of(`${value} RxJS`))
);

observable.subscribe((value) => console.log(value));
```

**Expected Output:**

```
Hello RxJS
World RxJS
```

**switchMap**

Switches to a new Observable on each emission, canceling the previous one:

```javascript
import { switchMap } from "rxjs/operators";
import { interval, of } from "rxjs";

const observable = interval(1000).pipe(
  switchMap((value) => of(`Switched to ${value}`))
);

observable.subscribe((value) => console.log(value));
```

**Expected Output:**

```
Switched to 0
Switched to 1
Switched to 2
... (continues every second)
```

## Setting Up Redux-Observable

To start using Redux-Observable, you need to install the necessary packages:

```bash
npm install redux-observable rxjs
```

### Creating an Epic

An **epic** is a function that takes a stream of actions and returns a stream of actions. Let's start with a basic example:

```javascript
import { ofType } from "redux-observable";
import { mapTo } from "rxjs/operators";

const pingEpic = (action$) =>
  action$.pipe(ofType("PING"), mapTo({ type: "PONG" }));

export default pingEpic;
```

Here, when a `PING` action is dispatched, the epic intercepts it and maps it to a `PONG` action.

### Integrating the Epic with Redux

```javascript
import { createStore, applyMiddleware } from "redux";
import { createEpicMiddleware } from "redux-observable";
import rootReducer from "./reducers";
import pingEpic from "./epics";

const epicMiddleware = createEpicMiddleware();

const store = createStore(rootReducer, applyMiddleware(epicMiddleware));

epicMiddleware.run(pingEpic);
```

- **createEpicMiddleware()**: This function creates the middleware required for Redux-Observable.
- **applyMiddleware(epicMiddleware)**: This applies the epic middleware to your Redux store.
- **epicMiddleware.run(pingEpic)**: This runs the `pingEpic`, allowing it to start intercepting actions.

When the Redux store is set up and a `PING` action is dispatched, the `pingEpic` will intercept it and dispatch a `PONG` action.

### Handling AJAX Requests with Redux-Observable

Let's take a more practical example where we fetch user data from an API. We'll define action creators, create an epic to handle the AJAX request, and update the reducer to process the actions.

#### Action Creators

First, define action creators for starting the fetch and handling the response:

```javascript
export const fetchUser = () => ({ type: "FETCH_USER" });
export const fetchUserFulfilled = (payload) => ({
  type: "FETCH_USER_FULFILLED",
  payload,
});
```

#### Epic for AJAX Request

Create an epic to handle the AJAX request:

```javascript
import { ofType } from "redux-observable";
import { ajax } from "rxjs/ajax";
import { mergeMap, map, catchError } from "rxjs/operators";
import { fetchUserFulfilled } from "./actions";

const fetchUserEpic = (action$) =>
  action$.pipe(
    ofType("FETCH_USER"),
    mergeMap(() =>
      ajax.getJSON("/api/user").pipe(
        map((response) => fetchUserFulfilled(response)),
        catchError(() => of({ type: "FETCH_USER_FAILED" }))
      )
    )
  );

export default fetchUserEpic;
```

1.  **ofType('FETCH_USER')**: Filters the actions to only include those with the type `'FETCH_USER'`.
2.  **ajax.getJSON('/api/user')**: Makes an AJAX request to fetch user data from the `/api/user` endpoint.
3.  **map(response => fetchUserFulfilled(response))**: Maps the AJAX response to a `FETCH_USER_FULFILLED` action.
4.  **catchError(() => of({ type: 'FETCH_USER_FAILED' }))**: Catches any errors during the AJAX request and maps them to a `FETCH_USER_FAILED` action.

When a `FETCH_USER` action is dispatched, the epic makes an AJAX request. If the request is successful, a `FETCH_USER_FULFILLED` action is dispatched with the response data. If the request fails, a `FETCH_USER_FAILED` action is dispatched.

#### Combining Epics

If you have multiple epics, combine them using `combineEpics`:

```javascript
import { combineEpics } from "redux-observable";
import fetchUserEpic from "./fetchUserEpic";

const rootEpic = combineEpics(fetchUserEpic);

export default rootEpic;
```

#### Updating the Reducer

Update your reducer to handle the new actions:

```javascript
const initialState = {
  user: null,
};

const userReducer = (state = initialState, action) => {
  switch (action.type) {
    case "FETCH_USER_FULFILLED":
      return { ...state, user: action.payload };
    default:
      return state;
  }
};

export default userReducer;
```

When a `FETCH_USER_FULFILLED` action is dispatched, the user data in the state is updated with the fetched data. When a `FETCH_USER_FAILED` action is dispatched, an error message is set in the state.

## Practical Use Cases for Redux-Observable

### Debouncing API Requests

Let's say you want to provide autocomplete suggestions as the user types. Instead of making an API call for every keystroke, you can debounce the requests.

```javascript
import { debounceTime, switchMap } from "rxjs/operators";

const searchEpic = (action$) =>
  action$.pipe(
    ofType("SEARCH"),
    debounceTime(500),
    switchMap((action) =>
      ajax.getJSON(`/api/search?q=${action.payload}`).pipe(
        map((response) => ({ type: "SEARCH_FULFILLED", payload: response })),
        catchError(() => of({ type: "SEARCH_FAILED" }))
      )
    )
  );

export default searchEpic;
```

### Cancelling Ongoing Requests

Using `switchMap`, you can cancel the previous request if a new one comes in:

```javascript
const searchEpic = (action$) =>
  action$.pipe(
    ofType("SEARCH"),
    debounceTime(500),
    switchMap((action) =>
      ajax.getJSON(`/api/search?q=${action.payload}`).pipe(
        map((response) => ({ type: "SEARCH_FULFILLED", payload: response })),
        catchError(() => of({ type: "SEARCH_FAILED" }))
      )
    )
  );

export default searchEpic;
```

### Polling an API

You might need to poll an API to get updates regularly. Here's how you can do it:

```javascript
import { interval } from "rxjs";
import { switchMap } from "rxjs/operators";

const pollEpic = (action$) =>
  action$.pipe(
    ofType("START_POLLING"),
    switchMap(() =>
      interval(5000).pipe(
        switchMap(() =>
          ajax.getJSON("/api/data").pipe(
            map((response) => ({ type: "POLL_SUCCESS", payload: response })),
            catchError(() => of({ type: "POLL_FAILED" }))
          )
        )
      )
    )
  );

export default pollEpic;
```

### Handling WebSocket Connections

Redux-Observable can also be used to manage WebSocket connections:

```javascript
import { webSocket } from "rxjs/webSocket";

const websocketEpic = (action$) =>
  action$.pipe(
    ofType("CONNECT_WEBSOCKET"),
    switchMap(() =>
      webSocket("ws://example.com").pipe(
        map((message) => ({ type: "WEBSOCKET_MESSAGE", payload: message })),
        catchError(() => of({ type: "WEBSOCKET_FAILED" }))
      )
    )
  );

export default websocketEpic;
```

## Conclusion

Redux-Observable, powered by RxJS, provides a robust and flexible way to handle asynchronous actions in Redux applications. By embracing observables and functional programming, you can simplify your code and make it more maintainable.

Whether you're dealing with API calls, debouncing user input, managing WebSocket connections, or polling APIs, Redux-Observable offers powerful tools to manage these workflows efficiently.

If your application involves complex async workflows, give Redux-Observable a try. You might find it to be the perfect solution for your needs. For more detailed information and examples, check out the [official Redux-Observable documentation](https://redux-observable.js.org/).
