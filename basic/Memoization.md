---
title: Memoization, Decorator functions- Advanced Javascript 
subtitle: Important Javscript Question 
slug: memoization.md
tags: memoization, Decorator functions, javascript, interview questions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704189402735/Dpnzs_RRe.png?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---

Memoization is a powerful optimization technique in programming, particularly useful in JavaScript and React applications. It involves caching the results of function calls to avoid redundant processing. It also is one of the most asked questions in interviews. 

Let's dive into what memoization is, its advantages and drawbacks, and how to implement it in JavaScript, including an explanation of decorator functions.

## What is Memoization?

Memoization is an optimization technique where the result of a function call is stored (or "memoized"). When the function is called again with the same arguments, the cached result is returned, avoiding the need to execute the entire function again.

## When and Why is Memoization Needed?

**Memoization is beneficial when:**

- A function is called frequently with the same arguments.
- The function computations are heavy or time-consuming.
  
**It's particularly useful in scenarios like:**

- Optimizing performance in React components.
- Working with recursive algorithms or complex calculations.

## Let's learn with some code

Suppose we frequently need to print `add(a+b)`, this is how we would write:

```
function add(a+b){
  return a + b;
}

// console logging it twice case we need it at two different places:

console.log(add(2,3));
console.log(add(2,3));

```

Now, Imagine if instead of a simple `add(a+b)` function it was a big complex recursive function it was. Calling this function repeatedly would be expensive.

This is where memoization comes into picture. It memoizes or rather caches the value for you using the argument passed as the key and the result returned as the value. So, the next time you use the same arguments in the function, it wouldn't have to perform all the expensive calculations again and would return the required value!

### Understanding Memoization in JavaScript

Consider a recursive factorial function:

```
const factorial = (x) => {
    if (x === 0) {
      return 1;
    }
    // Recursively call factorial
    return x * factorial(x - 1);
  };
```

Now, if I pass an argument of x (for example, 18) in the factorial function, I want it to memoize the result, so it doesn't perform an expensive operation again if called with the same argument.

To achieve this, we need to understand the concept of a ***Decorator Function***.

### What is a decorator function?

In layman's terms, a decorator function takes a basic function and adds some extra features or steps to it without altering its original purpose. It's like wrapping the original function in a new layer that can do more things. This enhances the functionality of your basic function without modifying it directly.

To apply memoization to the factorial function, we create a new function called `memoizedFactorialFunction`


```
const memoizedFactorialFunction = (fn) => {
   const cache = {};

   return (...args) => {
     if (args.toString() in cache) {
       console.log('Fetching from cache:', cache);
       return cache[args.toString()];
     }
     const result = fn(...args);
     cache[args.toString()] = result;
     return result;
   };
};

```

- We're passing our original `function as fn` in the `memoizedFactorialFunction`. This is typically for two reasons
    - To check if the argument exists in the cache. We spread the arguments (as there can be more than one), convert them to a string (since the cache stores keys as strings), and check for their existence. If the argument exists as a key, it returns its value as the result and exits the function.
    - If the argument is not present in the cache, the function executes the original function with the given arguments, stores the result in the cache, and returns the result.

To call the function, we simply pass the original function,  `factorial(x)` to `memoizedFactorialFunction(fn)` like this:

```
console.log(memoizedFactorialFunction(factorial(5)));
//first time it will calculate and store in the cache

console.log(memoizedFactorialFunction(factorial(5)));
//second time it will directly return from the cached value

```
That's all you need to fo! In React, memoization can be achieved using `React.memo` for components and `useMemo` for values within components.

## Cons Of Memoization

- *Memory Overhead:* Storing cache results consumes memory.
- *Complexity:* Can introduce complexity in code management.



This simple yet important concept is one of the most asked questions in JavaScript interviews. If you would like to know more about such concepts in layman's terms, consider subscribing to our newsletter. I'll see you next week with more insights! :)

