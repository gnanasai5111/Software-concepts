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

## Built-in modules
- Modules that Node js comes with.

###1. Path Module
- It provides utilities for working with file and directory paths.
```
const path = require('path');
```
**path.basename()**
- It returns the last Portion of a path
```
path.basename('/foo/bar/baz.txt'); // 'baz.txt'
```
**path.extname()**
- It returns the extension of the path
```
path.extname('/foo/bar/baz.txt'); // '.txt'
```
**path.join()**
- Joins all given path segments together and normalizes the resulting path.
```
path.join('/foo', 'bar', 'baz.txt'); // '/foo/bar/baz.txt'
```
**path.resolve()**
- Resolves a sequence of paths into an absolute path.
- It Provides absolute path if no path starts with /.
- If a path starts with /, it starts building from there.
```
path.resolve('foo', 'bar'); // '/current/working/dir/foo/bar'
path.resolve('/foo', 'bar');// '/foo/bar'
```

###2. Events Module
- Event is an action or an occurence that has happened in our application that we can respond to.
- The events module allows you to create and handle custom events using the EventEmitter class.
```
const EventEmitter = require('events');
const emitter = new EventEmitter();

emitter.on('message', (data) => {
  console.log(`Message received: ${data}`);
});
// Attaches a listener (callback) for the specified event.

emitter.emit('message', 'Hello from Node.js!');
Triggers the event and calls all attached listeners.
```

## Character sets and Encoding
- A character set means Predefined set of charcters that represent numbers.
- Examples: ASCII, UTF-8, UTF-16.
- Encoding dictates how to represent the number in a charcter set as binary data.

## Stream
- The stream module in Node.js provides an abstraction for working with streaming data.
- Stream is a sequence of data that is moved from one point to another over time. It allows handling data in chunks rather than loading it all at once, which is efficient for both memory usage and performance.

4 Types of stream
- **Readable** :  data can be read from (e.g., file read).
- **Writable** : data can be written to (e.g., file write).
- **Duplex** : data can be read and written (e.g., TCP sockets).
- **Transform** : can modify data while reading/writing (e.g., compression).

## Buffer
- A Buffer is a chunk of data stored in memory.
- Node.js uses Buffer to handle raw binary streams, like file I/O or network packets.
- Buffers are useful for working with binary data directly.
```
const buf = Buffer.from('Hello World!');
console.log(buf); // <Buffer 48 65 6c 6c 6f 20 57 6f 72 6c 64 21>
```

## fs module
- The fs module allows interaction with the file system: reading, writing, updating files.

```
const fs = require("fs");

//Synchronous read
const fileContent = fs.readFileSync("./hello.txt", "utf-8");
console.log(fileContent);

//Asynchronous read
fs.readFile("./hello.txt", "utf-8", (error, data) => {
  if (error) {
    console.log(error);
  } else {
    console.log(data);
  }
});

//Synchronous write
fs.writeFileSync("./greet.txt", "hello world");

//Asynchronous write (append mode with flag)
fs.writeFile("./greet.txt", "Good Morning", { flag: "a" }, (error) => {
  console.log(error);
});
```

## Pipe 
- A pipe connects the output of a readable stream directly into a writable stream.
- It allows data to flow automatically from one stream to another.
- Helps in chaining operations like reading a file and writing its contents to another file or compressing data.
```
const fs = require("fs");

const readable = fs.createReadStream("input.txt");
const writable = fs.createWriteStream("output.txt");

readable.pipe(writable);
```

## HTTP
- Hypertext Transfer Protocol (HTTP) is an application-layer protocol for transmitting hypermedia documents, such as HTML. It was designed for communication between web browsers and web servers.

```
const http = require("http");

const server = http.createServer((req, res) => {
  if (req.url === "/") {
    res.writeHead(200, { "Content-Type": "text/plain" }); 
    res.write("Home Page");
  } else if (req.url === "/about") {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.write("About Page");
  } else {
    res.statusCode = 404;
    res.write("Page Not Found");
  }
  res.end();
});

server.listen(3000, () => {
  console.log("Server is running on Port 3000");
});
```

