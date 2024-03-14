# 11. Async, Concurrency & Parallelism

Asynchronous coding, concurrency, and parallelism are 3 different concepts that have clear distinctions in S++:

- Asynchronous coding: a function calling convention that allows the caller to continue execution while the callee is
  still running. This is done applying the `async` keyword as a unary operator for the function call. Using the `async`
  keyword wraps the return type in a `Fut` type.
- Concurrency: yielding from coroutines, which are functions that can be suspended and resumed. This is done using
  the `gen` keyword to generate values out of a coroutine. Any function with a `gen` expression inside is a coroutine,
  and must return a `Gen[Mov|Ref|Mut]` type.
- Parallelism: running multiple tasks at the same time, which is done using the `Thread` class and its associated
  primitives.
