# What is the Event loop

How does JavaScript even work

Javascript: 
- Single Thread
- non-blocking
- asynchronous
- concurrent

and 

- Call stack
- event loop
- callback queue
- other apis

### JS runtime

heap stack

setTimeout DOM I/O

### Call Stack

one thread == one call stack == one thing at a time

报错是否会抛出Stack track，他是调用栈追踪

Maximum call stack size exceeded： Chrome will throw this error when call a function recursively

### Blocking

What happens when things are slow?
Single Thread
But why？
We

So solution? asynchronous callbacks

### Concurrency & the Event loop

One thing at a time except not really

####

- any function that other function call
- asynchronous callback
