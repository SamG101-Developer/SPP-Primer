# 5.3. Type Conversion & Casting

The type system is so strong that not even automatic upcasting is allowed. No other type of implicit casting is allowed
in S++; the type of the argument must be an exact symbolic match, to the parameter being matched against.

## Type casting

To cast between types, superimpose the `From[FromType]` type over the target type. This call contains a static `from`
method, using the origin type to create the target type. This can be superimposed any number of times for different
origin types. For example:

```
# "From" implementation
sup From[Origin] {
    use Origin = Origin
    
    fun from(that: Self.Origin) -> Self { }
}
```

```
cls Foo { }
cls Bar { }
cls Baz { }

sup From[Bar] on Foo {
    fun from(that: Self.Origin) -> Self { ... }
}

sup From[Baz] on Foo {
    fun from(that: Self.Origin) -> Self { ... }
}

fun main() -> Void {
    let x = Bar()
    let y = Foo.from(x)
}
```

Whilst using the `From` type isn't strictly required to cast types (any function could), it provided a consistent method
of casting between types, and can be used as a constraint for a generic type. There is a `From` type but not
a `To`/`Into` type, because S++ doesn't support return type overloading.

## Hierarchical casting

To cast up and down the type-tree, the standard library provides upcast and downcast functions:

```
std.upcast[Base, Derived: Base](obj: Derived) -> Base { }
std.downcast[Base, Derived: Base](obj: Base) -> Opt[Derived] { }
```

There are compile time checks to ensure that the `Base` and `Derive` types are hierarchically, linked. Because there is
no guarantee that a downcast is successful, because there could be any number of types that are derived from the `Base`
type.

The `upcast` function requires the `Base` type to be explicitly provided, and the downcast function requires
the `Derived` type to be explicitly provided.
