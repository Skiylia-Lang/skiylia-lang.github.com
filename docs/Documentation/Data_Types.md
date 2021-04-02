---
layout: default
title: Data Types
nav_order: 3
parent: Documentation
---

<a style="float: left;" href="https://skiylia-lang.github.io/docs/Documentation/Syntax.html">← Syntax</a>
<div style="float:clear"></div>

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

# Data Types

# Booleans

Booleans represent truthiness in Skiylia. There are only two boolean literals, `true` and `false`.

They are returned when evaluating the truthiness of an expression `a == b` or by directly fetching the boolean representation of an object `bool(a)`.

# Numbers

## Float

All numbers in Skiylia are stored internally as a floating point value, a similarity shared by most all languages. Floats can be accessed by passing any number with a non-zero decimal component `0.91`, or by directly calling the float representation of an object `float(1.4)`

## Integers

Integers are the subset of `float` that do not contain a decimal component `14`. When representing values in code, the Skiylia interpreter automatically converts any floats to integers where possible.

Floats can be explicitly converted to integers by calling several methods: `int()` (or `integer()`), `round()`, `ceil()`, and `floor()`.
```
integer(3.9415)       // 3
int(3.9415)           // 3
round(3.9415)         // 4
ceil(3.9415)          // 4
floor(3.9415)         // 3
```

# Strings

Strings are natively stored in UTF-8 Encoding in Skiylia, though any value can be stored. All string literals are enclosed with `" "` double-quote marks. Additionally, a string can be constructed by directly calling the `str()` (or `string()`) function.

When calling comparisons, the Skiylia interpreter automatically converts any string objects to floats (or integers) where possible.

# Null

Skiylia has a single none-type, `null`. This is automatically returned where a method does not return anything, and will always equate to false in a boolean operation, unless directly compared with another `null`.

<a style="float: left;" href="https://skiylia-lang.github.io/docs/Documentation/Syntax.html">← Syntax</a>
<div style="float:clear"></div>
