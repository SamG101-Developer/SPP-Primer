# 7.5. Heap & Stack
In S++, the stack is used aggressively, with the heap only ever being used for arrays, as they can be resized. This 
means that the heap is not used for any other purpose, and so the risk of memory corruption is greatly reduced. 
Because there are no global variables, or static class variables, and borrows are 2nd class, using the stack for 
almost everything is possible.

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

#### Shadow stacks

#### Stack overflow / underflow detection

### Integrity related

#### Control flow integrity

#### Data flow integrity

#### Code signing

#### Sandboxing

### Other

#### Address space layout randomization

#### Data execution prevention
