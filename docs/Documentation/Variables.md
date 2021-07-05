---
layout: default
title: Variables
nav_order: 7
parent: Documentation
---

<a style="float: left;" href="https://skiylia-lang.github.io/docs/Documentation/ControlFlow.html">← Control Flow</a>
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

# Variables

Variables are named objects that can store any value (including function and class references!). A variable can be defined two separate ways in Skiylia, implicitly and explicitly.

#### Explicit

Variables declared with the `var` keyword are explicit variables, the Skiylia interpreter immediately knows that a new variable needs to be defined. Variable names follow the `var` keyword, and their initial value must be set following an `=` symbol:

```
var a = 10
```

Additionally, empty variables, whose value is `0` by default, can be created by just calling the `var` keyword on a variable name.

```
var b
```

Calling `var` with a variable that has already been defined will throw an error:

```
var a = 10

var a = 6

/// This will output:
    [Line 3, Char 5] Syntax Error: Variable with this name already in scope. ///
```

#### Implicit

Variables can also be declared implicitly, without the use of the `var` keyword.

```
a = 10
```

Unlike explicit variables, implicit ones must always be given an initial value.

```
b

\\ This will obviously raise an error
```
```
b = 0

\\ This is the correct way to zero-declare
```

There is one exception to the above rule: the increment variable in a for loop. If this variable is defined in a loop, it will be set to 0 even if no value was given:

```
for x where x<=10:
  print(x)

/// This will output:
    0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
    Even though 'x' did not have an explicit 'var' declaration, or an explicit value declaration ///
```

As Skiylia is based on Python, it may seem strange to keep explicit variable declaration. As the `var` keyword can only be used when a variable is first defined, this can help with readability, so will be retained (until further notice)

# Scope

Skiylia variables obey scoping rules; A variable exists, and is accessible, only from where it is defined, until the end of the code block it was defined in.

```
def hello():
  a = 10
  print(a)

print(a)
hello()
print(a)
```

`a` has not yet been defined for the first `print`, so this will raise an error.
The second `print` in the function will work perfectly fine.
The final `print`, while following `a` being defined, is outside of the local scope; `a` exists only within the `hello()` function

Variables defined at the top level of a script are considered global, though more succinctly their local block is the zeroth block: the program itself. Variables defined here are accessible to all parts of the script, but are not visible to any scripts that import this script.

It is possible to define a variable inside a block, whose parent block also contains the same variable name. This technique is known as shadowing:

```
def hello():
  a = "hi"

  def no():
    a = "nope"
    print(a)

  print(a)

/// This will output:
    nope
    hi ///
```

As discussed above, explicitly declaring a variable in the same scope will throw an error, while implicit declaration will overwrite its value

```
var a = "hi"
var a = "hello"
/// This will output:
    [Line 2, Char 5] Syntax Error: Variable with this name already in scope. ///
```

# Assignment

After a variable has been declared, a new value can be assigned to it with implicit declaration:

```
var a = 10
a = 34
```

If the left hand side contains more than a variable name, this is considered a [setter](https://skiylia-lang.github.io/docs/Documentation/Methods.html#getters-and-setters), rather than assignment.

<a style="float: left;" href="https://skiylia-lang.github.io/docs/Documentation/ControlFlow.html">← Control Flow</a>
<div style="float:clear"></div>
<br>
<br>
