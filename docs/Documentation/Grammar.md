---
layout: default
title: Grammar
nav_order: 40
parent: Documentation
---

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

# Grammar

The complete grammar for Skiylia, as it currently stands, is listed below.

This page makes use of a slightly modified version of [Backus-Naur](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form) notation.

# Notation

A Greater than `>` defines the left hand side in terms of the right.

A Bar `|` allows a choice between any number of separated values.

A Parenthesis `()` implies a grouping of some number of objects.

A Double quote `" "` enclosing a object shows that that value must appear exactly.

An Asterisk `*` attached to an object shows that it appears zero or more times.

A Plus `+` attached to an object shows that it appears one or more times.

A Question mark `?` attatched to an object shows that it appears one or less times.

# Syntax Grammar

Syntax grammar describes how tokens are parsed into the internal representation of Skiylia (be it abstract syntax tree, or byte-code).

The first rule matches the entirety of a Skiylia script (or the command line REPL).
```
program             > declaration* EOF
```

### Declaration

A program is a series of declarations, each of which are themselves statements.

```
declaration         > importDeclaration
                    | classDeclaration
                    | functionDeclaration
                    | variableDeclaration
                    | statement

importDeclaration   > "import" Identifier

classDeclaration    > "class" Identifier ( "(" Identifier ")" )?
                      ":" "\n" function*

functionDeclaration > "def" function

variableDeclaration > "var" Identifier ( "=" expression )?
```

To keep the syntax cleaner, the function grammar has been pulled out here.  

```
function            > Identifier "(" paramters? ")" ":" "\n" block

paramters           > Identifier ( "," Identifier )*
```

### Statement

Statements do not introduce bindings (objects that the interpreter needs to track).

```
statement           > checkStatement
                    | doStatement
                    | exprStatement
                    | forStatement
                    | ifStatement
                    | interuptStatement
                    | untilStatement
                    | whileStatement
                    | block

checkStatement      > "check" expression ("," expression)?

doStatement         > "do" (whileStatement | untilStatement)

exprStatement       > expression "\n"

forStatement        > "for" ( variableDeclaration | exprStatement )
                             forcondition? ":" "\n" statement

forcondition        > ( "when" expression )? ( "do" expression )?
                    | "in" Identifier

ifStatement         > "if" expression ":" "\n"? statement
                        ( "elif" expression ":" "\n"? statement)*
                        ( "else" ":" "\n"? statement )?

interuptStatement   > "break"
                      | "continue"
                      | "return" expression?

untilStatement      > "until" expression ":" "\n" statement

whileStatement      > "while" expression ":" "\n" statement

block               > ( declaration "\n" )+

```

Note: the block requires indentation to increase before, and decrease after, itself.

### Expressions

```
expression          > assignment

assignment          > ( call "." )? Identifier "=" assignment
                    | conditional

conditional         > logicalor ( ( ( "?" expression ":" )
                                    | "?:" | "??" ) conditional )?
```

### Binary operations

Binary operations are those that take two values. (not neccesarily those that require binary numbers, like `0b101`)

```
logicalor           > logicalxor ( ( "|" | "or" ) logicalxor )*

logicalxor          > logicaland ( ( "^" | "xor" ) logicaland )*

logicaland          > equality ( ( "&" | "and" ) equality )*

equality            > comparison ( ( "==" | "!=" | "===" | "!=="
                                    | "~~~" | "!~~" ) comparison )*

comparison          > term ( ( ">" | ">=" | "<" | "<=" | "<=>" ) term )*

term                > factor ( ( "-" | "+" ) factor )*

factor              > unary ( ( "*" | "/" | "**" ) unary )*
```

### Unary operations

Operations that require only a single operand

```
unary               > ( "!" | "-" )* unary
                    | ( "++" | "--" )? call
                    | postfix

postfix             > call ( "--" | "++" )?
```

### Literals

These are the final parts of the script that actually encode values like `6` or `Hello World!`

```
call                > literal ( "(" arguments ")" )*
                    | literal ( "." Identifier )*

arguments           > expression ( "," expression )*

literal             > Number
                    | String
                    | "self"
                    | "super" "." Identifier
                    | "(" expression ")"
                    | true
                    | false
                    | null
                    | Identifier
```

# Lexical Grammar

Lexical grammar describes how characters are parsed into tokens such that the syntax grammar can be used.

```
Number              > Digit+ ( "." Digit+ )?

String              > {"} {any character}* {"}

Identifier          > Alpha AlphaNumeric*

AlphaNumeric        > Alpha | Digit

Alpha               > "a" | "b" ... "z"
                    | "A" | "B" ... "Z"
                    | "_"

Digit               > "0" | "1" ... "9"
```

Strings must begin and end with `"`, but it is quite hard to represent that within our Backus-Naur rules.
