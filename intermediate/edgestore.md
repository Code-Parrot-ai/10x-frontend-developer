---
title: "Next.js Large file uploads using Edge Store"

subtitle: "Uncover the simplicity and efficiency of managing file uploads in Next.js projects using Edge Store"

slug: "nextjs-file-uploads"

tags: nextjs, web development, file upload, edgestore

cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711136035289/EZSoGA1y0.webp?auto=format

domain: 10xdev.codeparrot.ai

saveAsDraft: false
---

> Resources: https://github.com/harshalranjhani/edgestore-resources

### The Current State of File Uploads in Next.js

Handling file uploads in Next.js requires setting up a server to manage these uploads and writing a significant amount of boilerplate code. This process can be time-consuming and prone to errors, which poses a challenge for developers looking to create efficient and reliable applications when dealing with large files or low network conditions.

### What is EdgeStore?

EdgeStore is a type-safe Node package that makes it super easy to upload and retrieve files from the cloud. It's designed to cut down on the setup or configuration time, letting you say goodbye to all that extra boilerplate code you'd normally have to write for cloud file uploads. With EdgeStore, managing cloud files becomes straightforward, freeing you up to focus more on building great features for your app.

### Using Edgestore in a Next.js project

First let's start by initializing a Next.js project:

```bash
npx create-next-app@latest # yarn create next-app
```

After you're done setting up the Next.js project, you'll be prompted with a few questions, I would suggest going with all the default options, only that we'll be using Typescript in this article, since edgestore is type-safe, why not utilize that right?

Now enter inside your app and install all the dependencies:

```bash
npm install # yarn
```

Now we will install the dependencies required by edgestore:

```bash
npm install @edgestore/server @edgestore/react zod # yarn add @edgestore/server @edgestore/react zod
```

We will start by creating a new account on [edgestore](https://dashboard.edgestore.dev/sign-up). After you're successfully signed up, you can head over to your [dashboard](https://dashboard.edgestore.dev/) where you can create a new project. After creating a new project you will have access to a access key and a secret key.

Add these keys to your `.env.local` file:

```env
EDGE_STORE_ACCESS_KEY=your-access-key
EDGE_STORE_SECRET_KEY=your-secret-key
```

Next, create a folder named `api` inside the `src/app` directory.

Now create a new file `route.ts` inside the src directory at the location `src/app/api/edgestore/[...edgestore]`:

Copy the following into route.ts:

```typescript
import { initEdgeStore } from "@edgestore/server";
import { createEdgeStoreNextHandler } from "@edgestore/server/adapters/next/app";
const es = initEdgeStore.create();

const edgeStoreRouter = es.router({
  publicFiles: es.fileBucket({
    maxSize: 1024 * 1024 * 10, // 10MB
    // accept: ["application/pdf"],
  }),
});

const handler = createEdgeStoreNextHandler({
  router: edgeStoreRouter,
});

export { handler as GET, handler as POST };

export type EdgeStoreRouter = typeof edgeStoreRouter;
```

Here I've created a file upload bucket where the maximum upload size is 10mb and additionally you can also specify the file extensions to be accepted.

For images, edgestore provides a dedicated bucket called `imageBucket` which you can replace with `fileBucket` to dedicate it for images.1

Now we will set up the context provider for our frontend:
For this we create a new file called `edgestore.ts` inside `src/lib`:

Copy the following into `layout.tsx`:

```typescript
"use client";
import { type EdgeStoreRouter } from "../app/api/edgestore/[...edgestore]/route";
import { createEdgeStoreProvider } from "@edgestore/react";
const { EdgeStoreProvider, useEdgeStore } =
  createEdgeStoreProvider<EdgeStoreRouter>();
export { EdgeStoreProvider, useEdgeStore };
```

And then we can wrap our app with the `EdgeStoreProvider`. Copy the following into `src/app/layout.tsx`:

```typescript
import { EdgeStoreProvider } from "../lib/edgestore";
import "./globals.css";

// ...

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>
        <EdgeStoreProvider>{children}</EdgeStoreProvider>
      </body>
    </html>
  );
}
```

We can use the `useEdgeStore` hook to directly upload files from the frontend.

Inside your `page.tsx` copy the following:

```typescript
"use client";

// ..

import { useEdgeStore } from "../lib/edgestore";

export default function Page() {
  // .. state declarations

  const { edgestore } = useEdgeStore();

  return (
    <div className="m-20">
      <input
        type="file"
        onChange={(e) => {
          setFile(e.target.files?.[0]);
        }}
      />
      <button
        onClick={async () => {
          setUrl(null);
          if (file) {
            const res = await edgestore.publicFiles.upload({
              file,
              onProgressChange: (progress) => {
                // you can use this to show a progress bar
                console.log(progress);
                setProgress(progress);
              },
            });
            // you can run some server action or api here
            // to add the necessary data to your database
            console.log(res);
            setUrl(res.url);
            setProgress(null);
          }
        }}
      >
        Upload
      </button>
      <div className="mt-10">
        {progress !== null && <div>Progress: {progress}%</div>}
        {url && (
          <div>
            URL: <Link href={url}>{url}</Link>
          </div>
        )}
      </div>
    </div>
  );
}
```

After this you can try to upload a sample file and you should see something like this after the successful upload:

![Upload Preview](https://cdn.hashnode.com/res/hashnode/image/upload/v1711132052095/kmMsa2Mea.png?auto=format)

And that's it! It's actually lightning fast and super easy to upload files to the cloud without having to setup formData or any API logic!

### Some more functions that edgestore provides

#### Replace file

You can replace an already uploaded file by passing the `replaceTargetUrl` option. The old file will be automatically deleted after the upload.

```typescript
const res = await edgestore.publicFiles.upload({
  file,
  options: {
    replaceTargetUrl: oldFileUrl,
  },
  // ...
});
```

#### Temporary files

Edgestore provides us the option to store temporary files which if not confirmed are deleted within 24 hours.

To upload a temporary file simply add the following to your `options`:

```typescript
options: {
  // ..
  temporary: true,
},
```

To confirm a temporary file:

```typescript
await edgestore.publicFiles.confirmUpload({
  url: urlToConfirm,
});
```

#### Download files

Sometimes the browser displays the file instead of downloading it forcefully, if you want to force that download, use `getDownloadUrl`:

```typescript
import { getDownloadUrl } from "@edgestore/react/utils";

getDownloadUrl(
  url, // the url of the file to download
  "example.pdf" // optional, the name of the file to download
);
```

### Conclusion

When it comes to getting your Next.js apps up and running quickly with file storage, Edgestore is a terrific solution. Many configuration choices covering a wide range of use-cases have been offered  which make it super easy to use.

Edge Store's integration with Next.js is a step towards the development of web apps that are user-focused, user-friendly, and faster in the future.

Read more and discover the full potential of Edge Store by visiting the [official documentation](https://edgestore.dev/docs/quick-start).
