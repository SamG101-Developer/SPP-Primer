# 7. Memory Management

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
