# 7.2. Ownership
In S++, ownership is an important feature of memory management, and is used to ensure that uninitialized memory is 
never used, and that memory is always freed when it is no longer needed. This is done by having a unique owner of a
value.

When a variable is defined with a value, ie `let x = 5`, `x` is "owned", because it has a value. If a function call 
moves `x`, then `x` is now uninitialized, and cannot be used. This is because the value has been moved to the function
call. This is seen in Rust too.

## Move vs. Copy
By default, variables are moved into functions when no convention is given to the argument. To instead allow a type 
to always be _copied_, the `Copy` class must be superimposed onto the type. This is inspired by Rust's `Copy` trait. 
The `Copy` class has a single method, `copy`, which returns a copy of the value.
