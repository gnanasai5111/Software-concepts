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
4. All callbacks within the I/O queue are executed. (e.g., file system, sockets). I/O Polling: If there are no ready callbacks, the event loop waits/polls for I/O to complete before continuing.
5. Callbacks in the micro task queues if present are executed. nextTick queue followed by Promise queue.
6. All callbacks in the check queue(setImmediate() callbacks) are executed. 
7. Callbacks in the micro task queues if present are executed. Again, first tasks in the nextTick queue and then tasks in the promise queue.
8. All callbacks in the close queue are executed(e.g., socket.on('close'), stream.on('close'))
9. For one final time in the same loop, the micro task queues are executed. nextTick queue followed by promise queue
