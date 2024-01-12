---
title: Micro-Frontend - Netflix Case Study
subtitle: How Do Big Enterprises Scale Their Frontend
slug: micro-frontend-netflix
tags: microfrontend , micro-frontend , react , scaling, javascript , scale frontend
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705073205349/MXf9TbuhW.webp?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---


Last week, we learnt about the basics of Micro Frontend. It's time we dive deep into it and understand with an example. We'll be covering a lot of concepts on scaling frontend and identifying independent features so can be parallely scaled without interfering in each other's progress. If you missed reading that make sure to go through it : [Micro-Frontend : Part One](https://10xdev.codeparrot.ai/micro-frontend) . We've covered about Monolithic and Microservice/Micro-Frontend in detail. Today we'll be applying that knowledge through a case study!



## Netflix: Frontend Case Study 📲

If you've ever used Netflix platform, you would know it has 3 main pages specifically.

- Login/ signup Page
- Main Page
- Your Profile and Setting

Now, authentication and Profile in itself are huge components but today we'll be going through Netflix's main page.

If Netflix was a Monolithic Frontend- it would allbe in a same codebase interdependent on each other. However, Netflix is pretty complex to be like that.
Let's try to dissect Netflix's pages.

*Here are all the things on top of my mind for Netflix:* 

1. **All the movie requirements (functional)**
   - Watching a movie
   - Preview of the movie
   - Searching for a movie
      - By Actors
      - Genre
      - Name
2. **All the functional requirements**
   - Adapting diff quality of videos to network band provided by the user
   - Supporting different Screens
   - Using Internet Band
3. **Data Center**
   - API
   - Entities
4. **Data Store On Frontend**
5. **Accessibility**
6. **Optimization**
7. **Design System**
   - Common Components
   - Typography
   - UI, etc
  
This goes on and on. Do do you see how difficult it would be if they were all interdependent on each other? And this is where micro-frontend comes into picture. Assigning different components and frontend to different teams.

I essentially see Netflix like this:

### Main Page

![A Promo Component for new movies or sponsored content](https://cdn.hashnode.com/res/hashnode/image/upload/v1705072836739/6H0Zu2EKC.png?auto=format)

### Movie Page

![Preview of the Movie with a short clip](https://cdn.hashnode.com/res/hashnode/image/upload/v1705072628200/asW832k1n.png?auto=format)


### Search Functionality   

![Search Component](https://cdn.hashnode.com/res/hashnode/image/upload/v1705072653440/OHL8UJ6xL.png?auto=format)





**Diffeerent Components**

```
<!-- Homepage Component -->
<div id="homepage">
    <!-- This can be a separate application -->
</div>
<script src="homepage.js"></script>

<!-- Movie Player Component -->
<div id="movie-player">
    <!-- This can be another separate application -->
</div>
<script src="movie-player.js"></script>

<!-- Search Component -->
<div id="search-component">
    <!-- Yet another separate application -->
</div>
<script src="search-component.js"></script>
```

This was only the tip of the iceberg that goes into identifying and making different components to make sure our frontend is scalable and are not dependent on different features.This is a simplified version of understanding how a complex Frontend Architecture might look like in production for bigger Enterprises . Apart from this a lot of optimization, network performance also comes into picture since it's a very graphic heavy platform which we'll cover later.

If you enjoy reading such topic. Please consider staying tuned!
