---
layout: default
title: Functions
nav_order: 5
parent: Documentation
---

<a style="float: left;" href="https://skiylia-lang.github.io/docs/Documentation/Arrays.html">← Arrays</a>
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

# Methods

Skiylia is an object oriented language, so any given script will spend a not insignificant amount of time using method calls

```
array.add("hello")
```

In this case, we have the callee `array`, followed by the method operator `.`, then the method `add()`, and finally it's arguments `"hello"`.

As with the inspiration for Skiylia, Python, multiple method arguments are comma separated. additionally, if the method allows it, the argument list can be empty:

```
array.join(1, 2, 3)

class.test()
```

# Getters and Setters

Methods need not have to be functions of the callee object, and can take the form of variables. These properties are referenced almost identical to method calls, though do not take parentheses

```
class.name

/// This will fetch the variable 'name' found within the
    Object `class`, much the same as any other variable. ///
```

As with variables, these exposed properties can also be overwritten, using identical syntax no less.

```
class.name = "Testing"
```

<a style="float: left;" href="https://skiylia-lang.github.io/docs/Documentation/Arrays.html">← Arrays</a>
<div style="float:clear"></div>
<br>
<br>
