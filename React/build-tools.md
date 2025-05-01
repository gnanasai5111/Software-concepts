## Transpiler
- Transpiling refers to converting code written in one language or syntax into another.
- For example, code written in ES6+ JavaScript (or higher versions like TypeScript) may need to be transpiled into older JavaScript versions that are compatible with older browser

Common tools for this are:
**Babel**: Transpiles modern JavaScript (ES6+) or TypeScript into backwards-compatible JavaScript.
**TypeScript Compiler (tsc)**: Compiles TypeScript files into JavaScript.

## Bundling
- Bundling is the process of combining multiple files (e.g., JavaScript, CSS, images, etc.) into a single or smaller set of files to
 improve performance.
- This minimizes the number of requests the browser needs to make when loading the application.
- Bundlers (like Webpack, Parcel, and Vite) take all your application files (JS, CSS, images) and combine them into optimized bundles.



### Webpack
Its a highly configurable JavaScript module bundler widely used in production-grade apps.

**Key Features:**
- Full control over build via `webpack.config.js`
- Supports **loaders** and **plugins** (e.g., Babel, Sass, image handling)
- **Code splitting** using `import()` and SplitChunks
- **Tree shaking** (removes unused code)
- **Hot Module Replacement (HMR)**
- Supports legacy browsers well
- Massive plugin ecosystem

### Vite
Vite is a modern build tool focused on speed and optimization, specifically designed to improve the development experience
- Vite serves files directly using native ES modules during development, allowing instant reloading and fast start-up times.
 This eliminates the need for bundling during development.
- Vite uses Rollup under the hood for bundling in production, which results in highly optimized and minimal bundles.
- Rollup is a JavaScript module bundler designed primarily for production builds.

**Key Features:**
- **Instant dev server startup** using ESBuild
- **Lightning-fast HMR**
- **Built-in support** for React, Vue, TypeScript, JSX, CSS
- **Automatic code splitting**
- **Tree shaking** with Rollup in production
- **Minimal or zero configuration**
- Fastest developer experience available

### Parcel
A zero-config bundler that works out of the box with smart defaults and parallel processing.

**Key Features:**
- **No config needed** — auto detects file types and settings
- **Built-in TypeScript, JSX, SCSS** support
- **Automatic code splitting and tree shaking**
- **Parallel bundling** for faster builds
- **HMR built-in**
- Simpler setup than Webpack with more features than Vite by default



### When to Use Which

1. Webpack : Webpack is highly configurable and works well for complex projects where you need full control over the build process. 
2.  Vite : Fast development, modern stack (React/Vue/TS).
3. Parcel :  Parcel is great for projects that need a simple, fast, and hassle-free setup. It's perfect for small to medium-sized
applications where configuration complexity isn't required.

## TreeShaking 
- Tree Shaking is a technique used to remove unused code from your final bundle during the build process.
- It ensures that only the code you actually use in your application gets included in the final production bundle, leading to smaller file sizes and faster load times.

## Hot module replacement
- Hot Module Replacement (HMR) is a feature that allows modules (pieces of your app) to be updated in the browser without requiring a full page reload. This makes the development experience faster and more efficient.

