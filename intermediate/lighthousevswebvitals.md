---
title: "Light House vs Web Vitals: Which score is real?"

subtitle: "Discover how to use React Profiler to find and fix performance issues in your React applications."

slug: "optimize-react-components-with-the-react-profiler"

tags: react, performance, optimization, react-profiler, react-memo, usecallback

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1716613534464/I38p952Do.png?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

## What is Google Lighthouse?

Google Lighthouse is an open-source, automated tool for improving the quality of web pages. It provides audits for performance, accessibility, SEO, and more. You can run Lighthouse in Chrome DevTools, from the command line, or as a Node module.

### How to Run Lighthouse

You can easily run a Lighthouse audit directly from the Chrome DevTools:

1. Open Chrome DevTools (F12 or right-click on the page and select "Inspect").
2. Click on the “Lighthouse” tab.
3. Select the categories you want to audit (Performance, Accessibility, Best Practices, SEO, PWA).
4. Click “Generate report”.

Example report of codeparrot.ai

![lighthouse report](https://cdn.hashnode.com/res/hashnode/image/upload/v1716967587209/I4tSa4WhE.png?auto=format)

## Overview of a Lighthouse Report

- **Performance:** 91
- **Accessibility:** 95
- **Best Practices:** 78
- **SEO:** 100
- **PWA:** Not available (PWA score is not provided)

### Performance (91)

- **First Contentful Paint (FCP):** 2.1 seconds
  - Time taken for the first text or image to be painted.
- **Largest Contentful Paint (LCP):** 2.9 seconds
  - Time taken for the largest content element to be painted.
- **Total Blocking Time (TBT):** 100 milliseconds
  - Sum of all time periods between FCP and Time to Interactive, when the main thread was blocked for long enough to prevent input responsiveness.
- **Cumulative Layout Shift (CLS):** 0.003
  - Measures the visual stability of the page and how often unexpected layout shifts occur.

### Accessibility (95)

This measures how accessible the content of your website is to users, especially those with disabilities. This involves evaluating aspects such as color contrast, ARIA roles, and screen reader support.

### Best Practices (78)

This section evaluates adherence to best practices in web development. A score of 78 indicates there are some areas that could be improved to ensure the website follows modern development best practices.

### SEO (100)

A perfect score of 100 indicates excellent adherence to SEO best practices, ensuring the website is optimized for search engines. This includes:

- Proper use of meta tags
- Descriptive link text
- Ensuring pages are crawlable

## What are Web Vitals?

Web Vitals is a set of metrics introduced by Google to help quantify the user experience on a web page. These metrics focus on three main aspects:

1. **Loading** (Largest Contentful Paint - LCP)
2. **Interactivity** (First Input Delay - FID)
3. **Visual Stability** (Cumulative Layout Shift - CLS)

These metrics are essential for understanding and improving the user experience on your site.

### How to Measure Web Vitals

Just enter the website link in google pagespeed insights and you will get the web vitals score.
Example report of codeparrot.ai

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1717083312916/lE74Nb4fb.png?auto=format)

### Analyzing PageSpeed Insights Report

#### Performance Metrics Breakdown

1. **First Contentful Paint (FCP): 1.0 s**

   - FCP measures the time it takes for the first piece of content to be rendered on the screen.
   - **Status:** Good. This is within the recommended time frame of under 1.8 seconds.

2. **Largest Contentful Paint (LCP): 1.3 s**

   - LCP measures the time it takes for the largest content element visible in the viewport to be rendered.
   - **Status:** Good. This is within the recommended time frame of under 2.5 seconds.

3. **Total Blocking Time (TBT): 810 ms**

   - TBT measures the total time that the main thread is blocked, preventing user input.
   - **Status:** Needs Improvement. The recommended TBT is under 200 milliseconds.

4. **Speed Index: 4.1 s**

   - Speed Index shows how quickly the contents of a page are visibly populated.
   - **Status:** Needs Improvement. The recommended Speed Index is under 3 seconds.

5. **Cumulative Layout Shift (CLS): 0.028**
   - CLS measures the visual stability of the page, indicating how much the page layout shifts unexpectedly.
   - **Status:** Excellent. This is well within the recommended threshold of under 0.1.

## Differences Between Lighthouse and Web Vitals

