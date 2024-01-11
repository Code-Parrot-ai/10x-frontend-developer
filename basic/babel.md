---
title: The Comprehensive Guide to Babel
subtitle: Exploring the Richness of Linguistic Diversity
slug: babel
tags: jsx, browser, babel, react, javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704866971565/FvhVkCE_F.png?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---

## BABEL - OVERVIEW

BabelJS, a JavaScript transpiler created by Australian developer Sebastian McKenzie, seamlessly transforms modern ECMAScript features into an older standard. This enables compatibility across both old and new browsers, making it a vital tool in web development for enhancing code portability and maintainability.

## WHY BABEL JS?

JavaScript serves as the language comprehensible to browsers like Chrome, Firefox, Internet Explorer, Microsoft Edge, Opera, and UC Browser. While ECMA Script 2015 (ES6) is a stable version compatible with both old and new browsers, subsequent versions like ES7, ES8, and ESNext introduce new features that lack universal browser support. Due to this disparity, it's uncertain when complete compatibility across all browsers will be achieved for these newer ECMAScript versions.

Using ES6, ES7, or ES8 features in code may lead to breakages in older browsers due to insufficient support. To address this, developers employ tools like Babel, a transpiler that converts code to a desired ECMA Script version, typically ES5. Babel's features, including presets and plugins, allow configuration of the target ECMA version for code transpilation. This enables developers to utilize the latest JavaScript features, and after transpilation with Babel, the code can be seamlessly run on various browsers without compatibility issues.

## What is Babel-Transpiler?

Babel-Transpiler is a tool that transforms the syntax of contemporary JavaScript into a format comprehensible to older browsers. It converts features like arrow functions, const, and let classes into their older equivalents, such as functions and var. This process maintains functionality while adapting the code to ensure compatibility with browsers that may not support the latest JavaScript syntax.

## Jsx and React

Babel can convert JSX syntax! Check out React preset to get started. Use it together with the babel-sublime package to bring syntax highlighting to a whole new level.
You can install this preset with

```
npm install --save-dev @babel/preset-react
```

and add @babel/preset-react to your Babel configuration.

```
export default function DiceRoll(){
  const getRandomNumber = () => {
    return Math.ceil(Math.random() * 6);
  };

  const [num, setNum] = useState(getRandomNumber());

  const handleClick = () => {
    const newNum = getRandomNumber();
    setNum(newNum);
  };

  return (
    <div>
      Your dice roll: {num}.
      <button onClick={handleClick}>Click to get a new number</button>
    </div>
  );
};

```

## What is Babel-polyfill?

Babel-polyfill is a library that provides a set of polyfills for new ECMAScript features not natively supported by older JavaScript environments. It ensures that the runtime environment has the necessary functions and methods to execute code written using modern ECMAScript syntax. Babel-polyfill is used to address compatibility issues and enable the use of advanced language features in environments that lack native support for them.

The ECMAScript features that can be transpiled and polyfilled in JavaScript vary across different versions of ECMAScript. Here are some features from ECMAScript 2015 (ES6) and later versions that are commonly transpiled and polyfilled:

### 1. Arrow Functions (ES6):

- Transpiled for compatibility with older browsers.

### 2. Block-Scoped Declarations (let, const - ES6):

- Polyfilled to emulate block-scoping in older environments.

### 3. Template Literals (ES6):

- Transpiled for compatibility with browsers that don't support the syntax.

### 4. Destructuring Assignment (ES6):

- Transpiled for broader browser compatibility.

### 5. Spread Syntax (ES6):

- Polyfilled to enable usage in environments lacking native support.

### 6. Classes (ES6):

- Transpiled for compatibility with browsers not supporting the class syntax.

### 7. Promise (ES6):

- Polyfilled for environments without native Promise support.

### 8. Async/Await (ES8):

- Transpiled and polyfilled for compatibility with older browsers.

### 9. Object.values() and Object.entries() (ES8):

- Polyfilled to provide support in environments that lack native implementations.

### 10. Array.includes() (ES7):

