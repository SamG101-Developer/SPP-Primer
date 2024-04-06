# 5.4. Generics

S++ has a powerful generics system allowing for the creation of reusable code. Generics can be used with functions,
classes, typedefs and superimpositions, and are defined with the `[...]` syntax, inspired by Python, rather than the
`<...>` syntax used in Java, C++ and Rust.

## Where generics can be used

Generic parameters in classes come after the name of the class, i.e. `class MyClass[Type]`. They can be used for
attribute types. Constraining a generic parameter of a class means that the class can only be instantiated with a type
that satisfies the constraint.

Generic parameters in functions come after the name of the function, i.e. `fun my_function[Type](...) {...}`. They can
be used for parameter types, the return type and local variable types. Constraining a generic parameter of a function
means that the function can only be called with a type that satisfies the constraint. This allows overloads to be
created based on the generic parameter.

Generic parameters in typedefs come after the `use` keyword, and before the identifier, like for Rust's `impl` keyword.
This is because the generics parameters are part of the type's definition. An example of this
is `use [T] Vec[T] as MyVec[T]`. Constraining a generic parameter of a typedef means that the type can only be used with
a type that satisfies the constraint.

Generic parameters in superimpositions come after the `sup` keyword, and before the identifier, like for Rust's `impl`
keyword. This is because the generics parameters are part of the type's definition. An example of this is
`sup [T] BaseClass[T] on DerivedClass[T]`. Constraining a generic parameter of a superimposition means that the methods
and types introduced in the `sup` block can only be used when a type that satisfies the constraint is the argument of
that generic parameter.

## Generic parameter classifications

Generic parameters are 1 of 4 types:

| Type                | Corresponding Argument | Inferred            |
|---------------------|------------------------|---------------------|
| Required            | Must be specified      | Cannot be inferred  |
| Required-Inferrable | Must not be specified  | Are always inferred |
| Optional            | Can be specified       | Cannot be inferred  |
| Variadic            | Must not be specified  | Are always inferred |

The order of generic parameter specification is as follows:

1. Required generic parameters
2. Required-Inferrable generic parameters
3. Optional generic parameters
4. Variadic generic parameters

This is because required generic parameters must be given corresponding generic arguments, either with a normal generic
argument or a named generic argument. Following this, required-inferrable generic parameters must be inferred, and
cannot be specified. However, they are still required generic parameters, and are therefore needed in the signature, so
they must come after the non-inferrable-required generic parameters.

Next, optional generic parameters can be specified. Optional generic parameters must be specified with named generic
arguments, as they are optional. This allows for non-inferrable-required generic parameters, and optional generic
parameters, to both be specified, without there being a chance to specify inferable-required generic parameters.
Finally, variadic generic parameters are inferred, and cannot be specified.

```
fun my_function[T, U, V=Str, ..Ts](a: U, b: FunMov[Bool, (Ts)]) {...}

my_function[Str, V=Bool](a, b)
```

In this example:

- `T` is a non-inferrable-required generic parameter, and must be specified.
- `U` is an inferrable-required generic parameter, and is inferred.
- `V` is an optional generic parameter, and is specified.
- `Ts` is a variadic generic parameter, and is inferred.

## Inferring generic arguments

### Classes
- Class attribute type.
- Constraint of another generic parameter.

### Functions
- Return type.
- Parameter type.
- Constraint of another generic parameter.

### Typedefs
- If the generic is given to the LHS type.

### Superimpositions
- If the generic is given to the class being superimposed over.

## Generic constraints

## Specialization

## Void

The `Void` type can be used as a generic argument for a generic parameter, but cannot be used for a class attribute
type. This is because representing the absence of a value is not possible in S++. Using `Void` as a parameter type
removes the parameter from the overload being considered. This is seen a lot in the `Gen.next(value: Send)` method of
the `Gen` class, as the parameter type is the `Send` generic parameter of the `Gen` class, but defaults to
`Send=Void`, meaning that a lot of the time, `.next()` doesn't take an argument.
