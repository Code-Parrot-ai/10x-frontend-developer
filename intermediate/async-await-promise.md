---
title: "Is async/await a good idea? 🤔 async/await vs promises"

subtitle: "Understanding the difference between Promises and async/await in JavaScript"

slug: "async-await-vs-promises"

tags: javascript, web development, software development, async, await, promises

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708611976908/sZwu51E1R.png?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

### Understanding Promises 🤝

Before the advent of `async`/`await`, Promises were the go-to solution for handling asynchronous operations in JavaScript. A Promise in JavaScript is an object representing the eventual completion or failure of an asynchronous operation. It allows you to attach callbacks instead of using nested callbacks in a complex phenomenon often referred to as "callback hell."

**Example:**

```javascript
function fetchData(url) {
  return new Promise((resolve, reject) => {
    // Simulate an API call
    setTimeout(() => {
      const data = "Fake data from " + url;
      resolve(data);
    }, 1000);
  });
}

fetchData("https://api.example.com/data")
  .then((data) => console.log(data))
  .catch((error) => console.error(error));
```

**Cons:**

- **Complexity in Handling Multiple Asynchronous Calls:** When dealing with several asynchronous tasks that depend on each other, the code can become nested and harder to read.
- **Still Callbacks:** Under the hood, Promises still use callbacks, albeit in a more manageable form.

![promise-flow-chart](https://cdn.hashnode.com/res/hashnode/image/upload/v1708609511092/h07xYo2-0.png?auto=format)

### Entering `async`/`await` 🕚

Introduced in ES2017, `async`/`await` is syntactic sugar built on top of Promises. It allows you to write asynchronous code that looks and behaves like synchronous code, which is a significant leap forward in terms of readability and simplicity.

**Example:**

```javascript
async function fetchData(url) {
  try {
    // Simulate an API call
    const response = await new Promise((resolve, reject) => {
      setTimeout(() => {
        const data = "Fake data from " + url;
        resolve(data);
      }, 1000);
    });
    console.log(response);
  } catch (error) {
    console.error(error);
  }
}

fetchData("https://api.example.com/data");
```

**Pros:**

- **Simplicity and Readability:** The `async`/`await` syntax is clean, straightforward, and easy to understand at first glance. 📖
- **Error Handling:** It allows the use of try/catch blocks, making error handling more intuitive than chaining `.catch()` methods.
- **Debugging:** Debugging asynchronous code is easier, as the code execution is paused on the `await` expressions, making it behave like synchronous code during debugging sessions.

**Cons:**

- **Error Propagation:** Errors must be carefully handled, or they can be silently ignored, leading to harder-to-find bugs. 🚫
- **May Lead to Unintended Blocking:** If not used wisely, `await` can lead to blocking of code execution, especially if used in loops or unnecessary serialization of asynchronous operations. ⏳

### Understanding the Difference in Execution 🖥️

#### Promises Execution

Promises are executed immediately upon creation. This means that when you create a new Promise, the executor function passed to the constructor is run straight away. The then-catch-finally pattern is used to handle the results of the Promise once it has been resolved or rejected.

Consider this flow:

1. **Initialization:** The Promise is created and the executor function runs immediately.
2. **Pending State:** Until the asynchronous operation completes, the Promise remains in a pending state.
3. **Settlement:** The Promise is either fulfilled with a value (resolved) or an error (rejected).
4. **Chaining:** `.then()` is called if the Promise is resolved, `.catch()` if it's rejected, and `.finally()` runs in both cases after the resolution or rejection.

Promises enforce a clear separation between the initiating of an asynchronous operation and the handling of its result, which can be both a strength and a complexity depending on the situation.

#### `async`/`await` Execution

The `async`/`await` pattern simplifies the chaining of Promises by making asynchronous code look and behave more like synchronous code. This is especially useful when you need to perform a series of asynchronous operations in a specific order.

Here’s the typical execution flow:

1. **Async Function:** An `async` function is declared, which implicitly returns a Promise.
2. **Awaiting:** Within the `async` function, `await` is used to pause the execution until the Promise resolves.
3. **Sequential Execution:** Each `await` call waits for the previous operation to complete before executing the next line, making it easier to follow the code flow.
4. **Error Handling:** `try`/`catch` blocks within an `async` function can catch both synchronous and asynchronous errors, giving a synchronous feel to error handling.

While `async`/`await` can make code easier to read by reducing the nesting of `.then()` and `.catch()` methods, it's important to note that it can also lead to performance issues if not used correctly, as it might introduce unnecessary waiting.

### Comparing Promises and `async`/`await`

| Feature                           | Promises                                                             | `async`/`await`                                                                        |
| --------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| **Syntax**                        | Thenable chain                                                       | Syntactic sugar over Promises, uses `async` and `await` keywords                       |
| **Error Handling**                | Uses `.catch()` for errors                                           | Uses try/catch blocks                                                                  |
| **Readability**                   | Good for simple chains, but can get complicated with multiple chains | More readable and looks synchronous                                                    |
| **Debugging**                     | Can be challenging in complex promise chains                         | Easier, as code can be stepped through like synchronous code                           |
| **Return Value**                  | Always returns a Promise                                             | `async` function returns a Promise                                                     |
| **Execution Flow**                | Non-blocking, always asynchronous                                    | Pauses at each `await` for the Promise to resolve, making it easier to follow the flow |
| **Ideal Use Case**                | Suitable for single or less complex asynchronous operations          | Better for handling multiple asynchronous operations in a sequence                     |
| **Complex Asynchronous Patterns** | Possible but may lead to "callback hell" if not managed properly     | Simplifies handling complex asynchronous code patterns                                 |
| **Community Preference**          | Widely used before ES2017, still prevalent for simple cases          | Increasingly preferred for its simplicity and cleaner code structure                   |

**Promises** kick off the moment you create them, and you handle the results with `.then()` or `.catch()`.

**`async`/`await`** makes you wait at each `await` for the promise to finish, which can make your code easier to follow but might slow things down if you’re not careful.

### So, What Should You Use? 🤔

- **Use Promises** when you have lots of async things happening that don’t depend on each other. They’re great for managing multiple things at once without creating a mess.
- **`async`/`await`** is awesome when you need things to happen in a specific order, one after the other. It keeps your code clean and easy to read.
