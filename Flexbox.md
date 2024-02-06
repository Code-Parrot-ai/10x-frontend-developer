---
title: CSS Flexbox
subtitle: Understanding the principles of Flexbox layout in CSS
slug: CSS-Flexbox
tags: CSS
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704189402735/Dpnzs_RRe.png?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---

# CSS FLEXBOX

The Flexible Box (Flexbox) Layout is a CSS web layout model that enables a container to alter its item size attributes to best utilize space and fit into all screen sizes, expanding to fill space and shrinking where necessary to prevent overflow. 

In this article, we will discuss different Flexbox properties along with why and when they can be used. By the end of this guide, you will have understood the principles of Flexbox and how to apply them in your code.

## UNDERSTANDING FLEXBOX

The Flexbox is a better way of utilizing spaces in CSS when dealing with containers. One cannot understand how to use Flexbox without first knowing how it works.

Unlike the regular Block and Inline layouts, the Flexbox layout is based on Flex-flow Directions. This means items will be laid out following either the Main Axis(left to right and vice versa) or the Cross Axis(top to bottom and vice versa). It is also important to note that the Main Axis may not necessarily be horizontal and solely depends on the Flex-Direction(see below), and the Cross Axis is always the one perpendicular to the Main Axis. Simple enough? 

![Untitled](https://lh3.googleusercontent.com/drive-viewer/AEYmBYR6SXwPIa49T56JPtjYow8447Fpjaurl8PUdI3YlFhHr17LHkVfGB6bGdWRNdpUengKHNCsSCA8pNLqQteK3D_-KV362Q=s2560)

## FLEXBOX PROPERTIES

Flexbox Layout has a wide range of properties. Some are meant for the parent element(flex container), while others are meant for the children element(flex items).

Examples of properties for the parent element include;

- display
- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content
- Examples of properties for the children element include;
- order
- flex

## FLEXBOX PROPERTIES

In this section, we will discuss the above-listed properties in detail and give examples so you can be familiar with the syntax.

Let's begin with the properties of the parent element;

### display

This defines a flex container, be it inline-flex or block-flex. It enables a flex context for all the direct flex items.

```css
.container {
   display: block-flex;
}
```

### flex-direction

The Flexbox is a single-direction layout and this property determines the direction which the flex items will follow in the container. It also determines if the main axis will be horizontal or vertical(see above). 

```css
.container {
   flex-direction: row | row-reverse | column | column-reverse;
}
```

If the flex-direction is set to ‘row’ or ‘row-reverse’, the main axis will be, therefore, horizontal(left to right or vice versa), while if it is set to ‘column’ or ‘column-reverse’, the main axis will be vertical(top to bottom or vice versa).

### flex-wrap

This property is applied when flex items try to fit onto one line by default. This makes the items wrap as needed.

```css
.container {
   flex-wrap: wrap | wrap-reverse | nowrap;
}
```

- wrap: makes flex items wrap unto multiple lines from top to bottom.
- wrap-reverse: does the same thing but from bottom to top(reverse).
- nowrap: lets the flex items fit by default.

### flex-flow

This is pretty much a shortcut to using the Flex-direction and Flex-wrap as it combines both their properties.

```css
.container {
   flex-flow: column wrap;
}
```

The above example sets the flex-direction to the column and the flex items to wrap onto multiple lines from top to bottom.

### justify-content

This aligns content along the main axis. It is used to manipulate leftover spaces and to align flex items when they overflow the line. This property contains different attributes which are important for it to work.

```css
.container {
   justify-content: flex-start | flex-end | space-between | space-around | space-evenly | start | end | center;
}
```

- flex-start(default): this puts the items at the start of the container.
- flex-end: this puts the items at the end of the container.
- space-between: this distributes items evenly on the line, with the first item at the start and the last item at the end.
- space-around: this distributes items evenly on the line, with equal space around them.
- space-evenly: this distributes items evenly so the space between them and the edges of the container is equal.
- start: this puts the items at the start of the writing direction.
- end: this puts the items at the end of the writing direction.
- centre: items are centred along the line.

### align-items

Now as the justify-content property aligns items on the main axis, this property does the same on the cross-axis. It defines how items are laid out along the cross-axis.  

```css
.container {
   align-items: stretch | flex-start | flex-end | center | baseline;
}
```

- stretch: this stretches(pun intended) the item to fill the container.
- flex-start: this puts items at the start of the cross-axis.
- flex-end: this puts items at the end of the cross-axis.
- center: this centers items along the cross-axis.
- baseline: this aligns items in a way that their baselines align.

### align-content

This property aligns the entire content on the cross-axis, not just the items. It is mostly effective on multiple-line content(where flex-wrap is active).

```css
.container {
   align-content: flex-start | flex-end | center | space-between | space-around | space-evenly | stretch;
}
```

- flex-start: this puts content at the start of the container.
- flex-end: this puts content at the end of the container.
- center: this centers content along the cross-axis.
- space-between: this evenly distributes content, with the first line at the start of the container and the last line at the end.
- space-around: this evenly distributes content with equal space around each line and the edges of the container.
- space-evenly: this evenly distributes content with equal space around them.
- stretch: this stretches content to take the leftover space.

Let's discuss the properties of the children element; 

### order

Flex items are usually laid out in source order by default, but this property controls the way the items appear in the container.

```css
.item {
   order: 5;
}
```

The above example is like having a bunch of pictures on a shelf but using the ‘order’ property to rearrange the pictures without physically moving them - changing them in the source code.

### flex

This property is useful in combining the attributes flex-grow and flex-shrink to manipulate the items in the container.

```css
.item {
   flex: none | [ <'flex-grow'> <'flex-shrink'> ]
}
```

- none: leaves the flex item at the default value.
- flex-grow: this gives an item the ability to grow if necessary, especially when there is leftover space in the container. The default value is 0, and when an item is given this property, it takes up as much leftover space as the value assigned to it. So if an item’s value is set to 3, it will try to take up thrice as much of the space of either one of the others.
- flex-shrink: this gives an item the ability to shrink if necessary. The default value is 1. So if an item’s shrink value is set to 2, it will try to take up twice as little of the space of either one of the others.

## APPLYING FLEXBOX PROPERTIES

Now that we have touched on the major flexbox properties above, let us learn how to apply them in our code;

Below is a CodePen where we use the example above;

```css
.flex-container {
  /* We first create a flex layout context */
  display: flex;

  /* Then we define the flow direction 
     and if we allow the items to wrap 
   * Remember this is the same as:
   * flex-direction: row;
   * flex-wrap: wrap;
   */
  flex-flow: column wrap;

  /* Then we define how is distributed the remaining space */
  justify-content: space-around;
}
```

Now let's add some HTML and see the result in the CodePen below;

```html
<ul class="flex-container">
  <li class="flex-item">A</li>
  <li class="flex-item">B</li>
  <li class="flex-item">C</li>
  <li class="flex-item">D</li>
  <li class="flex-item">E</li>
  <li class="flex-item">F</li>
</ul>
```

![Capture 2.PNG](https://lh3.googleusercontent.com/drive-viewer/AEYmBYQCobsTZeiuLxctDRBt_q3KpL7VBV2A-DvJSkzOpKff_5Hp4JE1i-5ktOOwDX7zs0QkrRefuB65GuP1AcpI_lK_NMhWOw=s1600)

The items are arranged this way as a result of the Flexbox property ‘column wrap’(see above).

Let us try something a little more complex. We are going to adjust a navigation element which is at the top of a website, so that it can be centered on medium-sized screens and single columned on small devices. For this, we also need to do some ‘**Flexbox Prefixing**’, which enables our website to support as many browsers as possible. a flexbox prefix normally begins with ‘**@**’.

Example:

```css
/* For Large Screens */
.navigation {
  display: flex;
  flex-flow: row wrap;
  /* This aligns items to the end line on the main axis */
  justify-content: flex-end;
}

/* Medium screens */
@media all and (max-width: 800px) {
  .navigation {
    /* When on medium-sized screens, we center it by evenly distributing space around items */
    justify-content: space-around;
  }
}

/* Small screens */
@media all and (max-width: 500px) {
  .navigation {
    /* On small screens, we are no longer using row direction but column */
    flex-direction: column;
  }
}
``` 

Now take a look at our results in the CodePen below;

```html
<ul class="navigation">
  <li><a href="#">Home</a></li>
  <li><a href="#">About Us</a></li>
  <li><a href="#">Our Products</a></li>
  <li><a href="#">Contact Us</a></li>
</ul>
```

![Capture 3.PNG](https://lh3.googleusercontent.com/drive-viewer/AEYmBYQXY2oN3NFPuuLbPIhd6CaeQnIR2eEUeW-Cwn3p44VTPlQorLCj5VRxde5Fkn-hOghh0ozqMKfnJYr-4mW_Bt8l3AeEOQ=s1600)

Now the original position of the navigation element is right aligned at the top, but when you run this on a smaller screen, the position changes. This is the effect the Flexbox module can have on your website.

## Conclusion

The Flexbox layout is a very efficient alternative to the regular block and inline layout. It ensures that content on the website can easily adapt by adjusting its size and space regardless of screen size or browser compatibility. To learn more about Flexbox properties, Flexbox prefixing, and helpful tricks on using Flexbox, feel free to log on to [https://css-tricks.com/snippets/css/a-guide-to-flexbox/](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).