# 7.3. 2nd Class Borrows

S++ uses 2nd class borrows to ensure that all borrows are always valid, without the need for complex lifetime
analysis.

This works by only allowing borrows to be taken at function call sites (because control will return to the caller
function's scope), and from yielding values out of a coroutine (because control will always return to the
coroutine's scope, when the coroutine resumes execution).

Because borrows can only be taken at a point where an inner scope is created (in terms of stack frames), all borrows
are stored on the stack, avoiding the heap completely. This allows for faster access and automatic destruction of the
borrows once the stack frame is popped.

## Creating a borrow

Like in Rust, borrows are created using the `&` operator. This will create an immutable borrow of the value on the rhs,
and will be valid until the end of the current scope, or until the borrow is consumed as an argument to a function.
To create a _mutable_ borrow, the `&mut` operator is used. For conflicting borrows, see
the [law of exclusivity](7-4-The-Law-of-Exclusivity.md).

## Lifetime analysis

Because borrows can only be taken at function call sites, and from yielding values out of a coroutine, the lifetime
of a borrow will always be less than the lifetime of the function call site, or coroutine. This means that it is
guaranteed for a borrow to always be valid, without the need for complex lifetime analysis.

## Mutability of borrows vs. values

A parameter, for example, can be marked at `mut`. However, this does not affect the interior mutability of the
borrow it could be receiving. For example, `fun func(mut x: &Str) -> Void` means that `x` cannot be mutated in place,
ie `FunMut` methods cannot be called on `x`, but the value of `x` can be reassigned, ie `x = some_other_str_borrow` is
valid.

| Declaration of Borrow | Description                                   |
|-----------------------|-----------------------------------------------|
| `x: &T`               | Immutable borrow of `x`, cannot be reassigned |
| `x: &mut T`           | Mutable borrow of `x`, cannot be reassigned   |
| `mut x: &T`           | Immutable borrow of `x`, can be reassigned    |
| `mut x: &mut T`       | Mutable borrow of `x`, can be reassigned      |
