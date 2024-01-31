# 7.7. Allocation

Manual allocation is used for the `Arr[T]` type, and types that compose the `Arr[T]` type as an attribute. This is seen
in the `Vec[T]` type. Custom allocators can be used for these types, to allow for custom memory management. All
allocations are safe.

Custom allocators must superimpose the `std.Alloc[T]` class, which provides method for allocation, re-allocation and
de-allocation.

This was the process in creating the memory allocation code:
