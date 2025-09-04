## What is NodeJS?
Node.js is a single-threaded JavaScript runtime. It's not a language or a framework, but an environment that allows you to write JavaScript that interacts with different parts of the outside world beyond the browser.

## What does it mean by single-threaded?
NodeJS is a single-threaded platform. This means that it can only process one request at a time.

## How does Node.js handle multiple requests?
The event-driven model is very efficient and allows NodeJS to handle thousands of concurrent requests with ease.
Node.js uses two concepts
- Non-blocking I/O
- Asynchronous
[[Non-Blocking I-o image.png]]
![[Non-Blocking I-o image.png]]
Whenever a client sends a request the single thread will send that request to someone else. The current thread will not be busy working with that request. There are workers working for the server. The server sends the request to the worker, the worker further sends it to the other server and waits for the response. In the meantime if there is another request the thread will send it to another worker and the worker will wait for the response from the another server.

In this way the single thread will always be available to take the requests from the client. It will not block the requests.

## How is NodeJS better than traditional multithreaded request response model?
With traditional multithreaded request/response model, every client gets a different thread where as with NodeJS, the simpler request are all handled directly by the **EventLoop.** This is an optimization of thread pool resources and there is no overhead of creating the threads for every client request.