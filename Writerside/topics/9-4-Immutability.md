# 9.4. Immutability

Immutability is a key concept in functional programming, and is used in S++ to prevent side effects and make code easier
to reason about. In S++, all variables are immutable by default, meaning that once a variable has been assigned a value,
it cannot be changed. This is in contrast to languages like C or C++, where variables are mutable by default.

Variables and parameters can be made mutable by using the `mut` keyword. This allows for variables to be changed after
they have been assigned a value. Mutable variables are useful for when variable's values need to be changed, but should
be used sparingly, as they can introduce side effects and make code harder to reason about.

For variable destructuring, the `mut` keyword must be used on each part of the destructuring, as the destructuring is
treated as a separate assignment for each part. This means that to destructure a tuple into mutable variables, the `mut`
keyword must be used on each part of the tuple. For example, `let (mut a, b) = (1, 2)` would make `a` mutable, but `b`
immutable.

Immutability is enforced at compile time, meaning that the compiler will catch any attempts to change an immutable
variable. This allows for more robust code, as it prevents bugs that can be caused by changing variables in unexpected
ways.

## Interior Mutability

A borrowed value can be borrowed mutably or immutably, but this is separate from the mutability of the value itself.
This means a mutable borrow may be non-reassignable, or an immutable borrow may be re-assignable. This is an important
distinction, as it allows for finer-grained control over the mutability of values.

There is no internal mutability for owned values, because if a mutable non-assignable variable could have every
attribute mutated, the variable is mutable, it just means re-assigning to it is a longer process. An immutable but
re-assignable variable is a mutable variable, because attributes could be mutated by replacing the object with another
object where some attributes are the same and some are different.
