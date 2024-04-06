# 9.2. Error Handling & Opt/Ret

Error handling in S++ is done similarly to in Rust, using monadic error handling. The `Ret` (for return) type is used,
as it can hold a pass and fail state. The `Opt` (for optional) type is used to hold a value that may or may not
exist.

Here is a brief example of the `Opt` class:

```
cls None { }
use [T] Opt = T | None

sup [T] Residual[T, None] on Opt[T] {
    fun is_some(&self) -> Bool {
        ret case self is then None { false } else { true }
    }
    
    fun is_none(&self) -> Bool {
        ret case self is then None { true } else { false }
    }
    
    fun unwrap(&self) -> T {
        ret case self then
            is None { abort("called 'Opt.unwrap()' on a 'None' value") }
            is T { self }
    }
}
```
