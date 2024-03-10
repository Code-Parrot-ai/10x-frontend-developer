---
title: "Framer Motion: Animate React Easily"
subtitle: A beginner-friendly guide to adding smooth animations to your React app effortlessly.
slug: framer-motion-animate-react-easily
tags: frontend, animations, ui, framer, framer motion
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710014692087/Y49b1MQad.webp?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---

An important part of improving the online application user experience is animation. Creating sophisticated and fluid animations in the React ecosystem has frequently proven to be difficult, requiring developers to go through a multitude of tools or battle with CSS animations. Framer Motion is a robust and adaptable toolkit created exclusively for React that streamlines the animation creation process. In this blog, we'll dive deep into what Framer Motion has to offer. Let's explore how it might offer that extra spark needed to make your React applications stand out and truly elevate them.

## What is Framer Motion?

For any developer looking to add seamless and beautiful animations to their projects, Framer Motion is an excellent addition to their toolbox. Fundamentally, Framer Motion is a library with extensive animation features that are both strong and easily accessible, with the goal of making animation simple.
Framer Motion's simplicity and feature richness are what make it a wonderful tool.Not only does Framer Motion have a vast feature set, but it also prioritizes usability and performance above other animation libraries.

## Getting started with Framer motion in React

To get started, we'll require a React application with the framer libraries installed.
To install framer-motion in your react app, run

```bash
npm install framer-motion
```

or if you're using yarn, run

```bash
yarn add framer-motion
```

### Framer's `motion` component

At the heart of Framer Motion is the `motion` component, a powerful and flexible tool that transforms standard React components or HTML elements into animated wonders. There's a motion component for every HTML and SVG element, for instance `motion.div`, `motion.circle` etc. When you use a motion component, you're not just working with a static element anymore. Instead, you gain access to a suite of properties that control animations, gestures, and more.

Creating a React Component and using the `motion` component, importing it from "framer-motion"

```bash
import React from 'react';
import { motion } from 'framer-motion';

function MyAnimatedComponent() {
  return (
    <motion.div animate={{ scale: 1.2 }} transition={{ duration: 0.5 }}>
      Hello, animations!
    </motion.div>
  );
}

export default MyAnimatedComponent;
```

`animate`: The animate property allows us to do various transformation animations on the provided objects, such as translating on the X and Y axes, rotating, scaling, and changing the degree of opacity.

### Leveraging AnimatePresence for Exit Animations

Though handling animations for when components depart might be a little more difficult, Framer Motion's motion component offers an amazingly versatile approach to animate parts as they enter or while they're present on the screen. This is where the component called `AnimatePresence` comes in quite handy. It enables you to add exit animations to components in your React apps, resulting in a smooth and visually beautiful transition between the entering, updating, and quitting of your components.

`AnimatePresence` is a component that enables us to animate components when they're removed from the React tree. It's especially useful for conditional rendering or when components enter and leave the DOM based on user interactions, such as toggling visibility or navigating between routes.

To use `AnimatePresence`, wrap it around the components you wish to animate on exit. The only requirement is that these components accept an `exit` prop to define the animation that occurs when they're removed from the component tree.

Here is a sample example for the same:

```bash
import { motion, AnimatePresence } from "framer-motion"

export const MyComponent = ({ isVisible }) => (
  <AnimatePresence>
    {isVisible && (
      <motion.div
        initial={{ opacity: 0 }}
        animate={{ opacity: 1 }}
        exit={{ opacity: 0 }}
      />
    )}
  </AnimatePresence>
)
```

In this example, a component is conditionally rendered based on the isVisible prop. When isVisible is false, the component exits, and AnimatePresence triggers the exit animation specified in the exit prop of the motion.div.

`initial`: Using this property, we may set the initial location of an animated object. This might be its scale, rotation, and location on the y and x axes.

### Transitions
A `transition` defines the type of animation used when animating between two values.It gives you control over the personality of each motion and gives your animations a smooth, snappy, or bouncy feel. You can use this prop to offer a uniform appearance and feel to all of your animations by applying it to both the animate and exit properties.


#### Types of Transitions
Framer Motion supports several types of transitions, each offering a unique effect:

- **Tween:** The default type, useful for simple, straightforward animations. It interpolates values over time, providing a smooth transition from start to end.

- **Spring:** Adds a natural, physics-based motion to your animations, making them feel more dynamic. Spring transitions are great for interactions and gestures, giving a responsive feedback loop to user inputs.

- **Inertia:** Mimics a free-falling object coming to a rest, ideal for deceleration animations. It's particularly effective for swipe or momentum-based interactions.

A Sample Example of using the `spring` transition:
```bash
<motion.div
  animate={{ x: 100 }}
  transition={{ type: "spring", stiffness: 100 }}
/>
```

### Gesture-Based Interactions

Framer Motion also supports gesture-based interactions such as dragging, hovering, tapping, and more. These interactions can make the application feel more alive and responsive to user inputs.

#### Draggable Elements:

To make an element draggable, simply add the `drag` prop to a `motion` component. You can constrain the drag to a specific axis or define boundaries.

```bash
<motion.div drag="x" dragConstraints={{ left: -100, right: 100 }}>
  Drag me!
</motion.div>
```

#### Hover and Tap Effects:

Animating elements on hover or tap is straightforward with Framer Motion. Use the `whileHover` and `whileTap` props to define animations for these interactions.

```bash
<motion.button whileHover={{ scale: 1.1 }} whileTap={{ scale: 0.9 }}>
  Press Me
</motion.button>
```

### Exploring Further with Framer Motion

We have only begun to explore the full potential of Framer Motion in React applications. Framer Motion offers a wide range of features to turn your apps into something more than just functional—from straightforward fades and scales to intricate motions and animations that respond to user interaction.
You can go through the [official Framer Motion documentation](https://www.framer.com/motion/) for guides, examples, and detailed descriptions of the various components and features they provide.
