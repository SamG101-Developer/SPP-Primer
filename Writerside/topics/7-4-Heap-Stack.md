# 7.4. Heap & Stack

In S++, the stack is used aggressively, with the heap only being used for global constants. This is because the stack
is much faster than the heap, and because [second-class borrows](7-2-2nd-Class-Borrows) are used, the lifetime of
borrows is always less than the lifetime of the stack frame they are created in. This means that the stack can be used
for almost everything, and the risk of memory corruption is greatly reduced.

## Stack

### Stack protections

#### Stack canaries (stack cookies)

Every time a new stack frame is allocated, a random value is generated and stored on the stack. This value is placed
between the return address and the stack frame. When the function returns, the value is checked to ensure that it has
not been modified. If it has, then the program is terminated. This is one of the rare cases where a runtime error can
occur in S++.

#### Stack frame randomization

Stack frames have small amounts of random padding added to them, adjusting the exact location of the stack frame on
the stack. This makes it harder for an attacker to predict the location of the stack frame, reducing the risk of
attacks that utilize predicting memory locations.

#### Stack frame flags (non executable, non writable, immutable etc)

Stack frames have a 1-byte flag before the stack frame, which contains information about the privileges of the stack
frame. This includes whether the stack frame is executable, writable, immutable, etc. This is used to prevent attacks
that rely on modifying the stack frame, or executing code on the stack. As this would have a performance impact, it is
only used for critical stack frames, and applied with the [`stack_frame` annotation]().

#### Stack frame chaining (secure function calls)

#### Stack exhaustion

The stack canary is checked before the stack frame is popped, and if it has been modified, the program is terminated.
This will never result from array allocation on the heap (use the Alloc class for this).

#### Shadow stacks

Shadow stacks are used to store the return addresses of functions, and are checked when a function returns. If the
return address on the shadow stack does not match the return address on the stack, then the program is terminated.
This is not on by default due to the performance impact, but can be activated on a per-function basis using the
[`shadow_stack` annotation]().

### Integrity related

#### Control flow integrity

#### Data flow integrity

#### Code signing

#### Sandboxing

### Other

#### Address space layout randomization

#### Data execution prevention
