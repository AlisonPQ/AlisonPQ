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
