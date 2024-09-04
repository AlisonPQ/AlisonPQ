---
title: 'Data Structures Notes'
date: 2024-08-25T14:08:58-04:00
draft: true
---

Here are some notes about data structures.

### Arrays

| Method | Big O | Observation |
| ------ | ----- | ----------- |
| Lookup | O(1)  |             |
| Push   | O(1)  | can be O(n) |
| Insert | O(n)  |             |
| Delete | O(n)  |             |

#### Static Array

Fixed in size.

```
int[] staticArray = new int[3]; 
```

#### Dinamic Array

Dynamic arrays can change size during runtime

```
List<T> dynamicArray = new List<T>();
```

> Note: While JavaScript arrays are dynamic by nature, you can treat an array as "static" by not modifying its size after initialization. There’s no enforcement mechanism for static arrays in JavaScript itself, but the concept is more about intent.

### Hash Tables

**Hash Tables** or Hash Maps, Maps, Unordered Maps, Dictionaries, Objects. There are many ways to call this Data Structure, depending of the programming language.

#### Hash function

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

Technically a hash function that is used for hash tables is going to take a `input`, generate some sort of gibberish, and then convert it to an index space or an address space that it has based on this number unlike a race where we just had ordered indexes with hash tables, all we need to do is give it a key and we know exactly where that item is in our memory but you might be wondering, this black box (hash function), doesn't it slow things down? because every time we want to add a property and the value to a hash table we have to run it through tha hash function so we can decide where to put it in memory
