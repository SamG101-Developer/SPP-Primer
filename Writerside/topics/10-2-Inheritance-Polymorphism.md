# 10.2. Inheritance &amp; Polymorphism
In S++, [superimposition](10-1-Classes-Objects.md#superimposition) is used for inheritance, by extending the normal 
superimposition syntax slighty. Because any number of superimposition blocks can be defined, multiple inheritance is 
supported.

## Inheritance
Inheritance is done by using the `sup` keyword, followed by the name of the class to inherit from. Following this is 
the `on` keyword, and then the type being superimposed onto.

### Inheritance example#
```s++
cls Foo {
    a: I32
    b: I32
}

cls Bar {
    c: I32
    d: I32
}

sup Bar {
    fun foo(&self) -> Void { ... }
    fun bar(&self) -> Void { ... }
}

sup Foo on Bar {
    fun foo(&self) -> Void { ... }  # overrides Bar.foo
    fun bar(&self) -> Void { ... }  # overrides Bar.bar
}
```

### Multiple inheritance problem mitigations
#### Diamond problem
If two types both inherit from the same type, and then both types are inherited into another type, then it is 
possible that there are ambiguous function calls. There are ambiguous functions calls, if more than one class 
overrides a method, and then both of those classes are inherited into another class. If the method isn't overriden, 
or is only overidden in 1 class, then there is no ambiguity, and this is the version of the method called.

If there are ambiguous function calls, then the type who owns the desired function to be called must be specified: 
for example `B.foo(d)` specifies that the overriden implementation from `B` is desired.
