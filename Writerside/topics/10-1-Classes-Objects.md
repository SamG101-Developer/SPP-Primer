# 10.1. Classes & Objects

S++ has a unique class system that is inspired by Rust, but simplified and made more flexible. Classes have
different blocks for state and behavior. The `cls` block, used to define a class, contains the state only; this is a
list of attributes and their types. The `sup` blocks are used to define behavior over a class: methods, typedefs,
inheritance etc -- see [superimposition](10-2-Inheritance-Polymorphism.md#inheritance) for more information. Because
classes are types, they must have a
`PascalCase` name.

## Class declaration

Classes are declared using the `cls` keyword, followed by the name of the class. The class name must be in
`PascalCase`. The name is then optionally followed by a list or generic parameters required by the class and a block
of constraints in a `where` block. The body of the class is then defined in a block. The class block contains a list
of attributes and their types.

#### Class declaration example

```
cls Vector3D[T: Copy] {
    x: T
    y: T
    z: T
}
```

### Class attributes

Class attributes have a name and type. Because the name is a regular identifier (variable), it must be in snake_case.
Attributes can also be assigned default values, with the `x: Str = ""` syntax. The type of the attribute, like with
optional parameters, must still be specified, even though it can be inferred from the default value. This is to enforce
consistency and readability, and if the default value is removed, no other changes must be made.

Whilst the `Default` type can be superimposed over a class, it is not a compiler-known class, and doesn't have any extra
semantics.

## Forward declaration

Because the S++ compiler performs a "pre-pass", the symbols are already loaded in before any analysis begins. This
means that the order of definitions doesn't matter, meaning there is no point in including any type of syntax for
forward declarations. Declaring the same type twice will therefore result in an error.

## Superimposition

The behavior of a class is defined in 1 or more `sup` block. There are 2 different types of `sup` blocks; a "normal"
`sup` block, and an "inheritance" `sup` block. Normal sup blocks are used to superimpose methods and typedefs over a
class, and inheritance sup blocks are used to superimpose a class over another class. The inheritance sup block is
discussed in [inheritance](10-2-Inheritance-Polymorphism.md).

Superimposition provides a clear and organized way to define behaviour over classes, separated into as many sections as
needed. Even classes from other modules can be superimposed onto or with.

#### Superimposition example

```
cls Foo {
    a: I32
    b: I32
}

sup Foo {
    use Str as In

    fun foo(&self, s: Self.In) -> Void { ... }
    fun bar(&self, s: Self.In) -> Void { ... }
    fun baz(&self, s: Self.In) -> Void { ... }
}
```

### Optional superimposition

Superimposition over classes with generic parameters can be optional by using constraints. This allows certain
methods to be defined on a class only if it's generic parameters meet certain constraints. This is useful for defining
methods that only work on certain types, for example, optionals or copyables, etc.

#### Optional superimposition example

This example defined a method called `special_copy` that only exists on `Foo` classes if `T` superimposes `Copy`
itself (force by the generic constraint on `T` in the `sup` block declaration).

```
cls Foo[T] {
    a: T
    b: T
}

sup [T: Copy] Foo[T] {
    fun special_copy(&self) -> Self { ... }
}
```

## Initializing a class

Classes have no definable constructor, as it is the same as defining static method, allowing there to be 2 ways to do
the same thing. Instead, object initializers are available, which allow an object to be constructed and its attributes
set, without the need for a constructor. Because types are always PascalCase, it is obvious when an object is being
initialized vs a function being called; for this reason object initializers are not required to have a keyword, and can
use parenthesis, keeping braces exclusively for blocks. All arguments must be named, and the order of the arguments does
not matter.

### Default values

Each variable must be provided, under a named argument like `Type(a=1)`, unless one of two conditions are satisfied:

1. The class superimposes `Default`, and therefore can pull attributes off a default instance of the class.
2. A default value is explicitly provided, using the `else=` syntax.

Currently, providing a default value moves this value entirely; it is being decided whether this object should actually
be partially moved, and only move attributes that haven't been specified in the object initializer. It is likely that
the object will remain fully moved, as this maintains orthogonality with moving a value into a function and only moving
certain attributes.

### Superclasses

If a class inherits other classes, then every superclass instance must be provided, in a tuple following `sup=`, unless
one of the two conditions are satisfied:

1. The parent class superimposes `Default`, and therefore can pull attributes off a default instance of the class.
2. The parent class is stateless, ie has no attributes.

### Object initialization example

```
cls Point {
    x: I32
    y: I32
    z: I32
}


let p = Point(x=1, y=2, z=3)
let q = Point(x=0, else=p)
```
