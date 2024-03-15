# 2. Syntax

## General

S++ is designed to be syntactically pleasing, going so far as to replace traditional keywords with more modern variants
that allow for more aligned code, whilst still conveying the same meaning. For example, all top level constructs use
three characters: `fun`, `cls`, `sup`, `use`, `let` etc.

## Tokens

S++ was designed where tokens have one major use each, which could be broken down into a few sub-uses. For example,
parentheses are only used for "grouping expressions," but this could be grouping function arguments, parameters, tuple
items or typedef reductions.

Binary operator tokens are unique in their use, with the single exception of the borrow operator `&` and `&mut`, as
these have been carried over from Rust. This makes it clear what operation is occurring without knowing the context of
the code being inspected.

#### Braces

Braces are used for block delimiters. They are used to define the start and end of a block. There are a couple
different types of blocks, such as a function body (block of statements), a class body (block of attributes) and a
sup body (block of sup members). Braces always introduce a new scope, and new scopes can only be introduced with braces.

#### Parentheses

Parentheses are used for grouping expressions. This includes and is limited to: function call arguments, function
parameter lists, tuple elements or types, multiple type reductions, object initialization arguments, and a
parenthesized expression. Parentheses do not introduce a new scope.

#### Brackets

Brackets are used for grouping anything else, and array literals. This includes and is limited to: where clauses in
the where block, generic arguments, generic parameter lists, lambda captures and array literals. Brackets do not
introduce a new scope.
