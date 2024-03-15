# 7.2 Ownership

In S++, "ownership tracking" is a core feature of memory management. It ensures that only fully initialized objects are
used, mitigating common memory errors on C++ such as "double free" and "use after free". Objects that are uninitialized,
or partly-initialized cannot be moved or borrowed from.

An object that is uninitialized can have a new value set to it, making it fully initialized, or some attributes can be
set, making it partially initialized. An object that is partially initialized can have the rest of its attributes set,
making it fully initialized.

When a variable is defined, for example, `let x = 5`, the variable `x` is initialized. If the value stored by`x` is
moved, for example `f(x)`, then `x` is no longer initialized, is non-owned, and cannot be used. This is because the
value has been moved to the function's parameter identifier. This is similar to Rust's ownership model.

## Partial initialization

Partial initialization is allowed in S++, and is seen when destructuring an owned object. For example, if a point is
defined as `let p = Point(x=0, y=0)` and an attribute is moved, for example `let x = p.x`, then `p` is
partially-initialized, and cannot be used, except to assign attributes or a new value to `p`.

Attributes cannot be moved from a borrowed object because this would make the object partially-initialized, and
invalidate the borrow. Rust has a similar feature, where a borrowed object cannot be moved from.

## Move vs. Copy

By default, variables are moved into functions when no convention is given to the argument. To instead allow a type
to always be _copied_, the `Copy` class must be superimposed onto the type. This is inspired by Rust's `Copy` trait.
The `Copy` class has a single method, `copy`, which returns a copy of the value.
