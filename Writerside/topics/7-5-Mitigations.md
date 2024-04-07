# 7.5. Mitigations
Due to the extensive memory safety mechanisms, avery possible memory error is caught at compile time.

#### Null pointer dereference
Null pointer dereferences occur when a pointer isn't pointing to anything, and the program tries to access the 
memory at that address. In S++, pointers are never used. Instead, borrowed values are used, which are guaranteed to 
always be valid due to their second-class nature. This means that null pointer dereferences are impossible.

#### Use-after-free / dangling pointers
Use-after-free errors occur when a pointer is used after the memory it points to has been freed. This is not 
possible in S++, because borrows are [second-class](7-2-2nd-Class-Borrows.md), and so are guaranteed to be valid for 
the lifetime of the borrow.

#### Use of uninitialized memory
Use of uninitialized memory occurs when a pointer is used before it has been initialized. This is not possible in 
S++, because when a variable is uninitialized, or declared without a value, the compiler will only allow it to be 
used for having a value assigned to it. This means that uninitialized memory cannot be used.

#### Double free
Double free errors occur when a pointer is freed twice. This is not possible in S++, because ownership is tracked, 
meaning that an object cannot be used (and therefore cannot be consumed) after it has already been consumed. This 
means that a value cannot be freed twice. This is a special case of
[use of uninitialized memory](#use-of-uninitialized-memory).

#### Memory leaks
All owned objects are freed at the end of their scope, and because all borrows are second-class, they are stored on 
the stack, and freed when the stack frame they are in is popped. This means that memory leaks are impossible. When 
an object destructs, it recursively destructs all of its owned objects (attributes), ensuring that all memory is freed.

#### Buffer overflows
All array writes and reads are bounds-checked, ensuring that no out-of-bounds accesses can ever occur. As the `Arr[T]`
array type is the lowest level collection in S++, all other collections are based on arrays, and so are also 
bounds-checked.

#### Memory corruption
The heap isn't used in S++, which heavily mitigates the risk of memory corruption. The stacks use a number of 
protections to ensure that they cannot be corrupted. See the [stack protections]() section for more.

#### Pointer arithmetic

#### Type conversion errors

#### Race conditions

#### Deadlocks

#### Static data

#### Global data

#### Alignment

#### Stack overflow

#### Heap overflow
