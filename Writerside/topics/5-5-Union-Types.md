# 5.5. Union Types

Union types are types that can be any 1 of a set of types. The `Var[..Ts]` type is used, `..Ts` being the tuple of
allowed typed under this union type. The shorthand for union types uses teh `|` operator, for
example `function(p: U32 | Str) -> Void { }` is a function that takes either a `U32` or a `Str` as a parameter..

Pattern matching using the `is` keyword is used to determine which type is being used. This is done by using the `is`
keyword, followed by the type to check for. If the type matches, the block is executed. If the type does not match, the
next `is` block is checked. If no `is` block matches, the `else` block is executed. It is enforced that either every
type is considered on a separate branch, or that the `else` block is provided.