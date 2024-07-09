# 4.2. Conditional Looping

S++ uses the `loop` expression to perform conditional looping. A `loop` expression either mirrors the behaviour of a
typical `while` statement, or a `for` statement, depending on the condition. The `loop` keyword was chosen for
readability, maintaining the 4-character keyword length of other block-based keywords.

## For & While

Both the range-based for-loop, and the conditional while-loop, are supported in S++. The `loop` expression is used to
perform both of these operations.

### While

For a conditional loop, synonymous to a standard while-loop, a boolean condition must follow the `loop` keyword. This
condition is checked before each iteration of the loop. If the condition is false, the loop is exited. If the condition
is true, the loop is executed.

```
loop condition { ... }
```

### For

For a range-based loop, the `loop` expression is followed by an iterator expression. This iterator expression contains a
few parts: a local variable identifier, the `in` keyword, and an iterable object. The local variable's type is inferred
from the iterable object, and the local variable is assigned to each element of the iterable object in turn.

The 3 iterator types (`IterMov`, `IterRef`, `IterMut`) are used to determine the type of the local variable. For
example, `loop mut x in vec.iter_ref()` would infer `x` as `&T`, where `T` is the type of the elements in the vector.

## Control Flow

Control flow allows for the `skip` and `exit` statements - these reflect typical `continue` and `break` statements in
other languages. The `skip` statement is used to skip the current iteration of the loop, and the `exit` statement is
used to exit the loop early.

Loops cannot be labelled, but `exit` statements can be stacked to exit multiple loops at once. This is done by using the
`exit` statement multiple times: `exit exit` would break out of 2 loops. Following an `exit` statement, either a `wkip`
statement can be used: exit this loop then skip to the start of the outer loop; or a condition can be used, where the
loop returns a value to a variable, which would've been declared as `let x = while condition { ... }`}

## Else

For conditional loops, an else block can be paired with it: if the condition of a `loop` block is false before the first
iteration, the `else` block, if provided, is executed. This allows for cleaner code:

#### Without `while-else` block:

```
case condition == then
    true { loop condition { ... } }
else { ... }
```

#### With `while-else` block:

```
loop condition { ... }
else { ... }
```

## Future

In the future, the condition of the `loop` expression will be analysed, and determined if the condition is compile-time
evaluable. If this is the case, a warning will be shown, because either the loop will loop forever, or the loop will
never execute. This will help identify potential issues in the code.