---
title: "Why not to use Server Side Rendering?"

subtitle: "Learn about the drawbacks of server side rendering and when not to use it."

slug: "why-not-to-use-server-side-rendering"

tags: "server-side-rendering", "web-development", "frontend", "javascript", "react", "vue", "svelte"

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1709983997630/u61b-gbfr.webp?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---
## What is Server-Side Rendering?

SSR is a technique used in web development where the HTML of a webpage is generated on the server rather than in the browser. This means when a user requests a webpage, the server prepares the HTML document by executing the necessary logic and sends it to the client's browser, fully formed and ready to be rendered. This approach is different from CSR, where JavaScript runs in the browser to generate HTML content dynamically.

## How it works?
Server-side rendering is the predominant method used to present information on a display. It involves the server transforming HTML documents into data that the browser can interpret.

Every time you access a website, your browser sends a request to the server hosting the website's content. The duration of this request is brief, typically a few milliseconds, but it can vary based on several factors:

- Your internet connection speed
- The geographical location of the server
- The number of people accessing the site simultaneously
- The level of optimization of the website, among others

After processing the request, the browser receives the fully rendered HTML and displays it on your screen. Should you navigate to a different page within the same website, your browser will submit a new request for the specific content. This process repeats for every new page you visit that isn't already stored in the browser's cache.

Regardless of whether the new page has only minor differences from the current one, the browser will request the entire page and render it anew.

## Benefits of SSR

1. **Faster Initial Page Load:** SSR can significantly improve the time to first byte (TTFB), providing content to users more quickly. This can be particularly advantageous for SEO and for users with slow internet connections.
2. **SEO Optimization:** Search engines can more easily crawl and index SSR pages, as the content is already compiled into HTML upon their request.
3. **Social Media Sharing:** When sharing links on social media, SSR ensures that metadata (like images and descriptions) is properly loaded and displayed in the preview, enhancing engagement.

## Drawbacks of SSR

1. **Slower Page Transitions:** Transitioning between pages can be slower with SSR, especially if your site handles complex or heavy data. This is due to the double rendering process - once on the server and once on the client.
2. **Vulnerability:** With a larger surface to attack, SSR sites can be harder to secure compared to CSR sites. Knowledge and diligence in security practices are essential to mitigate this issue.
3. **Complex Caching:** Caching strategies tend to be more complicated with SSR, requiring more effort to configure effectively compared to CSR.
4. **Server Cost:** High-performance SSR may necessitate more robust and costly server resources than CSR.
5. **Higher Latency:** During peak traffic, SSR sites might experience higher latency, affecting the browsing experience. This issue is less prevalent in CSR, where latency, or ping rate, plays a smaller role in performance.

## When to Use and When Not to Use SSR

**When to Use SSR:**
- For landing pages or content-rich sites where SEO is a priority.
- When targeting users with slower internet connections, ensuring they receive content swiftly.
- On websites where social media sharing is a key part of your strategy.

**When Not to Use SSR:**
- For applications where real-time user interactions and dynamic updates are frequent, such as web applications with live chat features.
- When the development team lacks the expertise to handle the complexities of SSR, including security and caching strategies.
- If server resources are limited or the cost is a concern, CSR might be a more economical choice.

## Conclusion

SSR is a powerful approach in web development with its set of benefits, especially around SEO and initial page load times. However, it's not a one-size-fits-all solution. The choice between SSR and CSR should be informed by your project's specific needs, audience, and resources. Understanding the trade-offs and when to employ each rendering method can significantly impact your web application's success. As you continue to explore and experiment with these techniques, keep in mind that the ultimate goal is to provide a seamless, efficient, and secure experience for your users. Happy coding!

## [Bonus] Hybrid Approach

### How It Works

1.  **Initial Load with SSR:** When a user first visits a page, the server sends a fully rendered HTML document, ensuring that the content is quickly visible. This step is crucial for improving the Time to First Paint (TTFP) and Time to Interactive (TTI), which are important metrics for user experience and SEO.
    
2.  **Subsequent Interactions with CSR:** After the initial load, navigation and interactions within the site are handled client-side. JavaScript takes over to dynamically update the content without needing to reload the entire page from the server. This allows for a seamless, app-like user experience.
    
3.  **Selective Rendering:** Not all parts of an application need to be server-rendered. The hybrid approach allows developers to choose which pages or components are rendered on the server based on their impact on performance and SEO. For example, static pages like blog posts or product descriptions might be SSR, while dynamic sections like user dashboards can be CSR.

### Benefits of the Hybrid Approach

-   **Improved SEO:** The server-side rendering component of the hybrid approach ensures that search engines can crawl and index content effectively, improving the visibility of the web application.
-   **Enhanced Performance:** By serving fully rendered pages on the initial load, the application can provide content to users faster, improving metrics such as TTFP and TTI.
-   **Rich Interactivity:** Once the initial page is loaded, CSR takes over, providing users with a smooth, interactive experience without the need for full page refreshes.
-   **Flexibility:** Developers can strategically decide which parts of their application benefit most from SSR or CSR, allowing for optimized performance and resource utilization.