# 11.2. Concurrency &amp; Coroutines

## Coroutines in S++

Coroutines are the concurrency mechanism in S++. They allow the function to be suspended and resumed, and are formed by
any normal function containing a `gen` expression, used for yielding/generating values. When suspending, the coroutine
can yield, or "generate" a value, and when resuming, the coroutine can receive a value.

This allows for information to be passed back and forth between the caller and the coroutine. Because the coroutine is
always guaranteed to be resumed, coroutines are allowed to yield borrowed values, because their owned object is
guaranteed to outlive the borrow; the control will return to the coroutine, where the borrow's owned value exists.

Coroutines must return either `GenMov`, `GenRef`, or `GenMut` types, depending on the convention of the yields. All
yields must follow the same convention, and the convention is based on the variant of the `Gen` type being used. For
example, if `gen &1` is an expression found in the coroutine, then the return type must be `GenRef[Yield=BigNum]`.

A coroutine is not necessarily asynchronous. See [asynchronous functions](11-1-Asynchronous-Functions.md) for more
information.

## Out

### Yielding from a coroutine

Values can be yielded from a coroutine using the `gen` keyword (generate a value). This looks like `gen 123`,
where `123` is the value being yielded. The type of the value being yielded must match the `Yield` generic argument of
the coroutine's return type.

The `Yield` generic parameter cannot receive a `Void` type, because the caller may be storing the result of the `gen`
expression, and as a `Void` type cannot be stored, it cannot be yielded.

#### Generator types:

| Type                          | Convention        | Description                                  |
|-------------------------------|-------------------|----------------------------------------------|
| `GenMov[Yield, Return, Send]` | Move              | Moves the value out of the coroutine         |
| `GenRef[Yield, Return, Send]` | Reference         | Borrows the value from the coroutine         |
| `GenMut[Yield, Return, Send]` | Mutable Reference | Borrows the value mutably from the coroutine |

### Returning from a coroutine

Coroutines can return a value using the `ret` keyword. This will prevent the `.next()` method from being called from
the generator. The type of the value being returned must match the `Return` parameter of the coroutine's return type.

## In

### Sending a value into a coroutine

Values can be sent into a coroutine in the `.next()` method. If the `Send` type isn't `Void`, then an argument can
be passed to the `.next()` method. It is received in the coroutine using the `let x = gen 123` syntax, where `x` is the
name of the variable being assigned to, and its type will be the type of the `Send` parameter of the coroutine's return
type.

Sent values must be owned objects, because the coroutine may be suspended, and the value must be stored in the coroutine
until it is resumed. If the value is borrowed, then the value may be dropped before the coroutine is resumed, causing
undefined behaviour.

## Chaining coroutines

Coroutines can be chained with the `gen with` expression, allowing to yield everything out of a coroutine into and
out of the next coroutine. This is identical to the semantics of the `yield from` statement in Python.

### Chaining example

```
fun foo() -> GenMov[BigNum] {
    gen 1
    gen 2
    gen 3
}

fun bar() -> GenMov[BigNum] {
    gen 4
    gen 5
    gen 6
}

fun baz() -> GenMov[BigNum] {
    gen with foo()
    gen with bar()
}
```
