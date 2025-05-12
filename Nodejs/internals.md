# libuv
- Its a cross platform open source library written in c language.
- It handles asynchronous non-blocking operations in node js.
1. Thread Pool
2. Event loop etc
3. TCP/UDP sockets
4. File system operations
5. Timers, and more.

## Thread Pool
- A pool of background threads used by Node.js (via libuv) to perform expensive, blocking operations asynchronously, without blocking the main event loop.
- Node.js uses libuv which has a default thread pool of 4 threads.
ex: File system operations (fs.readFile, fs.writeFile), CPU-intensive crypto (crypto.pbkdf2, scrypt), Compression (zlib),DNS lookups (dns.lookup)

### Network I/O
- For network Requests, libuv does not use the thread pool. It uses native async mechanism  OS kernel's async I/O APIs (like epoll, kqueue, IOCP) whenever possible.
- libuv assigns the work to the OS, and then polls the kernel to check if the work is done.This is more efficient than using threads.

## Event Loop
- It is a c program and part of libuv.
- Since Node js is a single threaded language, event loop manages all the asynchronous operations by using thread pool or  by offloading operations to the system kernel whenever possible.


![image](https://github.com/user-attachments/assets/88600b8c-2cdb-4049-8daa-99aecaad1b09)

1. Any callbacks in the micro task queues are executed. First, tasks in the nextTick queue(process.nextTick() callbacks) and only then tasks in the promise queue(Promise callbacks (.then, .catch, .finally))
2. All callbacks(setTimeout() and setInterval() callbacks) within the timer queue are executed.
3. Callbacks in the micro task queues if present are executed. Again, first tasks in the nextTick queue and then tasks in the promise queue.
4. All callbacks within the I/O queue are executed. (e.g., file system, sockets).  If no I/O is ready yet, Node.js waits (polls) for a short time to check if any I/O gets completed before moving to the next step.
5. Callbacks in the micro task queues if present are executed. nextTick queue followed by Promise queue.
6. All callbacks in the check queue(setImmediate() callbacks) are executed. 
7. Callbacks in the micro task queues if present are executed. Again, first tasks in the nextTick queue and then tasks in the promise queue.
8. All callbacks in the close queue are executed(e.g., socket.on('close'), stream.on('close'))
9. For one final time in the same loop, the micro task queues are executed. nextTick queue followed by promise queue

## NPM (Node Package Manager)
- npm is the default package manager for Node.js.
- It helps install, manage, and share JavaScript packages (modules).

Common commands:
1. npm init: Starts creating a package.json file (interactive).
2. npm init -y: Creates a default package.json file.
3. npm install <package>: Installs a package locally.
4. npm install -g <package>: Installs globally.
5. npm uninstall <package>: Removes a package.

## package.json
- A file that holds metadata about your project and its dependencies.
- It is essential for every Node.js project.

Key fields:

1. "name" – Project name
2. "version" – Current version of your app
### Versioning
- It follows semantic versioning
- Format is X.Y.Z

- X Indicates MAJOR	Breaking changes
- Y Indicates MINOR	New features, backward compatible
- Z Indacates PATCH	Bug fixes only

3. "description" – A short description
4. "main" – Entry point file (e.g., index.js)
5. "scripts" – Custom commands you can run using npm run
```
// Use them with: npm run <script-name>
"scripts": {
  "start": "node app.js",
  "dev": "nodemon app.js",
  "test": "jest"
}
```

6. "dependencies" – Runtime packages
7. "devDependencies" – Development-only packages

- For publishing npm package use
```
npm login //Enter login details
npm publish
```

## Cluster Module
- Clustering in Node.js is a technique used to improve application performance and scalability by creating multiple worker processes that can handle incoming requests concurrently.
- This approach fully utilizes multi-core CPUs, addressing Node.js’s limitation of being single-threaded by default.
- A master (primary) process uses cluster.fork() to spawn worker processes.
- Each worker is an independent Node.js process with its own event loop, memory, and V8 instance.
- All workers share the same server port, enabling load-balanced request handling.
- The master process manages the workers: Distributes incoming connections and Listens for worker exits/crashes and can restart workers if needed.

```
const http = require("http");
const cluster = require("cluster");
const os = require("os");

const numCPUs = os.cpus().length;

if (cluster.isMaster) {
  console.log(`Master ${process.pid} is running`);

  // Fork workers equal to the number of CPU cores
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  // Handle worker exit and respawn
  cluster.on("exit", (worker, code, signal) => {
    console.log(`Worker ${worker.process.pid} died. Restarting...`);
    cluster.fork();
  });

} else {
  console.log(`Worker ${process.pid} started`);

  const server = http.createServer((req, res) => {
    if (req.url === "/") {
      res.writeHead(200, { "Content-Type": "text/plain" });
      res.write(`Home Page - served by ${process.pid}`);
    } else if (req.url === "/about") {
      res.writeHead(200, { "Content-Type": "text/plain" });
      res.write(`About Page - served by ${process.pid}`);
    } else {
      res.statusCode = 404;
      res.write("Page Not Found");
    }
    res.end();
  });

  server.listen(3000, () => {
    console.log(`Server running at http://localhost:3000 - PID: ${process.pid}`);
  });
}
```

## Worker Threads Module
- Worker Threads allow you to run JavaScript code in parallel within a single Node.js process.
- It is useful for CPU-intensive tasks like image processing, large data parsing, or complex calculations.
- when process isolation is not needed,that is, no seperate instance of v8,event loop and memory are needed, you should use worker_threads.

**main-thread.js**
```
const http = require("http");
const { Worker } = require("worker_threads");

const server = http.createServer((req, res) => {
  if (req.url === "/") {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.write("Home Page");
    res.end();
  } else if (req.url === "/slow-page") {
    const worker = new Worker("./worker-thread.js");

    worker.on("message", (j) => {
      res.writeHead(200, { "Content-Type": "text/plain" });
      res.write(`Slow Page ${j}`);
      res.end();
    });
  } else {
    res.statusCode = 404;
    res.write("Page Not Found");
    res.end();
  }
});

server.listen(3000, () => {
  console.log("Server is running on Port 3000");
});
```

**worker-thread.js**
```
const { parentPort } = require("worker_threads");
let j = 0;
while (j < 6000000000) {
  j++;
}
parentPort.postMessage(j);
```


