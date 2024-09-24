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
  
## Promises

- A Promise is an Object with Properties an Methods.
- Represents the Eventual Completion or Failure of an Asynchronous Operation.
- Provides a Resulting Value.

### A Quick Overview of Fetch

[Fecth](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as requests and responses.

### Promises examples

Example:

``` JavaScript
"use strict";

let wordnikWords = "http://api.wordnik.com/v4/words.json/",
    wordnikWord = "http://api.wordnik.com/v4/word.json/",
    apiKey = "?api_key=[API_KEY]]",
    wordObj;

fetch(wordnikWords + "randomWord" + apiKey)
.then(function(response) {
    wordObj = response;
    return response.json();
})
.then(function(data) {
    console.log(data.word);
    return fetch(wordnikWord + data.word + "/definitions" + apiKey);
})
.then(function(def) {
    return def.json();
})
.then(function(def) {
    console.log(def);
})
.catch(function(err) {
    console.log(err);
});
```

We can retrieve data with Fetch helps, we can access to data using `then` and `catch` to handle errors.

``` JavaScript
"use strict";

// GETTING DATA
/*fetch('https://jsonplaceholder.typicode.com/todos/5')
.then(data => data.json())
.then(obj => console.log(obj));*/

// POSTING DATA
let todo = {
    completed: false,
    userId: 1,
    title: "Learn Promises"
};

fetch('https://sonplaceholder.typicode.com/todos/', {
    method: 'POST',
    headers: {
        "Content-type": "application/json"
    },
    body: JSON.stringify(todo)
})
.then(resp => resp.json())
.then(obj => console.log(obj))
.catch(reject => console.log(`Unable to create todo ${reject}`));

console.log('Other code');
```

### IIFEs

Immediately Invoked Function Expression, is a JavaScript function that runs as soon as it is defined. The name IIFE is promoted by Ben Alman.

``` JavaScript
// IIFE
(function () {
  /* ... */
})();
```

``` JavaScript
// Arrow Function IIFE
(() => {
  /* ... */
})();
```

``` JavaScript
// async IIFE
(async () => {
  /* ... */
})();
```

### Creating JS Promises

``` JavaScript
"use strict"

let setTimeoutPromise = function(time) {
    return new Promise(function(res, rej) {
        if (isNaN(time)) {
            rej("A number is required.");
        }
        setTimeout(res, time);
    });
};

setTimeoutPromise(2000) 
// Change value to "word" as parameter to check the error
    .then(function() {
        console.log("Done");
    })
    .catch(function(err) {
        console.error(err);
    });
```

### Finally feature

The finally() method returns a Promise. When the promise is finally either fulfilled or rejected, the specified callback function is executed. This provides a way for code to be run whether the promise was fulfilled successfully, or instead rejected.

### Promise.all

The `Promise.all()` method takes an iterable of promises as an input, and returns a single Promise that resolves to an array of the results of the input promises.

``` JavaScript
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'foo');
});

Promise.all([promise1, promise2, promise3]).then((values) => {
  console.log(values);
});
// expected output: Array [3, 42, "foo"]
```

This returned promise will resolve when all of the input's promises have resolved, or if the input iterable contains no promises. It rejects immediately upon any of the input promises rejecting or non-promises throwing an error, and will reject with this first rejection message / error.

### Promise.race

The `Promise.race()` method returns a promise that fulfills or rejects as soon as one of the promises in an iterable fulfills or rejects, with the value or reason from that promise.

``` JavaScript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(resolve, 500, 'one');
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'two');
});

Promise.race([promise1, promise2]).then((value) => {
  console.log(value);
  // Both resolve, but promise2 is faster
});
// expected output: "two"
```

### Promise.allSettled

The `Promise.allSettled()` method returns a promise that resolves after all of the given promises have either fulfilled or rejected, with an array of objects that each describes the outcome of each promise.

It is typically used when you have multiple asynchronous tasks that are not dependent on one another to complete successfully, or you'd always like to know the result of each promise.

In comparison, the Promise returned by `Promise.all()` may be more appropriate if the tasks are dependent on each other / if you'd like to immediately reject upon any of them rejecting.

``` JavaScript
const promise1 = Promise.resolve(3);
const promise2 = new Promise((resolve, reject) => setTimeout(reject, 100, 'foo'));
const promises = [promise1, promise2];

Promise.allSettled(promises).
  then((results) => results.forEach((result) => console.log(result.status)));

// expected output:
// "fulfilled"
// "rejected"
```

### Promise.any

`Promise.any()` takes an iterable of `Promise` objects.
It returns a single promise that resolves as soon as any of the promises in the iterable fulfills, with the value of the fulfilled promise. If no promises in the iterable fulfill (if all of the given promises are rejected), then the returned promise is rejected with an `AggregateError`, a new subclass of `Error` that groups together individual errors.
