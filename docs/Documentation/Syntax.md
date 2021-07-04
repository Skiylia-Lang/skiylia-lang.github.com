---
layout: default
title: Syntax
nav_order: 2
parent: Documentation
---

<a style="float: left;" href="https://skiylia-lang.github.io/docs/Documentation/Documentation.html">← Documentation</a>
<a style="float: right;" href="https://skiylia-lang.github.io/docs/Documentation/Data_Types.html">Data Types →</a>
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

# Syntax

# Comments

Comments in Skiylia come in two flavours: line, and block.

Line comments begin with `//` and terminate at the end of the line.

```
// This is a single line comment.
```

Block (or multi-line) comments both start and end with `///`. They can span multiple lines, and even include single line comments without issue.

```
/// This is a comment
    that spans multiple lines.
    It is particularly helpful for longer explanations. ///
```

#### Comment style

Skiylia style strongly prefers all comments to end with a period, and all block comments to be aligned with leading whitespace.

```
print(1) // prints '1' to the screen.
print(5 + 34) //addition of two integers
///the expected output is
39///
```
```
// prints '1' to the screen.
print(1)

//addition of two integers.
print(5 + 34)

/// The expected output is:
    39. ///
```

The former is a perfectly valid Skiylia script, but is discouraged  due to readability.

# Keywords

Skiylia has a total of 27 reserved keywords that cannot be used for variable, function, or class names.

```
and break check continue class def do elif else
false for if import in not null or return self
super true until var when where while xor
```

Additionally, Skiylia reserves 22 keywords as the names of primitive functions.

```
abs array bool ceil clock elapsed float floor
input int integer mod pow print readfile round
sum sqrt str string wait writefile
```

All keywords are case sensitive, so while it is discouraged, a user could feasibly have a variable named `False` without conflicting with the `false` keyword.

# Script Structure

### Newlines

Newlines (`\n`) are significant in Skiylia, as they separate statements. This is in contrast to C-like languages, which use the semi-colon (`;`).

```
print("Hello") print("World!")
```

This is not a valid way of writing multiple statements, as whitespace is removed by the Skiylia Lexer.

```
print("Hello")
print("World")
```

Instead, the two `print` statements should be written as in the above.

Strings can also be divided by newlines without causing an error. This preserves the newline if said string is also printed.

```
/// An example of how strings can contain newlines.
    Of course, this may cause unexpected outcomes. ///

var a = "This is a string
         It is separated across multiple lines
           This indentation will be preserved.
         But anything else will not."

print(a)

/// Expected output:
    This is a string
    It is separated across multiple lines
     This indentation will be preserved.
    But anything else will not. ///

```

### Blocks

Much like Python, Skiylia code uses indentation to define blocks. Blocks follow all statements which end in colons (`:`), like function declarations or control flow statements.

A new block is created where the indentation level of a chunk of code increases, and ends when new code has a lower indentation.

```
/// If statements are an example of colon-terminated statements,
    hence a new block is required. ///

if a == 5:
  print("'a' was in fact equal to 5!")
```

Blocks define where variables can be accessed. Local variables are accessible in the same block they were defined in, and any block contained within it. Global variables are accessible from any part of the script, as they are defined in the 'zeroth' block.

#### Indentation rules

Indentation *must* increase following any statements that end in a colon.

```
def testFunction(a):
  if a == "test":
  print("'a' was equal to 'test'")
  return true
  print("'a' not was equal to 'test'")
```
In this example, the `print` statement is not indented relative to the conditional before it. This will cause an indentation error.

The keywords `break`, `continue`, and `return` act as block terminators, where indentation *must* decrease following them.

```
def testFunction(a):
  if a == "test":
    print("'a' was equal to 'test'")
    return true
    print("'a' not was equal to 'test'")

```
The final `print` function is at the same indentation level as the preceding `return` statement, and will cause an indentation error. Additionally, as the function is terminated after a `return`, the `print` will never be executed.

Conditionals, control-flow structures, function definitions, and class definitions (The group of which is imaginatively named 'Colon-terminated statements') are the only objects in Skiylia where a colon is permitted.

```
def testFunction(a):
  if a == "test":
    print("'a' was equal to 'test'"):
      return true
  print("'a' was not equal to 'test'")
```

The `print` statement is not a colon-terminated statement, and thus cannot precede a colon (`:`).

```
def testFunction(a):
  if a == "test":
    print("'a' was equal to 'test'"):
    return true
  print("'a' was not equal to 'test'")
```

The above is an example of the three rules above working in unison.

#### Exceptions to the rules

As with most languages, there are some exceptions to the rules. In Skiylia, this is the case where a colon-terminated statement is followed by a single expression.

Due to the colon acting as an implicit indentation marker, an expression can be written on the same line without throwing an Indentation error.

```
if a == true: print("'a' was true!")
else: print("'a' was false!")
```

Due to the colon acting as an implicit indentation marker, it is feasible for the user to mix implicit and explicit indentation without the interpreter throwing an err0r.

```
if a == true: print("'a' was true!")
  print("The raw value of 'a' was", a)
else: print("'a' was false!")
```

Skiylia style strongly discourages this type of code, as it decreases readability. Instead, whenever explicit indentation is included in a block, all other indentation should also be explicit, as shown below.

```
if a == true:
  print("'a' was true!")
  print("The raw value of 'a' was", a)
else:
  print("'a' was false!")
```

# Precedence

The following table describes the precedence structure of Skiylia, which is similar to almost all programming languages. Higher precedence operations are executed before those with lower precedence, ie: `a * (b + c)` will evaluate `(b + c)` first.

| Prec. | Operator | Description |
|:------|:---------|:------------|
| 1 | `()` `.` | Grouping, Method call |
| 2 | `-` `!` `--` `++` | Negate, Not, Decrement, Increment |
| 3 | `*` `/` `**` | Multiply, Divide, Exponentiate |
| 4 | `+` `-` | Add, Subtract |
| 5 | `>` `>=` `<` `<=` | Comparison |
| 6 | `==` `===` `~~~` `!=` `!==` `!~~~` | Equality and Inequality |
| 7 | `and` `&` | Logical and |
| 8 | `or` `\|` | Logical or |
| 9 | `xor` `^` | Logical xor |
| 10 | `? :` `?:` `??` | Conditionals |
| 11 | `=` | Assignment |

<a style="float: left;" href="https://skiylia-lang.github.io/docs/Documentation/Documentation.html">← Documentation</a>
<a style="float: right;" href="https://skiylia-lang.github.io/docs/Documentation/Data_Types.html">Data Types →</a>
<div style="float:clear"></div>
<br>
<br>
