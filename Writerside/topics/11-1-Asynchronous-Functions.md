# 11.1. Asynchronous Functions

S++ uses a similar way to achieve asynchronous code to `Go`. It uses an `async` keyword, but at the function call
site, not the function declaration. This means that functions don't have to have 2 separate implementations for
synchronous and asynchronous code, avoiding the "function colour" problem.

When a function is called asynchronously, a `Fut[T]` type wraps the return type of the function, and is returned
immediately, whilst the internal value is computed in the background. This means that the function call is
non-blocking, and the value can be retrieved later.

## The `Fut[T]` type

The future type `Fut[T]` has a `.await()` method on it, so that if required, the future can be blocked until its
internal value has been resolved.
