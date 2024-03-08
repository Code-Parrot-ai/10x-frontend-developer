---
title: "Getting started with PWAs"

subtitle: "Dive into the world of Progressive Web Apps (PWAs) and transform your web development skills. This guide covers the key steps to create fast, engaging, and reliable applications that work like native apps"

slug: "getting-started-with-pwas"

tags: web development, frontend, app development, javascript, progressive web apps, web apps, pwa

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1709893011830/OqSLFz8m-.avif?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

A progressive web app (PWA) is an app that's built using web platform technologies, but that provides a user experience like that of a platform-specific app. Some popular PWAs are Starbucks, BMW.
Try installing them by opening Browser Menu > Save and Share > Install

![Image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709893121859/rX2S_KqJx.avif?auto=format)

### How does it work

PWAs are powered by the underlying browser engine (like Chrome, Safari, Firefox, etc.). It opens in a standalone mode that looks and feels like a native app. This mode doesn't show the browser's address bar, navigation buttons, or other interface elements associated with traditional web pages. The browser engine helps in

1. Rendering Web Content: This includes parsing HTML, applying CSS styles and laying out the web page.

2. Executing JavaScript: PWAs heavily rely on JavaScript for their interactive and dynamic features. The browser engine provides the JavaScript engine (e.g., V8 in Chrome, SpiderMonkey in Firefox) that executes the JavaScript code, enabling the dynamic functionalities of PWAs like responding to user interactions, making network requests, and manipulating the DOM.

3. API Access: Modern web browser engines provide a variety of APIs that enable web pages to access device features and perform more complex operations. These include service workers for offline support and background sync, Web App Manifest for installing the web app on the home screen, and other web APIs for accessing device hardware (like camera, GPS, etc.). PWAs utilize these APIs to offer a more app-like experience.

### Native apps vs PWAs

So, should you build a native app or go with PWA? Here are some points to consider

1. **Development:** Native Apps are developed specifically for a particular platform (iOS, Android, Web) using platform-specific languages and tools. They require different codebases for different platforms. PWAs are Developed using standard web technologies (HTML, CSS, JavaScript). They are platform-independent and can run on any device with a compatible web browser, using a single codebase.

2. **Distribution:** Native Apps are distributed through app stores (Apple App Store, Google Play Store). They need to meet specific store guidelines and undergo a review process. PWAs are accessed through the web and do not require app store submission. They can be shared and installed directly from a website.

3. **Performance:** Native Apps, generally offer the best performance and smoothest user experience, as they can directly access device hardware and APIs. PWAs performance is improving but they are typically less performant than native apps. They also have more limitations compared to native apps for access to device APIs and features (camera, GPS, accelerometer, push notifications, etc.). Examples where PWAs won't be a good choice

### Fitness tracking app

A native fitness tracking app can access a wide range of device features and sensors to offer an in-depth fitness tracking experience. It can use the GPS to track running routes accurately, the accelerometer to count steps, and even the heart rate sensor (on devices that have one) to monitor the user's heart rate in real time. Additionally, it can send push notifications to remind the user to exercise or drink water. A PWA for fitness tracking can also access certain device features through modern web APIs. It can use the Geolocation API to track running routes (though it may be less precise than a native app), and the Motion Sensors API to count steps. However, its access to hardware-specific features like a heart rate sensor is typically limited compared to native apps. While PWAs can send push notifications, their capabilities might be restricted on certain platforms, especially iOS.

![Image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709893369897/k3mitKEhy.jpeg?auto=format)

### Mobile Games

A native game app, especially one with high-definition graphics and complex physics simulations, is designed to leverage the device's hardware to its fullest. Native development allows the app to optimize performance by using the device's GPU (Graphics Processing Unit) and multi-core processors efficiently. A PWA game might not match the performance level of a native app, particularly for resource-intensive games. This is because they still operate within the constraints of the browser, which can limit access to the full computational power of the device. PWAs might exhibit longer load times or reduced frame rates during complex animations and gameplay compared to their native counterparts.

![Image](https://cdn.hashnode.com/res/hashnode/image/upload/v1709893431032/anOJrHFRS.avif?auto=format)

### Building your first PWA

- Set Up the Basic Web Application
First, you need to create a basic web application using HTML, CSS, and JavaScript. This is the foundation of your PWA and should be designed responsively to ensure that it works well on a variety of devices and screen sizes.

- Create a Web App Manifest
The web app manifest is a JSON file that contains metadata about your app. This includes information like the name of the app, icons, and the start URL. The manifest allows your web app to be installed on the home screen of a device, similar to a native app. Here's an example of a basic manifest file:

```bash
{
  "short_name": "App",
  "name": "Example Application",
  "icons": [
    {
      "src": "icon/lowres.webp",
      "sizes": "48x48",
      "type": "image/webp"
    },
    {
      "src": "icon/hd_hi.ico",
      "sizes": "72x72 96x96 128x128 256x256",
      "type": "image/x-icon"
    }
  ],
  "start_url": "/",
  "background_color": "#FFFFFF",
  "display": "standalone",
  "scope": "/",
  "theme_color": "#000000"
}
```

Include this file in the root of your web application and link to it in the

section of your HTML:

```bash
<link rel="manifest" href="/manifest.json">
```

- Implement a Service Worker
Service workers are at the heart of PWAs, enabling capabilities like offline support and resource caching. A service worker is a JavaScript file that operates as a type of network proxy between your app and the internet, allowing you to intercept and manage network requests.

Create a service worker file (e.g., sw.js) and include logic for caching resources and handling offline requests. Then, register the service worker from your main JavaScript file:

```bash
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/sw.js').then(function(registration) {
    console.log('Service Worker registered with scope:', registration.scope);
  }).catch(function(err) {
    console.log('Service Worker registration failed:', err);
  });
}
```

Ensure responsiveness, cross-Browser Compatibility and add offline Functionality by using the service worker to cache important resources (HTML, CSS, JavaScript files, images).


### Adding PWAs to mobile

Users can add a Progressive Web App (PWA) to their mobile device, making it accessible like a native app from their home screen. The process varies slightly between different devices and browsers

### Android Devices Using Chrome:
When a user visits a PWA with Chrome, they might see a prompt at the bottom of the screen asking if they want to "Add [App Name] to Home screen."

If the prompt doesn't appear, the user can tap the menu button (three dots in the upper right corner) and then tap "Add to Home screen."

They can then choose a name for the shortcut and confirm the action. The PWA will appear as an icon on their home screen.

### iOS Devices Using Safari:
When visiting a PWA, tap the Share button at the bottom of the Safari window (the rectangle with an arrow pointing upward).
Scroll down and tap "Add to Home Screen."

Enter a name for the shortcut and then tap "Add." The PWA will now appear as an icon on the home screen.

### Conclusion 

PWAs are a powerful tool to build native apps like experience at lower cost. But whether it's the right choice depends on your use case and familiarity with web technologies