---
title: WINDOW Object in Javascript
subtitle: Understanding the window object and it's functionality in web development
slug: window-object-in-javascript
tags: window, javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704189402735/Dpnzs_RRe.png?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---


# WINDOW Object in JavaScript

The `window` object can be considered the most vital element of a JavaScript program. It is the global object in the web browser which contains the Document Object Model (DOM). The `window` object provides access to the web browser’s attributes such as opening new tabs, manipulating browser location etc. This means all functions and variables declared globally are attached to the `window` object.

In this article, we will discuss the `window` object and its functionality. By the end of this guide, you will have understood the importance of the `window` object and how to utilize it when writing your code.

## **Understanding the `window` object**

The `window` object represents the current window that the JavaScript code is running in, making it possible for the user to interact with the web browser and the document being displayed. The `window` object has four distinct features which include;

- **Browser-related Functionality:** The `window` object provides methods and properties related to the browser like `window.location`, `window.alert` etc.
- **Global Scope:** This means that all variables and functions declared globally with the `var` keyword will become properties of the `window` object.
- **DOM Interaction:** The `window` object serves as the global object for interacting with the Document Object Model. This allows HTML properties and their elements to be manipulated.
- **Setting Timers and Intervals:** The `window` object is involved in managing timers and intervals (e.g., `setTimeout` and `setIntervals` )

Below is an example of how we can implement the `window` object;

```jsx
function globalFunction() {
    alert("This is a global Function");
}
window.globalFunction();
```

Here’s what the output will look like;

![codepen function.PNG](https://lh3.googleusercontent.com/drive-viewer/AKGpihYJy30FLCVJFexS714RnvXZ8sOtU9MZ3BwdE6q9EN4Zcck65_sOs82L6-qUBlm_LIh3tK-DTPynU6_2SnHH3f6KYlG-=s1600)

As the global object, the `window` element gave access to the function `globalFunction` to appear as an alert (popup) on the browser. This is an example of the browser-related functionality feature of the `window` object.  

## Utilizing the `window` object

The `window` object exposes the functionality of a web browser by providing methods for performing different actions on it. It can either be used as a function property or to manipulate the web browser. Here are some examples below;

### `window` object as a function property

| Property Name | Function |
| --- | --- |
| window.document() | The HTML document shown in the window is represented by the Document object, which is referred to by the document property. |
| window.console() | The console gives the window’s Console Object back. |
| window.location() | The location attribute refers to the Location object, which has data about the page’s current URL. |
| window.innerWidth and window.innerHeight() | These characteristics describe the width & height of the browser window, without including the toolbars and scrollbars. |
| window.outerWidth and window.outerHeight() | These characteristics describe the width & height of the browser window, including the toolbars and scrollbars. |
| window.frameElement() | This gives the window’s current frame back. |
| window.parent() | This brings up the current window’s parent window. |

### `window` object to manipulate the web browser

| Property Name | Function |
| --- | --- |
| window.open() | This method opens a new browser window or tab. |
| window.close() | This method closes the current window or tab. |
| window.alert() | This method displays an alert message to the user. |
| window.prompt() | This method displays a prompt message to the user and waits for their input. |
| window.resizeTo() | This method resizes the window to a specific size. |
| window.setInterval() | At predetermined intervals, setInterval() calls a function or evaluates an expression (in milliseconds). |
| window.setTimeout() | When a certain amount of milliseconds have passed, the setTimeout() method calls a function or evaluates an expression. |

### **Conclusion**

The `window` object is an important part of JavaScript and it is frequently used in web development to manipulate the web browser and the document being displayed. It provides methods for manipulating a window and can be utilized as a function property. To learn more about  the `window` object in JavaScript with extensive examples, feel free to log on to [https://www.geeksforgeeks.org/window-object-in-javascript/](https://www.geeksforgeeks.org/window-object-in-javascript/)