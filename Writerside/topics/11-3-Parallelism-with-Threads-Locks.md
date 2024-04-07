# 11.3. Parallelism with Threads & Locks

Parallelism is the act of running multiple tasks at the same time. This is done using the `Thread` class and its
associated primitives, as seen in other languages like C++ and Rust. There is no `synchronizes` keyword as seen in Java,
because mutexes are used to lock data structures, and combining this with the `with` block from Python, it is trivial to
lock and unlock certain objects as and when needed.

If a thread falls out of scope, it will finish execution and be joined automatically. If a thread is still running when
the program finishes, it will be forcibly terminated. This is to prevent memory leaks and to ensure that all threads
finish execution before the program exits.

## Threads

Threads are created using the `Thread` class, and are started using the `start` method. The `start` method takes a
list of arguments that are of the same type as the function being called. The `start` method returns a `Result` type,
wrapping the return value of the function being called.

Threads can be joined using the `join` method, which will block the current thread until the thread being joined has
finished execution. This is useful for waiting for a thread to finish before continuing execution.

```
fun main() -> Void {
    let t = Thread(target=fun (a: I32, b: I32) -> I32 { ret a + b })
    t.start()
    std.print(t.join().unwrap())
}
```

## Locks

Mutexes are used to lock data structures, but must be combined with the reference counted `Shared` type to allow for
mutability. This is because the `Shared` type is a reference counted type, and can be shared between threads.

```
fun main() -> Void {
    let m = Mutex(value=0))
    
    with value = m.lock() {
        value += 1
    }
}
```

A context block is used so that the lock is released when the block is exited (in the .exit() method of the Mutex type,
returned by the .lock() method). Alternatively, an unnamed scope could be used, and the destructor of the Mutex type
would be called when the scope is exited, releasing the lock.

### Sharing mutexes between threads (TODO)

This will **fail**, because `m` is moved twice, into both handle functions.:

```
fun main() -> Void {
    let m = Mutex(value=0))
    let h = [Thread]
    
    h.push(Thread(target=fun () with [m] -> Void {
        with value = m.lock() { value += 1 }
    }))
    
    h.push(Thread(target=fun () with [m] -> Void {
        with value = m.lock() { value += 1 }
    }))
    
    h.iter_ref().for_each(fun (t: &Thread) -> Void { t.join() })    
}
```

To get around this, the `Shared` type must be used:

```
fun main() -> Void {
    let m = Shared(value=Mutex(value=0))
    let h = [Thread]
    
    h.push(Thread(target=fun () with [m1 = m.clone()] -> Void {
        with value = m1.lock() { value += 1 }
    }))
    
    h.push(Thread(target=fun () with [m1 = m.clone()] -> Void {
        with value = m1.lock() { value += 1 }
    }))
    
    h.iter_ref().for_each(fun (t: &Thread) -> Void { t.join() })
}
```

This will work, because the `Shared` type is reference counted, and can be shared between threads. The `Shared`
type's `.clone()` method is used to create a new reference to the `Shared` type, whose underlying data is shared between
the threads.

