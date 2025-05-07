# Node js
- Node.js is a powerful, open-source, and cross-platform JavaScript runtime environment .
- It lets you run Javascript outside of the browser.
- Built on the V8 JavaScript engine (used in Chrome)
- Uses an event-driven, non-blocking I/O model, making it efficient and scalable for real-time applications.
- npm (Node Package Manager) comes bundled with Node.js and is used to manage libraries & dependencies.

## ECMA script
- ECMAScript is the standard specification that defines how JavaScript should work.
- JavaScript is an implementation of the ECMAScript standard.

## JavaScript Engine
- A JavaScript engine is a program that executes JavaScript code.
- It parses,compiles and executes the code.


## JavaScript Runtime Environment
- A JavaScript runtime provides the environment in which JavaScript code can execute.
- It includes JavaScript engine (like V8), APIs for I/O, timers, file system, networking, etc. and Call stack, event loop, and callback queue.

## Common Js and ES Modules
- CommonJS and ES Modules are two different module systems used in JavaScript to organize and reuse code across files.
- CommonJS is the original module system used in Node.js and relies on require() to import modules and module.exports to export them.It loads modules synchronously, meaning at runtime, which works well in server-side environments like Node.js but not in the browser.
- On the other hand, ES Modules (ESM) is the modern JavaScript module standard introduced in ES6. It uses import and export syntax, and modules are loaded asynchronously, making them suitable for both browsers and modern Node.js environments (from version 12+).
- ESM supports advanced features like tree shaking (removing unused code) and top-level await, and is now the preferred choice for writing modular, modern JavaScript.
- To use ESM in Node.js, files need to have a .mjs extension or "type": "module" must be set in the package.json.
-  While CommonJS is still widely used in legacy code, ES Modules are becoming the standard for future JavaScript development.

## Modules
- Modules are encapsulated and resusable chunks of code. Each File can be treated as a Module
3 Types
. Local Modules - Modules which we create in our application.
2. Built-in Modules - Modlues which comes built-in with node js.
3. Third party Modules - Modules which are written by other developers, which we can use.


**Common Js Named Export**
``` 
const add = (a, b) => a + b;
const subtract = (a, b) => a - b;

module.exports = {
  add,
  subtract
};
```
**Common Js Named Import**
```
const { add, subtract } = require('./math');
```

**Common Js Default Export**
```
const add = (a, b) => a + b;
module.exports = add;
```

**Common Js Default Import**
```
const add = require('./math');
```

**ES MODULES Named Export** 
``` 
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;
```
**ES MODULES Named Import**
```
import { add, subtract } from './math.mjs';
```

**ES MODULES Default Export**
```
const add = (a, b) => a + b;
export default add;
```

**ES MODULES Default Import**
```
import add from './math.mjs';
```

## Module Wrapper 
- In Node.js, every file is treated as a separate module.
- Before execution, Node wraps your code inside a function. This is known as the Module Wrapper Function.
- This gives each file a private scope and access to special variables.
```
(function (exports, require, module, __filename, __dirname) {
  // Your actual code lives here
});
```
### Imediately Invoked Function Expression ((IIFE)
- The module wrapper is an IIFE – a function that is defined and invoked immediately.
- 
**Parameters Injected by Node.js**
  
1. exports –  shortcut to module.exports for exporting data.
2. require – to import other modules.
3. module –  holds metadata and is used to export values.
4. __filename – the absolute path to the current file.
5. __dirname – the absolute path to the current directory.
