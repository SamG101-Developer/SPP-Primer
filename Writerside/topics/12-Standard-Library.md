# 12. Standard Library

The standard library contains implementations for basic data structures and algorithms:

## Types:

| Type                    | Description                                          |
|-------------------------|------------------------------------------------------|
| `Tup`                   | A fixed-size collection of values of different types |
| `Arr`                   | A fixed-size collection of values of the same type   |
| `Vec`                   | A growable collection of values of the same type     |
| `Str`                   | A growable collection of characters                  |
| `Map`                   | A collection of key-value pairs                      |
| `Set`                   | A collection of unique values                        |
| `Opt`                   | A type that represents either a value or nothing     |
| `Res`                   | A type that represents either a value or an error    |
| `Bool`                  | A type that represents either `true` or `false`      |
| `BigNum`                | A type that represents a large number                |
| `BigDec`                | A type that represents a large decimal number        |
| `U[8,16,32,64,128,256]` | Unsigned integer types                               |
| `I[8,16,32,64,128,256]` | Signed integer types                                 |
| `F[8,16,32,64,128,256]` | Floating point types                                 |

The standard library is designed with classes that provide an API over backends for the type. This means that rather
than having a `HashMap`, `TreeMap`, `BTreeMap`, etc, there is a single `Map` type that can be used with any backend,
where the backend is specified as a generic argument. This allows for the same code to be used with different backends,
without needing to change the `Map` code. This is seen in the `Str` type too, where a `VectorString` or `RopeString` may
be used as the backend.
