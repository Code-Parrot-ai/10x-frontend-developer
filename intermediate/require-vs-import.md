---
title:  "require Vs import: Old Vs New war in Javascript"

subtitle:  "Exploring the Key Differences Between require and import"

slug:  "require-vs-import"

tags:  web development, javascript, software development, import, es6

cover:  https://cdn.hashnode.com/res/hashnode/image/upload/v1707555677847/HbtyAOmvO.webp?auto=format

domain:  10xdev.codeparrot.ai

saveAsDraft:  false

---

**importing a module** is a fundamental concept that refers to the process of bringing one module's code into another module. Think of it as borrowing a book from a library; you don't need to own every book, you just borrow what you need when you need it. Similarly, importing allows developers to reuse code across different parts of an application, enhancing modularity, maintainability, and code organization
In JavaScript we have two major systems of importing.
1. CommonJS Module System
2. ECMAScript (ES6) Module System

### The CommonJS Module System 📦

**CommonJS** is a standard for modularizing JavaScript that was designed with server-side development in mind, particularly for Node.js environments. Under this system, modules are loaded synchronously, meaning one after the other, which is straightforward but can lead to performance bottlenecks, especially when loading a large number of modules.

A CommonJS module might export its functionality like this:

```javascript
// In file square.js
module.exports = function square(x) {
   return x * x;
};
```

And you would import it in another file using `require`:

```javascript
// In file main.js
const square = require('./square.js');
console.log(square(5)); // Output: 25
```

### The ECMAScript (ES6) Module System 🌐

With the advent of ES6, the **ECMAScript** module system introduced `import` and `export` statements, providing a standard way to modularize JavaScript code for the browser. This system supports both static and dynamic imports, allowing for more efficient, tree-shakable builds, where only the necessary code is included.

Here's a simple ECMAScript module example:

```javascript
// In file math.js
export const add = (x, y) => x + y;
export const subtract = (x, y) => x - y;
```

And then you can import only what you need:

```javascript
// In file main.js
import { add } from './math.js';
console.log(add(2, 3)); // Output: 5
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1707549148999/nwAagWjml.jpg?auto=format)

### The Basic Differece

**Require** is part of the CommonJS module system, widely used in Node.js for server-side development. It allows you to include modules like this:

```javascript
const express = require('express');
const app = express();
```

**Import**, on the other hand, is part of the ECMAScript (ES6) module system, a standard for scripting languages like JavaScript. It's more commonly used in frontend development, especially with frameworks like React. Here's how you'd use it:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
```

### When to Use Require 🤔

- **Legacy Node.js Projects**: If you're working on or maintaining server-side projects that were initiated before the widespread adoption of ES6, you'll likely encounter `require`.
- **Dynamic Imports**: `require` allows for dynamic importing of modules, meaning you can conditionally and programmatically load modules. This can be particularly useful in certain scenarios where modules need to be loaded based on specific conditions at runtime.

### When to Use Import 💡

- **Modern Web Development**: For frontend development, especially with frameworks like React, `import` statements are the standard. They support asynchronous module loading and are more declarative, making your code easier to read and maintain.
- **Tree Shaking**: Unlike `require`, `import` allows for tree shaking—a method used during the build process to eliminate dead code, thus optimizing the bundle size.

| Feature          | `require`                                                                 | `import`                                                                              |
|------------------|---------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| **Module System**    | CommonJS                                                                 | ES6 (ECMAScript version 6)                                                            |
| **Loading Type**     | Synchronous (modules are imported sequentially)                          | Mostly static (modules are loaded in order at compile time, dynamic import is async)   |
| **Performance**      | Less efficient due to synchronous loading                                | More efficient with static imports due to predictability and async with dynamic imports|
| **Memory Usage**     | Imports entire module, leading to potentially higher memory usage        | Can import selective components, reducing memory usage                                |
| **Export Access**    | Access to components exported by `module.exports`                        | Access to components exported by `export`                                             |
| **Implementation**   | Can be used directly as it is the default method in Node.js              | Requires ES6 or ECMAScript module support enabled                                     |
| **Usage in Code**    | Can be used anywhere in the program                                      | Static imports are used at the top, dynamic can be used within the program            |

### Quick Summary 

The CommonJS and ECMAScript (ES6) module systems offer two distinct approaches for modularizing JavaScript code. CommonJS, designed primarily for server-side use in Node.js, operates synchronously, making it straightforward but potentially less efficient for loading numerous modules. ES6 modules, conversely, enable both static and dynamic asynchronous imports, allowing for selective loading and optimization of code through tree shaking. This makes ES6 modules particularly suitable for modern web development, where performance and maintainability are key. Developers can choose between these systems based on their project's environment, requirements, and the need for backward compatibility or cutting-edge functionality.