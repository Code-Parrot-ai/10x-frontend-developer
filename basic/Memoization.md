---
title: Memoization, Decorator functions- Advanced Javascript 
subtitle: Important Javscript Questions
slug: micro-frontend
tags: micro-frontend, microfrontend, frontend, scalable, frontend architecture, frontend Design
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

Suppose we want to print `add(a+b)` more than once, this is how we would write:

```
function add(a+b){
  return a + b;
}

// console logging it twice case we need it at two different places:

console.log(add(2,3));
console.log(add(2,3));

```

Now, Imagine if instead of a simple `add(a+b)` function it was a big complex recursive function it was. It would have to call this function twice and that would be expensive.

This is when memoization comes into picture. It memoizes or rather caches the value for you using the argument passed as the key and the result returned as the value. So next time you use the same arguments in the function, it wouldn't have to do all the expensive calculations and return you the required value!

### Let's try to understand it with an example in Javascript:

Suppose we've a recursive factorial function:

```
const factorial = (x) => {
    if (x === 0) {
      return 1;
    }
    // Recursively call factorial
    return x * factorial(x - 1);
  };
```

Now, I want to make sure that if I pass an arg of `x` (for example: 18) in the factorial function, it not only returns the value but also memoizes it so next time I need to pass the same arg, it doesn't perform an expensive operation again.

To perform that we need a bit of understanding on ***Decorator Function***.
### What is a decorator function?

In layman's terms, It takes a basic function and adds some extra features or steps to it, without altering the original purpose of the function. It's like wrapping the original function in a new layer that can do more things. This way, you can enhance the functionality of your basic function without modifying it directly.

To do memoization on the factorial fn, we need to create a new function call memoizedFactorialFunction


```
const memoizedFactorialFunction = (fn) => {
   const cache = {}

  return (..args) => {
  if(args.toString() in cache){
  console.log(cache);
  return cache[args.toString()];
}
  const result = fn(...args)
  cache[args.toString()] = result;
  return result;
}
```

- We're passing our original `function as fn` in the `memoizedFactorialFunction`. This is typically for two reasons
    - To check if the argument we're passing in the `fn` exist in the `cache` by first spreading the arguments, as there can be more than one argument. And then converting it to a string as the cache stores the key in string format. And then checking if it exists. If the arg exist as the key, then it returs it's value as the result and exists the function.
    - If the argument is not present, it comes out of the if loop and passes the arg in the original function, gets the result, storses the result in key-value pair again in the cache and returns the result.

 Now to call the function we'll simply need to pass the original function i.e `factorial(x)` in `memoizedFactorialFunction(fn)` like this:

```
console.log(memoizedFactorialFunction(factorial(5))); //first time it will calculate and store in the cache
console.log(memoizedFactorialFunction(factorial(5))); //second time it will directly return from the cached value

```
That's all you need to fo! In React, memoization can be achieved using `React.memo` for components and `useMemo` for values within components.

This very simple yet very important concept is one of the most asked questions in Javascript interviews. If you would like to know more about such concepts in layman's terms. Consider subscribing to our newletter. And I will see you soon, next week! :)


