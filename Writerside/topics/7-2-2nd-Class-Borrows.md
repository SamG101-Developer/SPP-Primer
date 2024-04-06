# 7.2. 2nd Class Borrows

S++ uses second-class borrows to ensure that all borrows are always valid, without the need for complex lifetime
analysis.

This works by only allowing borrows to be taken at 2 places:

- Function call sites: `f(&x, &mut y)`
- Yielding out of a coroutine: `gen &x`

Taking a borrow at a function call site will always be safe, because the lifetime of the borrow will always be less than
the lifetime of the owned object, as inner frames have smaller lifetimes than outer frames. This means that for the
duration that the borrow is active, the owned object will always exist, ensuring that the borrow is never invalidated.
Borrows for function arguments are stored on the stack because their lifetime will never extend the frame they're
created in.

Taking a borrow at a yield expression from a coroutine will always be safe, because control is guaranteed to return to
the coroutine scope when the coroutine is used again. When control is passed back to the coroutine, the borrow is
destroyed, ensuring that the lifetime of the borrow is never extended past the scope it originated from. For every
coroutine that could be called in a function, the function's stack frame is extended by a byte. This is to store the
borrows created in the coroutine (each iteration just replaces the borrow with a new one, so the stack frame size is
constant).

## Creating a borrow

Like in Rust, borrows are created using the `&` operator. This will create an immutable borrow of the value on the rhs,
and will be valid until the end of the current scope, or until the borrow is consumed as an argument to a function.
To create a _mutable_ borrow, the `&mut` operator is used. For conflicting borrows, see
the [law of exclusivity](7-3-The-Law-of-Exclusivity).

## Stacking borrows

Borrows can be stacked, but they are automatically reduced to a single borrow type. Taking a borrow of a borrowed value
still only creates the type `&T`, not `&&T`, but it allows the original borrow to not be moved, ie it increases the
number of active borrows. This is fine as it is still in an inner scope to the owned object, meaning that all the
borrows will be destroyed when the scope ends, and before the owned object is destroyed.

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
