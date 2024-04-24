# 7. Memory Management

S++ has partially automatic memory management. The programmer never has to manually allocate or deallocate memory;
object initialization allocates an object, and either a move or a destructor deallocates it. Borrows, however, must be
created manually, so the compiler knows whether a mutable or immutable borrow is being created.

It would have been possible to make borrows be created automatically by checking the function prototype being called,
and match argument to parameter conventions, but this would make it difficult to see where borrows are being created,
and overloads could not be created with different conventions to arguments, because there would be no way to determine
which one to use, so `&` and `&mut` are used instead.

Borrows are like Rust's borrows: they are pointers to an object, cannot be null and are guaranteed to be valid. There is
no `unsafe` mechanism in S++, because safe code can always be written, and `unsafe` code is a sign of a language
deficiency.

S++ uses three separate techniques in tandem to safely manage memory, whilst not compromising performance or
readability. These techniques are:

- Ownership tracking
- Second-class borrows
- The law of exclusivity

## Ownership

[Ownership Tracking](7-1-Ownership.md) is an important concept to ensure that non-initialized/moved objects and
part-initialized objects are never used. This prevents the undefined behavior seen in C/C++ when using uninitialized
memory. The only way to use an uninitialized/part-initialized object is when assigning it, or its attributes, a value.

## Second-class borrows

[Second-class borrows](7-2-2nd-Class-Borrows.md) are used to ensure that all borrows are always valid, without the need
for lifetime analysis. This is achieved by only allowing borrows to be taken at function call sites, and from yielding
values from coroutines. This means that borrows are guaranteed to be valid, because they owned object exists in the
outer scope, and the borrow is created in the inner scope.

## The Law of Exclusivity

[The Law of Exclusivity](7-3-The-Law-of-Exclusivity.md) is used to prevent mutability conflicts between overlapping
borrows. Either one mutable, or n immutable, overlapping borrows can exist at any one time.
