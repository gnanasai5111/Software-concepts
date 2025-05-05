## Rendering
- It is the process of transforming the component code you wrote into user interfaces that user can see and interact with.

## Client Side Rendering(CSR)
- Client-Side Rendering (CSR) is a web rendering technique where the browser downloads a bare HTML file and a JavaScript bundle.
- The HTML file typically contains only a root <div> (e.g., <div id="root"></div>), and the JavaScript handles rendering the actual content in the browser.
- The content becomes visible only after the JavaScript bundle is fully downloaded, parsed, and executed.
- Initial page load is slow, especially on slower networks or devices, because the user sees a blank screen until JavaScript is loaded and runs.
- Subsequent navigation is fast since it's handled on the client without full page reloads (SPA behavior).
-  Not ideal for SEO, because search engine crawlers might not see any meaningful HTML content unless pre-rendering or SSR is added.
-  Best suited for highly interactive applications like dashboards, admin panels, and internal tools where SEO is not a priority.

## Server Side Rendering(SSR)
- Server-Side Rendering (SSR) is a web rendering technique where the HTML content is generated on the server and sent to the browser fully rendered.
- When the user visits a page, the server Runs the JavaScript, Fetches required data, Generates complete HTML,And sends that HTML to the browser.
- The browser displays the page immediately, as the HTML already has the content.
- After showing the page, the browser downloads and runs JavaScript to make the page interactive (this step is called hydration).
- Initial load is fast, and the page is SEO-friendly, because search engines see the full content right away.
- Server handles more work, so it can increase server load and may be slower for complex apps with lots of users.

###  Hydration
- Hydration is the process where the browser takes over a pre-rendered HTML page (from SSR) and attaches event listeners and JavaScript logic to make it interactive.

## Static Site Generation
- SSG is a technique where the HTML for each page is generated at build time, not at runtime.
- During the build process (when deploying your app), the server generates static HTML files for all the pages.
- When a user visits a page, they receive pre-built HTML, and no server-side processing is required to render the page.
- JavaScript is downloaded after the page loads to make it interactive (like React's client-side hydration).

## React Server Components(RSC)
- React Server Components introduce a new way to build apps by splitting components into two types, each with different responsibilities.

### Server components
- Run only on the server.
- Fetch data and prepare HTML before sending it to the browser.
- Result in smaller client bundles.
- Cannot handle user interactions or browser-specific logic (useState, useEffect, etc.).
- In next.js , components are server components by default.

## Client Components
- They run in the browser and also Handles all interactive logic like forms, buttons, animations, etc.
- Can still receive an initial server-rendered HTML for faster page loads.
- Must be marked with "use client" at the top of the file.

## Server Rendering strategies

### Static Rendering
- Static rendering refers to generating the HTML at build time on the server before any user requests are made.
- Once generated, the HTML is cached and served as a static file for every user request, typically from a CDN.
- The result is a highly optimized, fast-loading page that doesn't require additional processing on the server when it's requested.

### Dynamic Rendering
- Dynamic rendering refers to generating the HTML on each request (server-side), rather than at build time.
- The content is rendered dynamically based on factors like the user’s request, session, or real-time data from a database or an API.

## generateStaticParams
- Used in dynamic routes to tell Next.js which pages to pre-render at build time.
- Improves performance by generating HTML ahead of time.

```
export async function generateStaticParams() {
  return [
    { id: '1' },
    { id: '2' },
    { id: '3' },
  ];
}
```
- So, Next.js will generate those 3 pages at build time, making them load very fast.

## dynamicParams
- Its Used in dynamic routes . It decides if other paths (not listed in generateStaticParams) should work.
```
export const dynamicParams = true;
```
- If its true, Any path will work and Page is rendered on-demand.
- If its false, Only the paths in generateStaticParams will work and All other paths will return a 404 error.

## Streaming
- Streaming means sending parts of the HTML(chunks) to the browser as soon as they’re ready, instead of waiting for the whole page to be rendered on the server.
- It’s useful for showing faster loading experiences (like loading spinners or shells) while the full content is still loading.
```
<Suspense fallback={<Loading />}>
  <HeavyComponent />
</Suspense>
```





