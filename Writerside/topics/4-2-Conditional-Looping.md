# 4.2. Conditional Looping

Conditional looping is done with the `loop` expression. There is no `for` loop in S++; instead, interior iteration is
done with the streaming API, using generators. The `loop` expression is modelled as an expression, but cannot be used
as the rhs of an assignment, because the inferred type is `Void`, which a variable cannot hold.

## Condition
The condition of a `loop` block must evaluate to a `Bool` value, so the compiler knows whether to continue looping or
not. The condition is evaluated before each iteration of the loop. The condition is **required**.

## Else
If the condition of a `loop` block is false before the first iteration, the `else` block, if provided, is executed.
This allows for cleaner code:

#### Without `while-else` block:
```s++
case condition == then
    true {
        loop condition { ... }
    }
else { ... }
```

#### With `while-else` block:
```s++
loop condition { ... }
else { ... }
```

## Control flow
There is no `break` or `continue` statement, because these disrupt the flow of the program.
