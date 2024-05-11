---
title: "Docker for Next.js"

subtitle: "Learn How to Dockerize Your Next.js Application for Development and Deployment"

slug: "docker-nextjs"

tags: web-development, docker, nextjs, deployment, containers, devops

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1715437751002/69XJlXfB8.webp?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

## What is Docker?  🐳

- **Docker** is an open-source platform that uses containerization technology to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all the parts it needs, such as libraries and other dependencies, and ship it all out as one package.
- **Docker Container:** A lightweight, standalone, executable package that includes everything needed to run a piece of software, including the code, runtime, libraries, environment variables, and config files.
- **Docker Image:** A blueprint for creating Docker containers. Images are immutable files that outline the instructions for a complete and executable version of an application.

## Creating a Next.js Image with Docker 🚀

In the root of your Next.js project, create a file named Dockerfile and add the following content: 

### Dockerfile

```Dockerfile
# Use the lightweight Node.js 18 Alpine image
FROM node:18-alpine

# Set environment variable with a default for production
ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

# Establish working directory
WORKDIR /app

# Copy and install dependencies
COPY package*.json ./
RUN if [ "$NODE_ENV" = "development" ]; \
        then npm install; \
        else npm install --only=production; \
    fi

# Copy application code
COPY . .

# Build the application in production
RUN if [ "$NODE_ENV" = "production" ]; \
        then npm run build; \
    fi

# Expose port 3000
EXPOSE 3000

# Specify the command to start the app
CMD if [ "$NODE_ENV" = "development" ]; \
        then npm run dev; \
        else npm start; \
    fi
```

## Building and Running the Docker Container 🛠️

To build and run the Docker container, enter the following commands in your terminal:

### Development Environment:

```bash
docker build --build-arg NODE_ENV=development -t my-nextjs-app-dev .
docker run -p 3000:3000 -v $(pwd):/app my-nextjs-app-dev
```

### Deployment Environment:

```bash
docker build -t my-nextjs-app-prod .
docker run -p 3000:3000 my-nextjs-app-prod
```

###  Stop Docker Container
```bash
docker stop <container-name>
```

## How to Push the Docker Image to Docker Hub 

To share your Docker image via Docker Hub, follow these steps:

1. **Login to Docker Hub**:
   ```bash
   docker login
   ```
2. **Tag your Docker image**:
   ```bash
   docker tag my-nextjs-app yourusername/my-nextjs-app:latest
   ```
3. **Push the image to Docker Hub**:
   ```bash
   docker push yourusername/my-nextjs-app:latest
   ```
You can now access your Docker image from any machine by pulling it from Docker Hub.
To pull the image, use the following command:
```bash
docker pull yourusername/my-nextjs-app:latest
```

Now onwards, you can deploy your Next.js application using Docker containers. It's a great way to ensure consistency across different environments and simplify the deployment process. 🚀

