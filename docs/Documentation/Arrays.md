---
layout: default
title: Arrays
nav_order: 4
parent: Documentation
---

<a style="float: left;" href="https://skiylia-lang.github.io/docs/Documentation/Data_Types.html">← Data Types</a>
<div style="float:clear"></div>
<br>
<br>

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

# Arrays

An array in Skiylia is a compound data type that contains a collection of any other data type. Arrays are created by calling the `array` function.

```
// An empty array.
var a = array()

// An array that contains the fibonacci numbers.
var b = array(1, 1, 2, 3, 5, 8)
```

This is equivalent to `list()` in Python.

# Fetching elements

You can fetch the element of an array by calling the `get()` operator on it. Array indices count upwards from zero.

```
var a = array(1, 1, 2, 3, 5, 8)

print(a.get(4))
/// Expected output:
    5. ///
```

Additionally, negative indices will count backwards from the end of an array.

```
var a = array(1, 1, 2, 3, 5, 8)

print(a.get(-1))
/// Expected output:
    8. ///
```

An Error will be returned if trying to access indices outside the length of the array.

```
var a = array(1, 1, 2, 3, 5, 8)

print(a.get(10))
/// Expected output:
    [Line 3, Char 9] Runtime Error: Invalid index '10' for array. ///
```

# Changing elements

You can overwrite the value of an element at any index of an array by calling the `set()` operator.

```
var a = array(1, 1, 2, 3, 5, 8)

a.set(3, 10)

print(a)
/// Expected output:
    Array(1, 1, 2, 10, 5, 8). ///
```

# Adding elements

It is possible to grow arrays after they have already been created, by calling either the `add()` or `insert()` functions.

```
var a = array(1, 1, 2, 3, 5, 8)

a.add(13)

print(a)
/// Expected output:
    Array(1, 1, 2, 3, 5, 8, 13). ///

a.insert(3, 13)

print(a)
/// Expected output:
    Array(1, 1, 2, 13, 3, 5, 8, 13). ///
```

`add()` will append the value to the end of the array, while `insert` will insert the value into the array at the specified index.

# Removing elements

It would be rather useless if values could not be removed from arrays as well. The two methods `pop()` and `remove()` function as the reverse of `add()` and `insert()` respectively.

```
var a = array(1, 1, 2, 3, 5, 8)

a.pop()

print(a)
/// Expected output:
    Array(1, 1, 2, 3, 5). ///

a.remove(2)

print(a)
/// Expected output:
    Array(1, 1, 3, 5). ///
```

`pop()` will remove the last value from an array, while `remove()` will remove the value at the specified index.

Additionally, the `pop()` and `remove()` functions return the values that were removed:

```
var a = array(1, 1, 2, 3, 5, 8)

print(a.pop())
/// Expected output:
    8. ///
```

# Array length

It is possible to fetch the length of an array, using `len()`, which can be helpful in comparisons.

```
var a = array(1, 1, 2, 3, 5, 8)

print(a.len())
/// Expected output:
    6. ///
```

`len()` is equivalent to the final index of an array, plus one.

<a style="float: left;" href="https://skiylia-lang.github.io/docs/Documentation/Data_Types.html">← Data Types</a>
<div style="float:clear"></div>
<br>
<br>
