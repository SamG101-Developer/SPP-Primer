# 9.3. 1st Class Functions

First-class functions are used in S++ to allow functions to be treated as values. This means that functions can be
passed as arguments to other functions, returned from functions, and assigned to variables. This is a key concept in
functional programming, and allows for a lot of flexibility in how functions can be used.

There are three function types: `FunMov`, `FunRef`, and `FunMut`. These types are used to represent functions that
consume, borrow, and mutably borrow their environment, respectively. These types are used in the same way as normal
functions, but with the added ability to be passed around as values.

## Function Types

### `FunMov`

A function with a `self` or `mut self` parameter is a `FunMov` function, as it consumes its `self` environment. This
means that the object that the method belongs to will be destroyed after this function is called, meaning that the
object cannot be used again until it has been re-assigned a new value.

### `FunRef`

A function with a `&self` parameter is a `FunRef` function, as it borrows its `self` environment. This means that the
object that the method belongs to will be borrowed, and can be used again after the function has been called. Free
functions, ie functions that do not have a `self` parameter, are also `FunRef` functions.

### `FunMut`

A function with a `&mut self` parameter is a `FunMut` function, as it mutably borrows its `self` environment. This means
that the object that the method belongs to will be mutably borrowed, and can be used again after the function has been
called. This is useful for functions that need to modify the object that they belong to, for reasons such as updating
internal state.

## Moving functions from objects.

The preprocessor converts functions into classes with `Fun[Ref|Mut|Mov]` superimposed over them, so that they can be
treated as first-class objects. This prevents methods from being moved off a class, as they are technically not treated
as attributes, but treated as symbols within the scope of the class.

Methods wouldn't be able to be re-assigned anyway, because their type is unique and non-accessible.

For example:

```
cls ClassA { }
sup ClassA {
    fun method(a: Str) -> Void { }
    fun method(a: U64) -> Void { }
}
```

becomes:

```
cls ClassA { }
sup ClassA {
    cls MOCK_method { }
    sup FunRef[Void, (Str)] on MOCK_method {
        fun call(self, a: Str) -> Void { }
    }
    sup FunRef[Void, (U64)] on MOCK_method {
        fun call(self, a: U64) -> Void { }
    }
    
    let method = MOCK_method();
}
```

It can be seen that the `method` attribute is now a `MOCK_method` object, which is not accessible, and so cannot be
reassigned.