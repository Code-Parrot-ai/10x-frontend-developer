---
title: "React to Vercel: Deployment Made Easy."
subtitle: "Learn how to deploy your React applications to Vercel seamlessly, from setup to live site, with this easy-to-follow guide"
slug: react-to-vercel-deployment-made-easy
tags: frontend, vercel, react, deployment, CI/CD
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710189790879/qobeZS95N.webp?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---

Deploying React apps can seem difficult, but tools like Vercel make it surprisingly simple. Vercel offers smooth deployment procedures and is an expert in hosting frontend frameworks. The following guide is designed for front-end developers who want to quickly and easily launch their React apps.

## What is Vercel?

Vercel is a cloud platform that allows users to build, scale, and secure web experiences. Vercel handles all the tricky bits, like making sure your site loads fast and stays up, so you can focus on creating more awesome stuff. It's like having a backstage crew for your one-person show, making sure everything runs smoothly while you soak up the applause.

## Creating a React app for deployment

You can either use your React app or create one scratch by using Vite:
```bash
npx create-vite-app vercel-deployment --template react
```

Now enter into the app by running:
```bash
cd vercel-deployment
```

Install all the dependencies using:
```bash
npm install
```

or if you're using yarn run:
```bash
yarn
```

Install the vercel CLI:
```bash
npm install --global vercel
```

or:

```bash
yarn add vercel
```
This command will install the **vercel CLI** globally in your system so you don't have to download it every time.

Once this is done you can check whether vercel was successfully installed or not by running:
```bash
vercel --version
```

If you see a version, you're good to go! 
Now let's login to the vercel CLI by running:

```bash
vercel login
```

You'll be prompted with various ways to login to vercel, you can select any one of those and proceed further.

Once you've successfully authenticated, run:
```bash
vercel
```

This is a command used to create a new deployment in vercel. After running this you'll be prompted with a few basic questions to finish setting up your deployment. I would recommend just going with the defaults if you're unsure about anything!

After all of this is done you'll be prompted with the Production url, copy and paste that url in your browser and there it is, your app is now accessible to the world! 🎉

If you've followed along with me, you should see something like this on the unique url generated for you:

![Deployment Preview](https://cdn.hashnode.com/res/hashnode/image/upload/v1710190596045/rBg6QCfzX.png?auto=format)


### Bonus - Setting up a CI/CD pipeline 

The approach we followed previously was good, but it would not be very helpful in cases where your code changes regularly. In that case, following the previous approach would mean that you'll have to re deploy every changed version of your code with a new url and new project each time.

Instead, we can set up a CI/CD pipeline directly on version which looks out for changes in your code using your github connected github repository to the project.

To do this just head over to [Vercel](https://vercel.com/) and log in if you're not already logged in. If this is your first project, you'll be seeing something like this.

![Vercel Dashboard](https://cdn.hashnode.com/res/hashnode/image/upload/v1710191446638/vkMlecaLW.png?auto=format)

Select "Import new Project" or "Add Project" from the options and connect your github when prompted.

After you're authenticated, you'll be seeing a list of all the git repositories connected to your account. Just select the one that you want to deploy.

![Git Repositories List](https://cdn.hashnode.com/res/hashnode/image/upload/v1710192697807/nz58mRsLc.png?auto=format)

You should be prompted with something like this:
![Project Initiation](https://cdn.hashnode.com/res/hashnode/image/upload/v1710192041467/keU7iolrc.png?auto=format)

### Project Name
This is the name of your vercel project.

### Framework Preset
If you're using something other than React to deploy to vercel, you can select it here.

### Root Directory
Specify the root directory of your project. In this tutorial it will remain default.

### Build and Output Variables
You can override build and installation commands here.

### Environment variables
If you're using any environment variables, you can specify those here.

If you're following along, I'd recommend you to keep everything as default and just click on Deploy! 🚀

It will start building your app, and you can check the logs in the given UI. After everything is successful you should be redirected to a dashboard page for your project with the public link for your react app.

The important thing here to note is that now whenever a new commit is pushed to the repository, the app will get updated automatically and there won't be any manual changes required!

Here is the preview of the deployment if you're following along:

![Deployment Preview](https://cdn.hashnode.com/res/hashnode/image/upload/v1710190596045/rBg6QCfzX.png?auto=format)

Congratulations on deploying your project to Vercel! 🚀 Now, it's time to shine and share your innovation with the world. 🌍✨