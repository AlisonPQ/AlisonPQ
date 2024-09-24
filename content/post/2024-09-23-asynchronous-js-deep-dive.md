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

## The Necessity of Callbacks

> "I will call back later!"

- A callback is a function passed as an argument to another function
- This technique allows a function to call another function
- A callback function can run after another function has finished

> Where callbacks really shine are in asynchronous functions, where one function has to wait for another function (like waiting for a file to load).

### Asynchronous Coding and Callbacks

When you are using callbaks, avoid to use `()` to invoke the callback function.

``` JavaScript
let determineTotal = function() {
    let total = 0,
        count = 0;

    processStudents(students, function(obj) {
        total = total + obj.score;
        count++;
    });

    console.log("Total Score: " + total + " - Total Count: " + count);
}

setTimeout(determineTotal, 0);
```

Where: `setTimeout(determineTotal, 0);`

### Problems with JavaScript Callbacks

- **Callback** hell, it is related to a bunch of nested callbacks becomes very difficult to work with callbacks.
- **Difficult to reason about**, if you have a lot of callbacks, that's what makes it difficult to reason about.
- **Inversion of control**, you cannot have callbacks is you turn control of your program over to something for example, if you are using asynchronous coding to connect with a server and get data wich you would need to do that control is turned over to something on the server or you may be using an API call that uses asynchronous coding that uses callbacks and you don't have control of that code.
