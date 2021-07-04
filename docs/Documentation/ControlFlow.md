---
layout: default
title: ControlFlow
nav_order: 6
parent: Documentation
---

<a style="float: left;" href="https://skiylia-lang.github.io/docs/Documentation/Methods.html">← Methods</a>
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

# Control Flow

Control flow defines which blocks of code are executed or evaluated throughout the runtime of a script. The two main types of control flow, branching and looping, respectively decide if a block is executed or not, and how many times it is executed.

# Truthiness

Control flow in any given programming language is dictated by the value of a given expression, more often than not if it evaluates to true.

In Skiylia, the two booleans `true` and `false` dictate truthiness, with certain datatypes having an inherent boolean value:

* the boolean falsehood, `false`, is false (evidently)
* the null operator, `null`, is false
* the number zero, `0`, is false
* empty strings, `""`, are false
* everything else evaluates as true

# If statements

A single if statement is the simplest example of branching conditional flow, and allows a code line to be skipped entirely:

```
if "hello there": print("General Kenobi")
```

In the case where more than one line of code is to be skipped, a full block is used:

```
if "hello there":
  print("General Kenobi")
  print("You are a bold one")
  print("Kill him!")
```

## Else

If an `else` branch is provided, it will be executed if the condition in the corresponding if is false. This can again take a single line, or block, depending on code length:

```
if succeded_jump:
  print("hello there")
else:
  print("ouch")
```

Skiylia style strongly discourages mixing inline and block conditionals, as it decreases readability. Whenever one of the above conditionals takes more than one line, it is recommended so too do all others.

## Elif

If more than one condition is to be tested, then an `elif` statement can be used as part of the control flow. Stacking multiple of these can build up structures similar to (but not equivalent) to the switch/case found in many C derivatives.

```
if jump == "success":
  print("hello there")
elif jump == "near-miss":
  print("ouch")
else:
  print("*splat*")
```

Unlike using multiple if statements, only the first truthy statement in an `if-elif-else` block is executed. In the example above, if `jump` was equal to `"success"`, then the code would run the `print` command, before skipping past the end of the `else` block entirely.

# Logical Operators

Binary Logical operators in Skiylia, unlike method calls, have the ability to short circuit on evaluation. That is to say, if the left hand side of an `and` statement is false, the language does not need to (and will not) evaluate the right hand side.

## Not

The only Unary Logical operator in Skiylia is the `not` operator, which uses both the `not` keyword and the exclamation symbol `!`. As this operation is *right associative*, the operation comes before any operands it acts upon:

```
print( not true )
print( ! true )
```

The truth table for `! A`:

|  A  | Output |
|:---:|:------:|
|True | False  |
|False| True   |

## And

The first of the binary Logical operations is the and operator, accessed in Skiylia both the keyword `and`, and the ampersand symbol `&`.

```
print( true and false )
print( true & false )
```

The logical And will evaluate the expression, if the left side is false, this returns false, else the right hand side is evaluated and returned. This behaviour is easy to understand when showing the truth table for `A & B`:


|  A  |  B  | Output |
|:---:|:---:|:------:|
|True |True | True   |
|True |False| False  |
|False|True | False  |
|False|False| False  |

If `A` is False, so too is the output. If `A` is true, the output is B


## Or

Or operations use the keyword `or` and the pipe symbol `|`. Logical or will evaluate the left hand side, returning true if it is true, else it will return the right hand side.

```
print( true or false )
print( true | false )
```

The truth table for `A | B` is again given below:

|  A  |  B  | Output |
|:---:|:---:|:------:|
|True |True | True   |
|True |False| True   |
|False|True | True   |
|False|False| False  |

## Xor

Exclusive or operations use the keyword `xor` and the caret symbol `^`. The exclusive or is very similar to standard or, though only returning true if one or the other of the inputs is True.

```
print( true xor false )
print( true ^ false )
```

The truth table for `A ^ B`:

|  A  |  B  | Output |
|:---:|:---:|:------:|
|True |True | False  |
|True |False| True   |
|False|True | True   |
|False|False| False  |

## Ternary

The ternary (or conditional) operator in Skiylia is identical to those in C derivatives, making use of the `? :` symbol:

```
print( a ? b : c )
var test = a ? b : c
```

The truth table for `A ? B : C`:

|  A  | Output |
|:---:|:------:|
|True | B  |
|False| C   |

The ternary operator thus functions similarly to an expressive form of the `if-else` statement.

## Elvis

The Elvis operator functions similarly to the conditional ternary, though uses the `?:` symbol. If the left hand is true, it is returned, else the right hand is evaluated and returned:

```
print( a ?: b )
var test = a ?: b
```

The truth table for `A ?: B`:

|  A  | Output |
|:---:|:------:|
|True | A  |
|False| B   |

It should thus be noted that the Elvis operator functions approximately as the ternary operator, though with an implicit truthy return.

## Null-Coalescence

The Null-Coalescence operator makes use of the `??` symbol, and provides another form of value checking. If the left hand is null, the right hand is evaluated and returned, else the left is returned.

```
print( a ?? b )
var test = a ?? b
```

