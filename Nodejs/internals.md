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
- For network Requests, libuv uses native async mechanism to avoid blocking main thread. It assigns works to operating system kernel and whenever possible it polls the kernel and see if the request has been completed.

## Event Loop
- It is a c program and part of libuv.
- Since Node js is a single threaded language, event loop manages all the asynchronous operations by using thread pool or  by offloading operations to the system kernel whenever possible.

![image](https://github.com/user-attachments/assets/88600b8c-2cdb-4049-8daa-99aecaad1b09)
