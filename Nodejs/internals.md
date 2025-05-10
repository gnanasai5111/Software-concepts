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


