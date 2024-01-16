---
title: Why You Should Not Use <div> Elements in Web Development?
subtitle: Enhancing Digital Inclusivity- A Guide to Website Accessibility
slug: web-accessibility.
tags: jsx, browser, accessibility, react, javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704866971565/FvhVkCE_F.png?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---

## Introduction

Have you ever witnessed the remarkable adaptability of a physically challenged individual using a mobile phone? Observing this can be a profound and enlightening experience. These individuals often employ a variety of accessibility tools, ingeniously navigating and interacting with apps in ways that many of us might not have considered. This serves as a powerful reminder to us, as developers and creators, about the critical importance of designing accessible websites. 

Website accessibility is not just a matter of legal compliance or ethical responsibility; it's a gateway to empower millions of users with diverse abilities, ensuring equal access to information and functionality.

## Understanding Website Accessibility

From my experience, the most effective approach to mastering web accessibility begins with delving into its various aspects. Reflecting on my early coding days, I recall overlooking several HTML topics, mistakenly deeming them trivial. Yet, I've learned that returning to the basics is essential. The key lies in understanding HTML semantics, which forms the backbone of web accessibility.

## Basic Standards of Website Accessibility

The cornerstone of web accessibility standards is the Web Content Accessibility Guidelines (WCAG), developed by the World Wide Web Consortium (W3C). These guidelines are widely accepted as the gold standard for building accessible websites. 

*The WCAG guidelines are divided into three levels of compliance:* 
- **A** (must support)
- **AA** (should support), and
- **AAA** (may support)
providing a range of accessibility targets to meet various needs.

## How To Write Accessible Code?

In my opinion, starting with reading various aspects of accessibility is the best way to do it. I remember, when I was first learning to code, I skipped a lot of topics in HTML cause they weren't priortized and felt unimportant. Going back to basics, would be the first thing you could start. HTML semantics contribute the large part of Web Accessibility.

*Some basic examples are:* 
- ### Semantic HTML: Use HTML5 semantic elements like `<header>`, `<footer>`, and `<nav>` to define the structure of your website.
- ### ARIA Roles: Use `ARIA` roles to help screen readers understand the purpose of elements. For example, role="navigation" for your main navigation menu.
- ### Keyboard Navigation: Ensure all interactive elements are accessible via keyboard. Use tabindex to manage focus order.
- ### Screen Reader Compatibility: Add alt text to images and provide text alternatives for non-text content.

## The Overuse of <div> Elements

Avoid using a lot of `divs` - always guilty of doing it I know :")
A `<div>` is a generic container with no semantic meaning. It's often used for styling purposes or as a layout tool. However, when overused, `<div>` elements can create a number of problems:

- ### Accessibility Issues: Screen readers rely on the semantic structure of a page to interpret content for visually impaired users. Overusing <div> elements can make a page more difficult to navigate using assistive technologies.
- ### Poor SEO: Search engines favor web pages with clear semantic structure. Excessive use of `<div>`s can lead to lower search rankings.
- ### Maintainability Challenges: Pages heavy with `<div>` elements can become difficult to maintain and update, especially in large projects.

## Appropriate Alternatives to `<div>`
Instead of defaulting to `<div>`, consider these semantically meaningful `HTML5` elements:

- ### `<header>` and `<footer>`: Use these for introductory content or navigational links (header) and for information like contact details or copyrights (footer).
- ### `<nav>`: Ideal for navigation links.
- ### `<section>` and `<article>`: Use `<section>` for distinct sections of a page and `<article>` for self-contained content, which could theoretically stand alone, like blog posts.
- ### `<aside>` : Perfect for content slightly related to the main content, like sidebars.
- ### `<main>`: It represents the primary content of the body of a document or application and should be unique to the document.

## Example: Improving Accessibility with Semantic HTML

Consider a webpage with a navigation bar, main content, and a sidebar, all wrapped in `<div>` elements. Here's how it can be improved:

### Before
    ```
    <div id="header">
      <!-- navigation links -->
    </div>
    <div id="main">
      <!-- main content -->
    </div>
    <div id="sidebar">
      <!-- sidebar content -->
    </div>
    
    ```

### After

    ```
    <nav>
      <!-- navigation links -->
    </nav>
    <main>
      <!-- main content -->
    </main>
    <aside>
      <!-- sidebar content -->
    </aside>
    
    ```


*A common oversight in web accessibility is neglecting keyboard navigation or failing to provide alt text for images. Regular accessibility audits are essential to identify and rectify such issues.*

## Conclusion
Web accessibility is not a one-time task but an ongoing commitment to inclusive design and development. By embracing these practices, we can create a digital world that is accessible to all, regardless of their abilities or circumstances.

## Learning Resources

For further exploration, consider the following tools and readings:
- (The A11Y Project Checklist)[https://www.a11yproject.com/checklist/]
- (WAVE (Web Accessibility Evaluation Tool))[https://wave.webaim.org/]

If you enjoy reading blogs like this where we talk about ins and outs of frontend development. Consider subscribing to us & we'll see you soon :)
