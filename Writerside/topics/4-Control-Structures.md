# 4. Control Structures

## Conditional structures
There are 4 main control structures in S++

| Name   | Description                        |
|--------|------------------------------------|
| `case` | Conditional branching              |
| `loop` | Conditional looping                |
| `with` | Contextual block                   |
| `else` | Else block (for `case` and `loop`) |

## Unconditional structures
There are no unconditional branching (`goto`) or looping (`loop` with no condition) expressions. Unconditional branching
is unstructured, and as there are no `break` or `continue` statements, unconditional looping is useless.

## Expressions
In S++, blocks are treated as _expressions_, not statements. This means that they can be used as function call
arguments, or the rhs of an assignment. This is a powerful feature, and allows for cleaner code. The final statement in
a block is the "returning" value. The exception is the `loop` block, which doesn't return a value, and thus cannot be
used as the rhs of an assignment.
