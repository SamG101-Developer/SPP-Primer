# 5.5. Union Types

Union types are types that can be any 1 of a set of types. The `Var[..Ts]` type is used, `..Ts` being the tuple of
allowed typed under this union type. The shorthand for union types uses teh `|` operator, for
example, `function(p: U32 | Str) -> Void { }` is a function that takes either a `U32` or a `Str` as a parameter.

Pattern matching using the `is` keyword is used to determine which type is being used. This is done by using the `is`
keyword, followed by the type to check for. If the type matches, the block is executed. If the type does not match, the
next `is` block is checked. If no `is` block matches, the `else` block is executed. It is enforced that either every
type is considered on a separate branch, or that the `else` block is provided.

A common example of union types are:

- The `Opt[T]` type, which is a `Var[T, None]`, with methods superimposed on it.
- The `Ret[Pass, Fail]` type, which is a `Var[Pass, Fail]`, with methods superimposed on it.

```
let val = function_returning_optional()  # Returns an Opt[Bool]
case val then
    is Bool { std.print("Value is ", val) }
    is None { std.print("No value") }
    
let val = function_returning_result()  # Returns a Ret[Str, Err]
case val then
    is Str { std.print("Pass: ", val) }
    is Err { std.print("Fail: ", val) }
```

## Flow typing

As seen in the above examples, when the `is` keyword is used in a `case` pattern branch, the type of the variable being
inspected is treated as the type being checked against. This is called flow typing, and is used to reduce the amount of
casting that is required in the code.

Only types that form the union can be in the pattern match (enforced at compile time), and if not every type is listed
in the pattern match, then the `else` block must be provided.
