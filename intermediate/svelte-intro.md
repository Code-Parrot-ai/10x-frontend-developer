---
title: "Svelte for Beginners: Easy Guide"

subtitle: "Introduction to Svelte for beginners: Simple steps to get started."

slug: "svelte-for-beginners"

tags: web development, svelte, javascript, web framework

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711299559492/dYVNRBnt6.webp?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

> Resources: https://github.com/harshalranjhani/svelte-resources

### What is Svelte?

Svelte is a modern web framework that allows you to write less code and build highly efficient web applications. Svelte provides a ground-breaking framework that is notable for its effectiveness and ease of use. Svelte guarantees applications are lighter and faster than those created with conventional frameworks by shifting the majority of its effort to compile time. It's compiler compiles your code into highly optimized vanilla JavaScript at build time. This means that there is no need for a virtual DOM, which makes Svelte applications faster and more efficient than other frameworks like React and Vue.

### Why Svelte?

Svelte offers several advantages that make it an attractive choice for web development:

- **Faster Loading Times:** Thanks to its compile-time optimization, Svelte significantly reduces the size of the final bundle. This leads to faster loading times, a crucial factor for enhancing user experience and improving SEO rankings.

- **Effortless Reactivity:** Svelte's reactivity model is both simple and powerful. Developers can define reactive statements easily, ensuring the UI stays up-to-date with the application state without the overhead of virtual DOM diffing.

- **Easy to Learn:** With a syntax that closely resembles standard HTML, CSS, and JavaScript, Svelte is incredibly easy for developers to pick up, especially those already familiar with web development basics.

- **Built-In State Management:** Unlike other frameworks that often require external libraries for state management, Svelte's built-in store feature offers a straightforward solution, simplifying state management across components.

### Getting Started with Svelte

To get started with Svelte, you can use the official Svelte template to create a new project. First, make sure you have Node.js installed on your system. You can then create a new Svelte project using the following command:

```bash
npm create svelte@latest my-svelte-app
```

You will be prompted with a series of questions to configure your project. In this example we're going with a skeleton project to start from scratch and we'll be using typescript. Once the project is created, you can navigate to the project directory and install all the dependencies by running `npm install`. You can then start the development server by running `npm run dev`.

I'm using the following configuration for the project setup:

