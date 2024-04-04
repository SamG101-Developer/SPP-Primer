# 11.2. Concurrency &amp; Coroutines

## Coroutines in S++

The concurrency mechanism in S++ is based on coroutines, which are the same as generators, like in Python.
Coroutines are functions that can be suspended and resumed, and in S++ they're formed by any normal function containing
a `gen` expression, used for yielding/generating values.

Coroutines must return one of the `Gen[Mov|Ref|Mut][Yield, Return=Void, Send=Void]` type. This type is a generic type,
with the `Yield` parameter being the type of the values yielded by the coroutine, the `Return` parameter being the type
of the value returned by the coroutine, and the `Send` parameter being the type of the value being sent to the
coroutine.

Coroutines are generators in S++, but are not necessarily asynchronous. See
[asynchronous functions](11-1-Asynchronous-Functions.md) for more information.

## Out

### Yielding from a coroutine

Values can be yielded from a coroutine using the `gen` keyword (generate a value). This looks like `gen 123`,
where `123` is the value being yielded. The type of the value being yielded must match the `Yield` parameter of the
coroutine's return type.

Yielded values can be borrows, because control will always return to the coroutine, guaranteeing that the value will
still be valid.

All yields from a coroutine must follow the same convention (move, reference, or mutable reference), and the convention
is based on the variant of the `Gen` type being used. For example, if `GenRef` is being used, then all yields must use
the `&` immutable borrow convention. This is similar to the `Fun[Mov|Ref|Mut]` function types whose variant depicts the
convention of the environment capture.

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
name of the variable being assigned to, and it's type will be the type of the `Send` parameter of the coroutine's return
type.

## Chaining coroutines

Coroutines can be chained with the `gen with` expression, allowing to yield everything out of a coroutine into and
out of the next coroutine. This is identical to the semantics of the `yield from` statement in Python.
