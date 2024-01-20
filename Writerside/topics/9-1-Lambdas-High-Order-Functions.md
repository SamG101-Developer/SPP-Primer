# 9.1. Lambdas & High Order Functions

## Lambdas
S++ supports lambdas (anonymous functions), using a very similar syntax to normal functions, with 3 changes:
- Lambdas have no name (they are anonymous)
- Lambdas cannot have any annotations
- Lambdas can capture environment variables (making them closures)

#### Lambda syntax example
```s++
fun main() -> Void {
    let x = fun (a: Str, b: Str) -> Str { ret a + b }
    std.assert(x("Hello, ", "World!") == "Hello, World!")
}
```

## Closures
Lambdas become closures when they capture environment variables. In S++, capturing environment variables is explicit, 
unlike Rust. This means each variable, and _how_ its being captured, must be specified. How a variable is captured 
is based on the convention used to capture it, which are the same as
[argument/parameter conventions](3-3-Functions.md#function-parameter-conventions); captures are treated as fixed 
value parameters.

S++ supports normal and named captures, like with [function arguments](3-3-Functions.md#calling-functions). Normal 
captures capture a variable (single identifier), and named captures allow aliasing, which can be useful for class 
variables.

### Closure syntax example
```s++
fun main() -> Void {
    let x = 1
    let y = 2
    
    let z = fun () with [&x, &y] -> Str { ret a + b }
}
```

### Closure function types
Because closures can capture variables from outside their scope, the type inference for a closure is not as simple as
for a normal function. The `Fun[Ref|Mut|Mov]` function types are still used. If there are no captures, then the type 
will be an owned `FunRef`, the same as a normal function.

If there are captures, then type of the function is based on the **most restrictive** capture. Consuming a capture 
is the most restrictive, then mutably borrowing, then immutably borrowing. This means that if a closure captures a 
variable by consuming it, then the type of the closure will be `FunMov`.

If there are captures, then the convention of the type of the function might also be changed on creation. The 
convention is based on the least restrictive capture. Capturing a variable by immutable reference will in turn cause 
the closure to be immutably borrowed, as it must extend to the lifetime of the captured variables.

For example, given the closure `fun () with [x, &y] -> Str { ret a + b }`, the type of the closure will be
`&FunMov[Str, (...)]`, because `x` is captured-by-move (`FunMov`), and `y` is captured-by-reference (`&`).
