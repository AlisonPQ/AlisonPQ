---
title: 'Data Structures Notes'
date: 2024-08-25T14:08:58-04:00
draft: true
---

Here are some notes about data structures.

- [Arrays](#arrays)
  - [Static Array](#static-array)
  - [Dinamic Array](#dinamic-array)
- [Hash Tables](#hash-tables)
  - [Hash function](#hash-function)
  - [Hash Collitions](#hash-collitions)
  
## Arrays

| Method | Big O | Observation |
| ------ | ----- | ----------- |
| Lookup | O(1)  |             |
| Push   | O(1)  | can be O(n) |
| Insert | O(n)  |             |
| Delete | O(n)  |             |

### Static Array

Fixed in size.

```
int[] staticArray = new int[3]; 
```

### Dinamic Array

Dynamic arrays can change size during runtime

```
List<T> dynamicArray = new List<T>();
```

> Note: While JavaScript arrays are dynamic by nature, you can treat an array as "static" by not modifying its size after initialization. There’s no enforcement mechanism for static arrays in JavaScript itself, but the concept is more about intent.

## Hash Tables

**Hash Tables** or Hash Maps, Maps, Unordered Maps, Dictionaries, Objects. There are many ways to call this Data Structure, depending of the programming language.

Consider:

![](/img/hashtable.jpg)

### Hash function

It is something that is used all across computer science, a hash function that generates a value of fixed length for each input that it gets.

There is many types of hash function, e.g. MD5, SHA-1, SHA-256.

MD5 Hash Example:

```
input: hello
output: 5d41402abc4b2a76b9719d911017c592
````

**Hash Functions key aspects**:

* One way (if you give somebody a key, they have no idea what the input was, it means that is impossible to have any clue as to what the input is)
* Function given an input always outputs tha same output (no matter how many times I put "hello" as input, output is going to be the same, notice tha capital letters matters)

Hash Table Data Structure gets really fast data access. All it needs it is an input into a hash function like MD5, it generates a number like `5d41402abc4b2a76b9719d911017c592` and inmediately know where it is in computer memory.

Technically a hash function that is used for hash tables is going to take a `input`, generate some sort of gibberish, and then convert it to an index space or an address space that it has based on this number unlike a race where we just had ordered indexes with hash tables, all we need to do is give it a key and we know exactly where that item is in our memory.

But you might be wondering, this black box (hash function), doesn't it slow things down? because every time we want to add a property and the value to a hash table we have to run it through tha hash function so we can decide where to put it in memory and if you have noticed that good job, that is a big factor.

You don't want this to take a very long time because, well, every time you add a property to memory or retrive a property to memory, because, again, we both times we are sending the key into the hash function to find where to get it from, so we need this to be really, really fast.

And underneath the hood, remember, because hash tables exist in all languages, they are implemented with an optimum hashing function that is really, really fast.

**Note**: Hash functions like SHA-256 take a really long time to generate a hash and it is an overly complex hashing function that is used a lot in places like cryptography where you want this to take longer.

To review, a key is sent to through a hash function that is going to hash something really, really fast and then map whatever the hash come out be into a memory address where we wants to store our data.

And when it comes to hashing functions, you tipically leave this to whaever framework or language you are using

Usually assume a time complexity or big O notation as O(1) because it happens really fast.

### Hash Collitions

| Method | Big O |
| ------ | ----- |
| Insert | O(1)  |
| Lookup | O(1)  |
| Delete | O(1)  |
| Push   | O(1)  |

 
