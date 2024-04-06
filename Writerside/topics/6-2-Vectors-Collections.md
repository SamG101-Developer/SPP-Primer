# 6.2. Vectors & Collections

There are a number of collections in the standard library:

- `Arr[T]`: a fixed-size [array](6-1-Arrays.md).
- `Vec[T, B]`: a dynamic array that can grow and shrink.
- `Map[K, V, B]`: a key-value store, with a backend type `B` (`HashMap`, `TreeMap`, etc).
- `Set[T, B]`: a set of unique values, with a backend type `B` (`HashSet`, `TreeSet`, etc).
- `List[T]`: a linked list.
- `Queue[T, B]`: a queue, with a backend type `B` (`Vec`, `List`, etc).
- `Stack[T, B]`: a stack, with a backend type `B` (`Vec`, `List`, etc).
- `Deque[T, B]`: a double-ended queue, with a backend type `B` (`Vec`, `List`, etc).

## Vectors

Vectors are a growable collection of values that are the same type. They are a level above the `Arr[T]` type, and are
implemented as a dynamic array. This means that they can grow and shrink in size, and are more flexible than arrays.
Vectors can have a backend, to allow for different implementations of the vector to be used. The default backend is a
`Vec[T, _VectorBackend]`, which is a dynamic array.
