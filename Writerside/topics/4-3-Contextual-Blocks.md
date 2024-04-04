# 4.3. Contextual Blocks

S++ has a feature called **contextual blocks**, which are blocks of code that are executed under a context
manager, allowing an "enter" and "exit" method on some object to wrap the block of code. A type can be used as a context
manager if it superimposes either the `CtxRef` or `CtxMut` context manager type.

Context managers are used to ensure that resources are cleaned up correctly, even if an error occurs. This includes file
management, socket management, mutex acquiring/releasing, etc.

If a context's enter method returns a value, then "aliasing" is allowed for the context block; this allows the value
returned from the enter method to be used in the block. This is useful for acquiring a resource and using it in the
block. The "exit" method always returns `Void`.

The `CtxRef` and `CtxMut` context manager types are used to specify whether the context manager is read-only or
read-write, respectively. There is no `CtxMov`, because both the `enter` and `exit` methods would have to move
the `self` argument, which is not allowed.

Context manager definitions:
```
cls [T] CtxRef[T] { }

sup CtxRef[T] {
    use Out = T
    fun enter(&self) -> Self.Out
    fun exit(&self) -> Void
}
```

```
cls [T] CtxMut[T] { }

sup CtxRef[T] {
    use Out = T
    fun enter(&self) -> Self.Out
    fun exit(&self) -> Void
}
```


## How to make a type a context manager

```
use std.CtxRef

cls Mutex[T] {
    value: T
}

sup [T] CtxRef[Void] on Mutex[T] {
    fun enter(&self) -> Self.Out {
        print("Locking mutex")
    }

    fun exit(&self) -> Void {
        print("Unlocking mutex")
    }
}