The truth table for `A ?? B`:

|  A  | Output |
|:---:|:------:|
|True | A  |
|False| A  |
|Null | B  |

This is roughly equivalent to the ternary ooperation `A == null ? B : A`. As null evaluates as false in Skiylia, the `A ?: B` and `A ?? B` operations function identically in all cases except where `A` is `false`, `0`, or `""`.

# Looping statements

A useful programming language without the ability to repeat execution of certain code chunks would be relatively useless, and Skiylia is not one of those languages. The individual statements below should be fairly familiar to anyone who has experience in other languages.

## While statement

The simplest looping statement is the `while` loop, which will execute a chunk of code so long as it's condition evaluates as `true`:

```
var n = 0
while n < 10:
  print(n)
  n++

/// This will output:
    0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ///
```

The loop works by evaluating the condition `n < 10`, then executes the loop body if this is true. Following that, it will then re-evaluate the condition, and continue looping until it is `false`.

An infinite loop can be created with `while true:`, as this will always evaluate as true.

Additionally, the `do` modifier can be added to the loop, which executes the body before evaluating the condition. Thus, the loop will always execute at least once:

```
var n = 10:
do while n < 10:
  print(n)
  n++

/// This will output:
    10
    (10 < 10 is false, but do forces the body to execute anyway)///
```

## Until statement

The `until` statement is equivalent to `while`, though continues to execute code while the condition evaluates to `false` instead of `true`.

```
var n = 0
until n == 10:
  print(n)
  n++

/// This will output:
    0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ///
```

An `until x:` loop is thus equivalent to `while not x:`, and is included to increase readability for more complex while statements. Additionally, the `do` keyword can be prefixed to an `until` loop, as with the `while` loop:

```
var n = 10:
do until n > 0:
  print(n)
  n++

/// This will output:
    10
    (10 > 0 is true, but do forces the body to execute anyway)///
```

## For statement

#### Iterable objects

The `while` and `until` statements are useful for indefinite looping, or those with defined conditionals that need to be evaluated after a loop, but in some cases it is more desirable to iterate other a defined collection.

```
var a = array(1, 2, 3, 4, 5, 6, 7, 8)

for x in a:
  print(x)

/// This will output:
    1, 2, 3, 4, 5, 6, 7, 8 ///
```

The increment variable can be defined elsewhere in the scope and used here, or can be defined implictly at the start of a for loop with no issue. In the example above, `x` does not require explicit declaration with the `var` keyword as other variables do, although using one will not throw an error, as shown:

```
var a = array(1, 2, 3, 4, 5, 6, 7, 8)

for var x in a:
  print(x)

/// This will output:
    1, 2, 3, 4, 5, 6, 7, 8 ///
```

As the `for` loop is utilised for implicit iteration, it is often preferred to `while` or `until` in cases where a loop needs to run for a given number of times. There are four distinct allowed Skiylia grammars to aid this:

#### Infinite loops

Only defining the increment variable will create an infinite loop, almost identical to a `while true:` with the added bonus of a counter (in the form of the increment variable of course):

```
for x:
  print(x)

/// This will output:
    0, 1, 2, 3, 4, 5, 6, 7, 8, Ad infinitum ///
```

#### Infinite loops with defined increments

The `do` statement is utilised in for loops, but modifies how the increment variable changes for each loop, rather than forcing the initial execution

```
for x do x+=2:
  print(x)

/// This will output:
    0, 2, 4, 6, 8, 10, 12, 14, 16, Ad infinitum ///
```

#### Defined loop break

In this case, the for statement is again used to create a `while`-like loop with a defined incremental counter. The for loop will continue executing until the statement evaluates to false, which is useful to count up to a certain range.

```
for x when x<=10:

/// This will output:
  0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ///
```

Additionally, the keyword `when` can be substituted for `where` with no issue

#### Defined loop break with defined increments

by using both the loop break and incremental modification, the for loop can count up (or down!) to any value, at any rate:

```
for x when x<10 do x=x+2:

/// This will output:
  0, 2, 4, 6, 8 ///
```

Or perhaps a more complicated set of definitions:

```
for x when x<100 do x*=(x+1):

/// This will output:
  0, 1, 2, 6, 42 ///
```

## Break statement

At times, a programmer can desire a loop to exit prematurely, and in Skiylia this is facilitated with the `break` keyword. It's inclusion causes the immediately enclosed loop to stop.

```
while true:
  var a = input("Do you like Skiylia?\n> ")
  if a == "yes":
    break

/// This will keep asking for an output
    until a user inputs "yes", in which
    case the loop will be stopped ///
```

## Continue statement

Conversely, a programmer may wish to skip part of the iteration, and continue onto the next, without dealing with the remainder of the loop body. This, conveniently, is accessed with the `continue` keyword:

```
for x where x <= 10:
  if x == 5:
    continue
  print(x)

/// This will output:
  0, 1, 2, 3, 4, 6, 7, 8, 9, 10 ///
```

<a style="float: left;" href="https://skiylia-lang.github.io/docs/Documentation/Methods.html">← Methods</a>
<div style="float:clear"></div>
<br>
<br>
