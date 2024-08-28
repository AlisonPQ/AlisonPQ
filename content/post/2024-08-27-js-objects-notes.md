---
title: 'JavaScript Objects Notes'
date: 2024-08-27T19:27:06-04:00
draft: true
---

## Understanding Objects in JavaScript

Some time ago when I was learning JavaScript coming from Object Oriented Programming using Strongly Typed Languages, I wrote some notes, in order to understand how objects work in JavaScript, I saw most of these notes on some videos and lectures. Well, here they are:

### Reference Type

Number, boolean, string, null, undefined, are defined by the language, so they are **Primitive Types**.

Reference type is a non primitive type, are not defined by programming languages, it means that they are created by programmer.

Consider:

```JavaScript
// Objects created by the programmer
var object1 = { value = 5 };
var object2 = object1             // Reference object 1
var object3 = { value = 5 };
```

When we created Object with a value, an object two equals object one and then object three with the same value as the first object.

Object 2 says: "I want whatever is inside the object 1".
Instead Object 3, gets created from scratch.

That is why `object1 === object2 //false` or `[] === []` is `false`, because they are diferente data structures, so at the end arrays are objects.

### Context

`Context` gets confused a lot with `Scope`.

`Scope` is created when it sees curly brackets, when a function is created as soon as it is created that function, there is a new scope.

On following example, `min` variable lives within this universe, it does not anything about root scope, that is why you get `ReferenceError` if you try to access to `min` or `max` for example.

```JavaScript
function randomInteger(n) {
  let min = 5;
  let max = 15;
  let randomInteger = Math.floor(Math.random() * (max - min + 1)) + min;
  console.log(randomInteger); 
}
```

Buuut, what is `Context` so?

`Context` tells you where you are within the object. If you go to the browser in inspector mode, right over the console and you write `console.log(this)`, where `this` (is a special word in JS) is the Window Object

You can access to alert with:

```JavaScript
this.alert('Hello worl!')
```

So, `this` means that is the object environment that you are in, again `this` just refers to what object it is inside of.

### Instantation

Instantiation is when you make a copy of an object and reuse the code. 

Let's imagine that you are building a big multiplayer game online and this game is going to have many, many players. The game can have wizards, trolls, warlocks,..., if you have to create an object for every single  player, that is a lot of repeated code, hassle and that is a lot of time, for sure it is not really very efficient. That is why you can do something called `Instantiation`, making instances or multiple copies of an object.

When you create a class, a player class says "every time I am making a copy of a player the first thing that gets run is the constructor function"

Example:

```JavaScript
// Instantiation in JS
class Player {
  constructor(name, type) {
    this.name = name;
    this.type = type;
  }

  introduce() {
    console.log(`Hi I am ${this.name}, I am a ${this.type}`);
  }
}

class Wizard extends Player {
  constructor(name, type) {
    super(name, type);
  }

  play() {
    console.log(`Hey! I am a ${this.type}`);
  }
}

// Instantiating Wizards

const wizard1 = new Wizard('Shelly','Healer');
const wizard1 = new Wizard('Shawn','Dark Magic');
```

Classical Inheritance

```JavaScript
var Player = function(name, type) {
  this.name = name;
  this.type = type;
}

PLayer.prototype.introduce = function() {
  console.log(`Hi I am ${this.name}, I am a ${this.type}`);
}

// Instantiating Wizards

const wizard1 = new Wizard('Shelly','Healer');
const wizard1 = new Wizard('Shawn','Dark Magic');

wizard1.play = function() {
  console.log(`Hey! I am a ${this.type}`);
}

wizard2.play = function() {
  console.log(`Hey! I am a ${this.type}`);
}
```

> **Note:** Maybe, I should say..."this story will continue", you know JS is high.
