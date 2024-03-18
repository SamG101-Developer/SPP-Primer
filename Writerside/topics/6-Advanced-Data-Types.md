# 6. Advanced Data Types

S++ has support for common composite data types:

- Tuples: a fixed-size collection of values of different types
- Arrays: a fixed-size collection of values of the same type

To enforce orthogonality in S++, all types are first-class objects. This means that, unlike C++, arrays are not a
special primitive type, but are instead a class that has its own API, for setting, getting, and deleting elements. A
tuple has the type `std.Tup[..Ts]`, and arrays have the type `std.Arr[T]`.
