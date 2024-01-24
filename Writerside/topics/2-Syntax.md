# 2. Syntax
Tokens in S++ are generally used for 1 thing only. Below is a table of non-binary-tokens and their usages. The 
exception is the `&` binary operator as it has another usage.

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
