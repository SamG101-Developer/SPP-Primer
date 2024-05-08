# 11.1. Asynchronous Functions

S++ uses a similar way to achieve asynchronous code to `Go`. It uses an `async` keyword, but at the function call
site, not the function declaration. This means that functions don't have to have 2 separate implementations for
synchronous and asynchronous code, avoiding the "function colour" problem.

When a function is called asynchronously, a `Fut[T]` type wraps the return type of the function, and is returned
immediately, whilst the internal value is computed in the background. This means that the function call is
non-blocking, and the value can be retrieved later.

## The `Fut[T]` type

The future type `Fut[T]` has a `.await()` method on it, so that if required, the future can be blocked until its
internal value has been resolved. In reality, this will probably never be used, because the function can just be called
synchronously to wait for the value.

## Memory safety

The issue with using borrows in `async` functions is that because the next line in the caller function may execute
before the async function call has evaluated, there is no guarantee that the owned value will outlive the borrow. This
is because the owned value may be moved in the caller function whilst the borrow is still active in the async function
call.

For example,

```
fun main() -> Void {
    let x = 1
    async f(&x)
    g(x)
}
```

As the call to `f` is asynchronous, the call to `g` may be executed before the call to `f` has evaluated. This would
cause `x` to be moved, whilst an active borrow to it is still in place in the async function `f`. Alternatively, if `x`
was declared mutably, the value may mutate whilst an immutable borrow is active, violating mutability rules.

Furthermore, the law of exclusivity cannot be enforced, as it would be impossible to know which borrows are active
across multiple async function calls.

This is mitigated by the borrow checker disallowing borrows to be used in async functions, and throwing a compile-time
error if this is attempted.