![Project Setup Preview](https://cdn.hashnode.com/res/hashnode/image/upload/v1711374380371/MKp37DJKN.png?auto=format)

### Writing Your First Svelte Component

Svelte components are defined using a `.svelte` file extension. Let's create a simple component that displays a greeting message. Create a new file named `HelloWorld.svelte` in the `src/components` directory and add the following code:

```svelte
<script>
    let name = 'world';
</script>

<h1>Hello {name}!</h1>

<style>
    h1 {
        color: royalblue;
    }
</style>
```

We now need to import this component into our `routes/+page.svelte` file. Update the `+page.svelte` file as follows:

```svelte
<script lang="ts">
    import HelloWorld from "../components/HelloWorld.svelte";
</script>

<HelloWorld />
```

Here the `+` sign in the `+page.svelte` file name is a convention used by SvelteKit to denote a page route.

You should now see the greeting message displayed on the page. This is a simple example of how you can create and use components in Svelte.

### Reactivity in Svelte

Svelte's reactivity model allows you to define reactive statements that automatically update the UI when the underlying data changes. Let's modify our `HelloWorld.svelte` component to include a button that increments a `num` variable:

```svelte
<script lang="ts">
    let name = 'world';
    let num = 0;

    function increment() {
        num += 1;
    }
</script>

<h1>Hello {name}!</h1>
<h2>Number: {num}</h2>
<button on:click={increment}>Increment</button>

<style>

  /* styles here */

</style>
```

You should see something like this:

![Reactivity in Svelte](https://cdn.hashnode.com/res/hashnode/image/upload/v1711378870264/pgbpcgoQ5.gif?auto=format)

This example showcases how effortlessly Svelte handles reactivity. The `num` variable is automatically monitored for changes, and the DOM is updated without the need for additional code or libraries.

### Creating a new Route

The routes of your app — i.e. the URL paths that users can access — are defined by the directories in your codebase:

- `src/routes` is the root route
- `src/routes/about` creates an /about route
- `src/routes/blog/[slug]` creates a route with a parameter, slug, that can be used to load data dynamically when a user requests a page like /blog/hello-world

### Built-in Transitions 😁

Svelte provides built-in transitions that allow you to animate elements with ease. Let's create a `/fade` route to demonstrate transitions in Svelte. Create a new folder named `fade` inside the `src/routes` directory and add an `+page.svelte` file with the following code:

```svelte
<script lang="ts">
    import { fade } from 'svelte/transition';
    let visible = true;
</script>

{#if visible}
    <div class="fade-container" transition:fade>Fade me in and out</div>
{/if}

<button on:click={() => (visible = !visible)}> Toggle Visibility </button>

<style>
    /* styles here */
</style>
```

You can now navigate to the `/fade` route in your browser and see the fade-in and fade-out effect when you click the button. This is just one example of the many built-in transitions available in Svelte.

![Fade preview](https://cdn.hashnode.com/res/hashnode/image/upload/v1711376563526/2aBRESMcY.gif?auto=format)

### Component Lifecycle

Svelte components have a lifecycle that includes various stages such as creation, update, and destruction. You can use lifecycle functions to perform actions at specific stages of a component's lifecycle. Here are some of the lifecycle functions available in Svelte:

- `onMount`: Schedules a callback to run as soon as the component has been mounted to the DOM.

- `beforeUpdate`: Schedules a callback to run immediately before the component is updated after any state change.

- `afterUpdate`: Schedules a callback to run immediately after the component has been updated.

- `onDestroy`: Schedules a callback to run immediately before the component is unmounted.

You can use these functions to perform tasks like fetching data, setting up subscriptions, or cleaning up resources when a component is created, updated, or destroyed.

We can add a simple example to our `HelloWorld.svelte` component to demonstrate the `onMount` and `onDestroy` lifecycle function:

```svelte
<script lang="ts>

 // ...

import { onMount, onDestroy } from 'svelte';

onMount(() => {
        console.log('Component has been mounted');
});

onDestroy(() => {
        console.log('Component is being destroyed');
});

  // ...

</script>
```

### Conditionals and Loops

Svelte provides a simple and intuitive syntax for conditionals and loops. You can use the `if` and `each` blocks to conditionally render elements or iterate over arrays. Here's an example of using conditionals and loops in Svelte.

Let's create a `/conditionals` route to demonstrate conditionals and loops. Create a new folder named `conditionals` inside the `src/routes` directory and add an `+page.svelte` file with the following code:

```svelte
<script lang="ts">
    import { slide } from 'svelte/transition';
    let show = true;
    let items = ['Apple', 'Banana', 'Cherry'];
</script>

<h1>Hello Svelte!</h1>

{#if show}
    <ul transition:slide>
        {#each items as item}
            <li>{item}</li>
        {/each}
    </ul>
{/if}

<button on:click={() => (show = !show)}>Toggle Visibility</button>

<style>

  /* styles here */

</style>
```

Earlier in this article we used the `if` block to conditionally render the fade effect. In this example, we're using the `each` block to iterate over an array of items and render a list along with the `if` block to toggle the visibility of the list.

If you head over to the `/conditionals` route in your browser, you should see the list of items rendered with a slide-in effect. Clicking the button will toggle the visibility of the list.

![Conditionals and Loops](https://cdn.hashnode.com/res/hashnode/image/upload/v1711377868691/zBkaXTtpF.gif?auto=format)

### Conclusion

Svelte is a powerful web framework that offers a fresh approach to building web applications. Its simplicity, reactivity model, and built-in features make it an excellent choice for developers looking to create efficient and maintainable applications. By following this guide, you should now have a good understanding of how to get started with Svelte and build your first components, routes, and transitions. You can read more about svelte on the official [Svelte website](https://svelte.dev/).

