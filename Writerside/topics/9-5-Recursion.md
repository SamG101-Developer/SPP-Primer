# 9.5. Recursion

Recursion is a key concept in functional programming, and is used in S++ to allow functions to call themselves. This is
useful for functions that need to perform the same operation multiple times, such as traversing a tree or calculating a
factorial.

Every recursive function is re-written to be tail-recursive by the preprocessor, meaning that the function is optimized
to use constant stack space. This allows for functions to be called recursively without the risk of a stack overflow,
creating time-limited, rather than space-limited, recursion.

## Tail Call Recursion

Tail call recursion is a form of recursion where the recursive call is the last operation in the function. This allows
the function to be optimized by the compiler to use constant stack space, as the stack frame of the current function can
be reused for the recursive call.