### Results Comparison

In the Lighthouse report, the performance score was 91, whereas the PageSpeed Insights report showed a performance score of 59. The discrepancy is primarily due to differences in the environments and specific metrics each tool prioritizes.

### Reasons for Lower Score in Web Vitals

The lower score in Web Vitals can be attributed to higher Total Blocking Time (TBT) in the PageSpeed Insights report. This indicates that while the initial loading times (FCP and LCP) are good, the page has issues with interactivity and responsiveness, likely due to heavy JavaScript execution or blocking resources.

### Scope and Purpose

**Lighthouse:**

- **Comprehensive Audits:** Lighthouse provides a broad set of metrics and audits across multiple categories, including Performance, Accessibility, Best Practices, SEO, and Progressive Web App (PWA).
- **Tool for Developers:** It is designed as a developer's tool to offer detailed insights into various aspects of a website, not just performance.

**Web Vitals:**

- **Focused Metrics:** Web Vitals focuses specifically on key user experience metrics. These metrics are chosen because they have a strong correlation with the overall user experience.
- **User-Centric:** The primary goal of Web Vitals is to quantify and improve the user experience in terms of loading speed, interactivity, and visual stability.

### Key Metrics

**Lighthouse Metrics:**

- **Performance Metrics:** First Contentful Paint (FCP), Largest Contentful Paint (LCP), Speed Index, Total Blocking Time (TBT), Cumulative Layout Shift (CLS).
- **Accessibility Metrics:** Checks for color contrast, ARIA roles, screen reader support, and other accessibility features.
- **Best Practices:** Assesses the use of deprecated APIs, secure resource loading, optimized JavaScript, and adherence to modern web development standards.
- **SEO:** Evaluates meta tags, descriptive link text, crawlability, and other SEO best practices.
- **PWA:** Checks for Progressive Web App features such as offline support, service workers, and manifest files.

**Web Vitals Metrics:**

- **Largest Contentful Paint (LCP):** Measures loading performance, focusing on the time it takes for the largest content element to appear in the viewport.
- **First Input Delay (FID):** Measures interactivity, specifically the delay between a user's first interaction with the page and the time when the browser responds to that interaction.
- **Cumulative Layout Shift (CLS):** Measures visual stability by quantifying how much the layout shifts unexpectedly during the page's lifecycle.

### Usage Scenarios

**Lighthouse:**

- **Development and Testing:** Ideal for developers who need a comprehensive audit of their website's performance and quality. It provides actionable insights into various aspects of web development.
- **Continuous Integration:** Can be integrated into CI/CD pipelines to ensure that code changes do not degrade the website's performance or quality.
- **Broader Analysis:** Useful for performing a wide range of checks beyond just performance, such as accessibility and SEO.

**Web Vitals:**

- **User Experience Optimization:** Best suited for monitoring and optimizing the core aspects of user experience—loading speed, interactivity, and visual stability.
- **Real-World Data:** Often used in conjunction with field data from tools like Google’s Chrome User Experience Report (CrUX) and real user monitoring (RUM) tools to understand how real users experience the website.
- **Simplified Metrics:** Provides a clear and focused set of metrics that are easy to understand and prioritize for user experience improvements.

### Data Collection

**Lighthouse:**

- **Lab Data:** Lighthouse provides lab data, which means it simulates page loads in a controlled environment and provides consistent, repeatable metrics. This is useful for debugging and testing changes before they go live.
- **Controlled Conditions:** Since it's run in a controlled environment, the results might differ from real-world user experiences, especially if there are significant differences in network conditions and device capabilities.

**Web Vitals:**

- **Field Data:** Web Vitals often rely on field data, capturing metrics from real user interactions. This provides a more accurate picture of how actual users experience the site.
- **Variability:** Since field data reflects real-world conditions, there can be variability in the results based on different user devices, network speeds, and other factors.

## Conclusion

While both Lighthouse and Web Vitals are essential tools for web performance optimization, they serve different purposes and provide different types of insights. Lighthouse offers a comprehensive audit tool that covers multiple aspects of web development, whereas Web Vitals focuses specifically on the core metrics that matter most to user experience. By using both tools, you can ensure their websites are both high-performing and user-friendly, meeting the needs of both search engines and end-users.
