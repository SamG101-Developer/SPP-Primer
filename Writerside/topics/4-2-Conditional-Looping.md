# 4.2. Conditional Looping

S++ uses the `loop` expression to perform conditional looping. A `loop` expression mirrors the behaviour of a
typical `while` statement in almost every other language. The `loop` keyword was chosen for readability, maintaining the
4-character keyword length of other block-based keywords.

An expression must always follow the `loop` keyword, which is the condition that is checked before each iteration of the
loop. If the condition is false, the loop is exited. If the condition is true, the loop is executed. There is no
unconditional looping structure in S++, because whilst `loop true` can be used, it is not recommended, as it is easy to
accidentally create an infinite loop.

The `loop` expression is modelled as an expression, but it can never be the RHS of an assignment, because `loop`
expressions don't every return a value, like a `case` expression can.

There are no looping management keywords, like the typical `break` and `continue` keywords, because these disrupt the
flow of the program. Instead, the condition of the loop should be used to control the flow of the program. This enforces
the left-to-right, top-to-bottom flow of code blocks, which is easier to read and understand.


The condition of a `loop` block must evaluate to a `Bool` value, so the compiler knows whether to continue looping or
not. The condition is evaluated before each iteration of the loop.

## Else

If the condition of a `loop` block is false before the first iteration, the `else` block, if provided, is executed.
This allows for cleaner code:

#### Without `while-else` block:

```
case condition == then
    true {
        loop condition { ... }
    }
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