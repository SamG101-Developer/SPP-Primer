# 2.1. Comments

Comments in S++ are inspired by Python rather than C++ and Rust. There are two different types of comments: single-line
comments and multi-line comments. Comments are ignored by the compiler, and are removed in
the [lexical analysis phase](14-1-Compilation-Pipeline.md#lexical-analysis) of compilation.

## Comment Syntax

| Comment type | Syntax          |
|--------------|-----------------|
| Single-line  | `# comment`     |
| Multi-line   | `## comment ##` |

## Single-line Comments

Single-line comments are used to comment out a single line of code. They are denoted by a `#` character, followed by the
comment text. Single-line comments can be placed at the end of a line of code, or on a line by themselves. Any unicode
character can be used in a single-line comment.

```
let x = 5 # This is a single-line comment
```

## Multi-line Comments

Multi-line comments are used to comment out multiple lines of code. They are denoted by a `##` character at the start of
the comment, and a `##` character at the end of the comment. Multi-line comments can span multiple lines, and can be
nested. Any unicode character can be used in a multi-line comment.

```
##
This is a multi-line comment
It can span multiple lines
##
```