- Polyfilled for browsers that do not support the includes method.

### 11. Rest Parameters (ES6):

- Transpiled for compatibility with environments not supporting this syntax.

### 12. Default Parameters (ES6):

- Transpiled for broader browser support.

It's important to note that the need for transpilation and polyfilling depends on the specific features used in your code and the target browser environment. Tools like Babel and Babel-polyfill are commonly employed to handle these transformations and ensure compatibility.

## Features of BabelJS

BabelJS encompasses several key features:

### 1. Babel-Plugins:

Babel supports a variety of plugins that can be utilized individually to transpile code based on the targeted execution environment. These plugins offer specific configurations for customizing the transpilation process.

### 2. Babel-Presets:

Babel presets consist of sets of plugins that serve as configuration details for the babel-transpiler. They guide Babel to transpile code in a specific mode, aligning with desired environments. For instance, using the "es2015" preset converts code to ES5.

### 3. Babel-Polyfills:

In cases where certain features like methods and objects cannot be transpiled, Babel-polyfill comes into play. It enables the utilization of such features in any browser. An example is the use of polyfills for promises to ensure functionality in older browsers.

### 4. Babel-CLI:

Babel-cli provides a command-line interface with commands facilitating easy code compilation. It includes features like plugins and presets that can be seamlessly integrated with the command, simplifying the transpilation process in a single step.

## Advantages of using BabelJS

Using BabelJS in JavaScript development offers key advantages:

### 1. Cross-Browser Compatibility:

Ensures code runs seamlessly on various browsers, including older versions.

### 2. Access to Latest ECMAScript Features:

Allows developers to utilize modern language features while transpiling code for compatibility.

### 3. Code Readability and Maintainability:

Enhances code clarity and maintainability by supporting modern syntax.

### 4. Incremental Adoption of New Features:

Facilitates a gradual transition to the latest language standards without disrupting existing code.

### 5. Plugin Ecosystem and Integration:

Offers a customizable transpilation process through a rich plugin ecosystem and seamless integration with build tools.

### 6. Support for Experimental Proposals:

Enables experimentation with and usage of experimental ECMAScript proposals.

### 7. Community and Documentation:

Benefits from a strong community and extensive documentation for support and learning resources.

## Disadvantages of using BabelJS

### 1. Increased Bundle Size:

Transpiling to older JavaScript versions may result in larger bundle sizes, impacting page load times.

### 2. Build Time Overhead:

The transpilation process can introduce build time overhead, particularly in larger projects.

### 3. Debugging Challenges:

Debugging transpiled code may be more challenging, requiring source maps to map back to the original source.

### 4. Dependency on Build Tools:

Babel's effectiveness depends on integration with build tools, adding complexity to the development environment.

## Usage Guide

This guide will walk you through the steps to compile your JavaScript application code, which utilizes ES2015+ syntax, into code compatible with current browsers. This process includes both transforming new syntax and polyfilling missing features. The setup encompasses the following steps:

1.  Running these commands to install the packages:
    npm install --save-dev @babel/core @babel/cli @babel/preset-env

2.  Creating a config file named babel.config.json (requires v7.8.0 and above) in the root of your project with this content:

```
Babel.config.json

{
  "presets": [
    [
      "@babel/preset-env",
      {
        "targets": {
          "edge": "17",
          "firefox": "60",
          "chrome": "67",
          "safari": "11.1"
        },
        "useBuiltIns": "usage",
        "corejs": "3.6.5"
      }
    ]
  ]
}
```

Or babel.config.js if you are using an older Babel version

```
babel.config.js

const presets = [
  [
    "@babel/preset-env",
    {
      targets: {
        edge: "17",
        firefox: "60",
        chrome: "67",
        safari: "11.1",
      },
      useBuiltIns: "usage",
      corejs: "3.6.4",
    },
  ],
];

module.exports = { presets };
```

And running this command to compile all your code from the src directory to lib:

```
Shell `
./node_modules/.bin/babel src --out-dir lib
```
