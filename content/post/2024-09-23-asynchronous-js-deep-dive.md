---
title: 'Asynchronous Deep Dive - JavaScript'
date: 2024-09-23T22:13:24-04:00
draft: true
---

## Understanding Asynchronous Coding

### Synchronous VS Asynchronous

- **Synchronous** code is executed line by line.
- **Asynchronous** means that things can happen independently of the main program flow.

> Callbacks are very important pattern for achieving asynchronous code.

### Advantages and Disadvantages

Synchronous Code:
Advantages

- Easy to write and reason about

Disadvantages

- May create blocking code
- Less performant

Asynchronous Code:

Advantages

- Very performant
- Eliminates code blocking

Disadvantages

- It can be difficult to reason about
- Hader to write

### Understanding the Event Loop

Consider:

``` JavaScript
/*EVENT LOOP - Synchronous*/
while isNotEmpty(eventQueue) {
    // pull out first item from event queue
    // Follorw the execution logic until call stack empty
}
```

Notes:

- **Call stack:** asynchronous code
- **Callback queue:** for a callback queue function to execute there must be no instruction executing on the call stack or a function being executed ahead of the callback queue
