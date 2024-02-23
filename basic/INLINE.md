---
title: CSS Inline vs Block vs Inline-Block Elements
subtitle: Understanding the differences between inline, block and inline-block elements
slug: CSS-inline-vs-block-vs-inline-block-elements
tags: CSS, inline, inline-block, block
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704189402735/Dpnzs_RRe.png?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---

# CSS INLINE vs BLOCK vs INLINE-BLOCK ELEMENTS

Ever wondered how content on webpages seem to follow a specific design layout? With some filling the entire width of the screen and others just laying side by side? This is due to the effects of display properties like **Inline, Inline-Block and Block**. These elements determine how content is displayed and how they interact with other content on the webpage.

In this article, we will discuss the difference between these elements and their functions. By the end of this guide, you will be able to note their differences along with a few code examples to show how they are applied. 

## `inline` element

This element displays content on the same line. Applying size properties (height and width) has no effect as content with this property does not start on a new line and only takes its default space.

```css
.inline-element  {
   display: inline;
   width: 2800px; /* No Effect*/
   height: 1000px; /* N0 Effect */
}
```

The image below shows an example of content that possesses `inline` element;

![inline image.PNG](https://lh3.googleusercontent.com/drive-viewer/AEYmBYQqODP30GAaFYptPhGBKqk6graeSdbIDhCk4UvD2Ni2hHjKB6yyaAhl-yGDINIDHllHr5k9Ztl6xHniG1_gSJyHYI3v5Q=s1600)

## `block` element

This element displays content row after row. This means content is made to appear above one other, with each one taking up a row (depending on the size of the content).

```css
.block-element {
  display: block;
}
```

Below is an example of content that possess `block` element;

![block.PNG](https://lh3.googleusercontent.com/drive-viewer/AEYmBYTLFp3Qcxti1t3IzkXOKiJ5IQUui1cpTQneTcmgHsLuALJjGIMBR799q1v_zMlSymoTn81F11wjvSG67BBv01m6oT36Ag=s1600)

Unlike with `inline` element, the height and width of content here can be adjusted to any preferred size.

## `inline-block` elements

We know that `inline` element keeps content on the same row, and `block` element arranges content one above the other, well the `inline-block` element is a combination of the first two. Think of it as an inline element whose size attributes can actually be adjusted.

```css
.inline-block-element  {
   display: inline-block;
   width: 100px; /* It will work */
   height: 100px; /* It will work */
}
```

See an example below;

![inline block main.PNG](https://lh3.googleusercontent.com/drive-viewer/AEYmBYQ5l4YEOJQtcbI-39Ay2eKRy3UN-4L3hqnQL4IfFU1oDx4IoFroKWL5v0JX_rkyn-71C2xqOw3qsxDQUpvYuJczXYzs6w=s1600)

In the above example, the letters **A, B** and **C** all have different size attributes but are all inline (no pun intended).

Let us try one more example using inline-block element, this time adding some HTML for better understanding;

```html
<div class="inline-block-element" 
     id="letterA">A</div>
<div class="inline-block-element" 
     id="letterB">B</div>
<div class="inline-block-element" 
     id="letterC">C</div>
<div class="inline-block-element" 
     id="letterD">D</div>
<div class="inline-block-element" 
     id="letterE">E</div>
<div class="inline-block-element" 
     id="letterF">F</div>
```

Now we add our CSS below;

```css
.inline-block-element {
  display: inline-block;
  background-color: purple;
  color: gold;
  margin: 5px;
}

#letterA {
  height: 100px;
  width: 170px;
}

#letterB {
  height: 90px;
  width: 20px;
}

#letterC {
  height: 67px;
  width: 100px;
}

#letterD {
  height: 90px;
  width: 200px;
}

#letterE {
  height: 300px;
  width: 50px;
}

#letterF {
  height: 70px;
  width: 200px;
}
```

![inline block 3.PNG](https://lh3.googleusercontent.com/drive-viewer/AEYmBYRKDq1ZOmYtwFeZGCtJPiQ9mgA8NEcSTmQM35GM6nOfI0U7_y_JjolwMUP4DMBOzGAX8TCgNjbMIWY-zbaEfSwBQB6U1w=s1600)

Thorough knowledge of basic display elements like these can be a big help to Frontend developers anywhere. It is also important to practice using display elements as it can boost creativity and flexibility. To learn about other CSS display elements, feel free to log on to [https://www.geeksforgeeks.org/css-display-property/](https://www.geeksforgeeks.org/css-display-property/)