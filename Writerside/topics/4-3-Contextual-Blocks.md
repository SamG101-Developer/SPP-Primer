# 4.3. Contextual Blocks

S++ has a feature called contextual blocks, which are blocks of code that are executed in a specific context. This is
pretty much a direct copy of Python's `with` statement. To allow a type to be used contextually, one of
the `Ctx[Mov|Ref|Mut]` type must be superimposed over it. This allows the `.enter_[mov|ref|mut]()`
and `.exit[mov|ref|mut]()` methods to be optionally overridden, to allow for the contextual block to be entered and
exited.

If the return type of the enter method is `Void`, then the `with` expression cannot be aliased, as variables cannot hold
a `Void` type. Aliasing the result of the `with` expression is done with a normal `let` statement. The return type of
the enter method matches the generic parameter of the `Ctx{Mov|Ref|Mut}` type.

Contextual blocks are still heavily under development, as the convention of the `self` parameter is still undecided.
Whilst there could be individual context types (`CtxMov`, `CtxRef`, `CtxMut`), this presents issues with:
1. `CtxMov` would need to move the object twice, once for the enter method and once for the exit method.
2. How is which type to use decided? Can more than one be used?

## Example (in theory)

```
use std.Ctx

cls Mutex[T] {
    value: T
}

sup [T] CtxRef[Void] on Mutex[T] {
    fun enter(&self) -> Void {
        print("Locking mutex")
    }

    fun exit(&self) -> Void {
        print("Unlocking mutex")
    }
}
