# 5. Type System

The S++ type system is strongly and statically typed. This means that all types are known at compile time, and that
types cannot be implicitly converted. Every type is a first-class object, including arrays, tuples, unions, functions
and classes. This means that they can all be passed as arguments, returned from functions, and assigned to variables,
enforcing the orthogonality of the language.

There are no "primitive" types with special syntax, like in C++. All types are defined in the standard library, and some
are known to the compiler, such as the integer-based classes, the boolean and void type. Again, these are all
first-class objects, so their semantic behaviour is the same as any object.

Type inference is used extensively, to the point that specifying a type for local variables that are given a value is
not allowed. This is because the type can be inferred from the value, and so specifying the type is redundant. This
also improves the readability of the code, as the type is not repeated.

Aliasing is supported in S++, allowing for the same type to be given multiple names. This is useful for when a type is
used in multiple places, but the name of the type is too long to be used everywhere. Furthermore, this allows for
importing types from namespaces into the current namespace.

There is no special syntax for casting, as the same behaviour can be achieved using standard function calls. To ensure
that all casts are normalized, however, the `From` type can be generically superimposed over a type, to allow conversion
from another type into it. This allows `Str.from(123)` to be used to convert an integer into a string, for example.

Generic types are supported and can be used with functions, classes, aliasing and superimposing. Generic parameters can
be required, optional or variadic, and can be constrained to a specific type or set of types. Constraints on `sup` block
generics allow for methods to optionally be added to a class, depending on the generic type.

Residual types are types that superimpose the `std.Residual` class. This class is used to represent a type that has a
fail and success state, and is used for error handling. The `Ret[Pass, Fail]` and `Opt[Type]` types superimpose this
class, and are analogous to `Result<T, E>` and `Option<T>` in Rust.

Union types are mapped to the `std.Var[Ts]` variant class, were the generic parameter `..Ts` is a variadic list of
types. This class is used to represent a type that can be one of multiple types, and is used for branching. It is
commonly seen with the `is` keyword, in pattern matching.

Flow typing is used with union types, to allow for a type to be treated as a possible internal type, within the scope of
the pattern match being considered. This reduces the amount of casting that is required, and improves the readability of
the code.

Arrays are the lowest level collection in S++, and are completely safe to use. See [Arrays](6-1-Arrays.md) for more.

Tuples are first-class objects, like in Rust. See [Tuples](6-4-Tuples) for more.
