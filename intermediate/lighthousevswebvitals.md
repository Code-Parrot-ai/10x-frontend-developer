## What is Google Lighthouse?

Google Lighthouse is an open-source, automated tool for improving the quality of web pages. It provides audits for performance, accessibility, SEO, and more. You can run Lighthouse in Chrome DevTools, from the command line, or as a Node module.

### How to Run Lighthouse

You can easily run a Lighthouse audit directly from the Chrome DevTools:

1. Open Chrome DevTools (F12 or right-click on the page and select "Inspect").
2. Click on the “Lighthouse” tab.
3. Select the categories you want to audit (Performance, Accessibility, Best Practices, SEO, PWA).
4. Click “Generate report”.

Example report of codeparrot.ai
![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716967587209/I4tSa4WhE.png?auto=format)

## Overview

The Lighthouse report provides a comprehensive audit of the website, focusing on several key areas: Performance, Accessibility, Best Practices, SEO, and PWA. Each category is scored out of 100. Here's a summary of the scores:

- **Performance:** 91
- **Accessibility:** 95
- **Best Practices:** 78
- **SEO:** 100
- **PWA:** Not available (PWA score is not provided)

### Performance (91)

The performance score is quite good at 91. This section evaluates how fast the web page loads and becomes interactive. Here are the key metrics:

- **First Contentful Paint (FCP):** 2.1 seconds
  - Time taken for the first text or image to be painted.
- **Largest Contentful Paint (LCP):** 2.9 seconds
  - Time taken for the largest content element to be painted.
- **Total Blocking Time (TBT):** 100 milliseconds
  - Sum of all time periods between FCP and Time to Interactive, when the main thread was blocked for long enough to prevent input responsiveness.
- **Cumulative Layout Shift (CLS):** 0.003
  - Measures the visual stability of the page and how often unexpected layout shifts occur.

### Accessibility (95)

The accessibility score is high at 95. This measures how accessible the content of your website is to users, especially those with disabilities. This involves evaluating aspects such as color contrast, ARIA roles, and screen reader support.

### Best Practices (78)

This section evaluates adherence to best practices in web development. A score of 78 indicates there are some areas that could be improved to ensure the website follows modern development best practices. This could involve:

- Avoiding deprecated APIs
- Using HTTPS
- Ensuring resources are loaded securely
- Reducing JavaScript execution time

### SEO (100)

A perfect score of 100 indicates excellent adherence to SEO best practices, ensuring the website is optimized for search engines. This includes:

- Proper use of meta tags
- Descriptive link text
- Ensuring pages are crawlable

### PWA (Progressive Web App)

The PWA category is not scored in this report, which might mean that the website does not implement PWA features or the audit was not set up to check for PWA capabilities.

## Detailed Metrics and Their Significance

### Performance Metrics

- **First Contentful Paint (FCP):** 2.1s
  - Indicates how quickly the first piece of content is visible. Good FCP ensures users see some content quickly.
- **Largest Contentful Paint (LCP):** 2.9s
  - Measures loading performance. To provide a good user experience, LCP should occur within 2.5 seconds of when the page starts loading.
- **Total Blocking Time (TBT):** 100ms
  - Low blocking time means the page responds quickly to user input. TBT less than 300ms is considered good.
- **Cumulative Layout Shift (CLS):** 0.003
  - Indicates how much the content shifts during loading. A CLS score less than 0.1 is good.

## Actionable Insights

1. **Improve LCP:** The LCP of 2.9 seconds is slightly above the ideal threshold of 2.5 seconds. Consider optimizing images, improving server response times, and reducing render-blocking resources.
2. **Best Practices:** With a score of 78, review the specific issues flagged in this section of the report. Common improvements include securing resources, optimizing JavaScript, and updating outdated libraries.

## Conclusion

The Lighthouse report for codeparrot.ai shows a well-optimized site with high scores in most categories. Focus on improving the Largest Contentful Paint and addressing any best practices issues to further enhance the site's performance and user experience. Regular audits and monitoring of these metrics will help maintain and improve these scores over time.

## What are Web Vitals?

Web Vitals is a set of metrics introduced by Google to help quantify the user experience on a web page. These metrics focus on three main aspects:

1. **Loading** (Largest Contentful Paint - LCP)
2. **Interactivity** (First Input Delay - FID)
3. **Visual Stability** (Cumulative Layout Shift - CLS)

These metrics are essential for understanding and improving the user experience on your site.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1717083312916/lE74Nb4fb.png?auto=format)

### Analyzing PageSpeed Insights Report

The PageSpeed Insights report you provided shows an overall performance score of 59, indicating that there is significant room for improvement. Let's break down the key metrics and identify areas to optimize.

#### Performance Metrics Breakdown

1. **First Contentful Paint (FCP): 1.0 s**

   - **What it is:** FCP measures the time it takes for the first piece of content to be rendered on the screen.
   - **Status:** Good. This is within the recommended time frame of under 1.8 seconds.

2. **Largest Contentful Paint (LCP): 1.3 s**

   - **What it is:** LCP measures the time it takes for the largest content element visible in the viewport to be rendered.
   - **Status:** Good. This is within the recommended time frame of under 2.5 seconds.

3. **Total Blocking Time (TBT): 810 ms**

   - **What it is:** TBT measures the total time that the main thread is blocked, preventing user input.
   - **Status:** Needs Improvement. The recommended TBT is under 200 milliseconds.

4. **Speed Index: 4.1 s**

   - **What it is:** Speed Index shows how quickly the contents of a page are visibly populated.
   - **Status:** Needs Improvement. Aim for a Speed Index under 3 seconds.

5. **Cumulative Layout Shift (CLS): 0.028**
   - **What it is:** CLS measures the visual stability of the page, indicating how much the page layout shifts unexpectedly.
   - **Status:** Excellent. This is well within the recommended threshold of under 0.1.
