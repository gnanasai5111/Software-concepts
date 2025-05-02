# Next Js
- Its a React framework to build full stack applications.

```
npx create-next-app@latest application-name
```

## Routing 
- Next.js uses File-Based Routing with the app/ directory (introduced in Next.js 13+).
- Routing is driven by the file and folder structure inside the app/ directory.

### Routing Convention
- All routes must reside in the app folder.
- A file named page.tsx or page.jsx is required in each route folder.
- Each folder represents a URL segment.

## Basic Routes
```
app/
├── layout.tsx
├── page.tsx         → '/'
├── about/
│   └── page.tsx     → '/about'
├── contact/
│   └── page.tsx     → '/contact'

```

## Nested Routes
- Nest folders to create Nested Routes
```
app/
└── blog/
    └── post/
        └── page.tsx → '/blog/post'
```

## Dynamic Routes
- Use square brackets [] to define a dynamic segment.
```
app/
└── products/
    └── [productId]/
        └── page.tsx → '/products/:productId'
```

```
import React from "react";

function ProductDetails({ params }: { params: { productId: string } }) {
  return <div>ProductDetails of product {params.productId}</div>;
}

export default ProductDetails;
```

Asynchronous Dynamic Routes
```
import React from "react";

async function ProductDetails({
  params,
}: {
  params: Promise<{ productId: string }>;
}) {
  const { productId } = await params;
  return <div>ProductDetails of product {productId}</div>;
}

export default ProductDetails;
```

## Catch-All Segments
- Next.js supports dynamic routes using catch-all segments, allowing you to match variable-length URL paths.
- **[...slug]** - Matches any number of path segments, and returns them as an array.
```
app/docs/[...slug]/page.tsx

/docs/a → params.slug = ['a']

/docs/a/b/c → params.slug = ['a', 'b', 'c']
```
- **[[...slug]]** - Similar to catch-all, but also matches when no segment is provided (optional).
```
app/docs/[[...slug]]/page.tsx
/docs → params.slug = undefined

/docs/a → params.slug = ['a']

/docs/a/b → params.slug = ['a', 'b']
```

## 404 Page (Not Found)
- Next.js automatically renders a 404 page if no matching route is found.
- To customize this page, create a not-found.tsx file inside the app/ directory.
- In your dynamic route page, you can call notFound() from next/navigation to trigger a 404 response when certain conditions are met. This is useful if you want to display a 404 page based on specific conditions, such as an invalid productId or missing data.

```
import { notFound } from "next/navigation";
import React from "react";

function ProductDetails({ params }: { params: { productId: string } }) {
  const { productId } = params;
  if (parseInt(productId) > 1000) {
    notFound();
  }
  return <div>Product Details of product {productId}</div>;
}

export default ProductDetails;

"use client";
import { usePathname } from "next/navigation";
import React from "react";

function NotFound() {
  const pathname = usePathname();
  return <div>Product Id {pathname.split("/")[2]} not found</div>;
}

export default NotFound;
```
## File Colocation
- File Colocation refers to the practice of placing related files (such as components, styles, and tests) together in the same folder to improve organization and maintainability.
- You can use any file name (except page.tsx or page.ts) for other related files within the same URL segment folder.

## Private Folders
- Private folders are used to contain parts of your application that are not directly part of the public-facing route structure but may still be important for internal functionality (e.g., utilities, authentication, and helpers).Use underscore before a folder to make it as private folder
```
_lib
```

## Route Groups
- Route groups allow you to logically group related routes without affecting the URL structure. This is helpful for organizing and structuring deeply nested routes.
- Route groups are enclosed in parentheses () and it doesnt include in the url segment
```
(auth)
```
## Layouts
- Layouts in Next.js are used to define a shared structure (like headers, footers, navigation, etc.) for specific sections of your application.
- A layout file is created with the name layout.tsx or layout.jsx and placed in the appropriate folder.

## Nested Layouts
- Nested layouts allow you to define different layouts at different levels of the app, enabling you to have specific layouts for specific routes or sections.
```
app/
├── layout.tsx           → Root layout, shared across the app
├── page.tsx             → Root page, accessible at '/'
├── dashboard/
│   ├── layout.tsx       → Dashboard layout, shared across dashboard pages
│   ├── page.tsx         → Dashboard homepage, accessible at '/dashboard'
│   └── settings/
│       └── layout.tsx   → Settings layout, shared across settings pages
│       └── page.tsx     → Settings page, accessible at '/dashboard/settings'

```

## Multiple Root Layouts
- Next.js supports having multiple root layouts for different sections of your app.
- This can be achieved using Route Groups which logically separate layouts into different categories while maintaining clean and organized routing.
```
app/
├── (auth)/
│   ├── layout.tsx       → auth-specific layout
│   └── login.tsx      
├── (app)/
│   ├── layout.tsx       → app-specific layout
│   └── page.tsx       

```


