# 3.3. Functions
In S++, there are 3 types of functions, similar to Rust. There is the `FunRef`, `FunMut` and `FunMov` function types.
All `fun` functions and methods are one of these 3 types, and can be passed around as values. The first-class nature 
of functions in S++ allows for a lot of flexibility in how they are used, and reinforces the orthogonality of the 
language.

## Function declaration
Functions are declared using the `fun` keyword, followed by the function name, a list of generic parameters, a list 
of parameters, a return type, and optional generic constraints.

```
fun foo(a: Str, b: Str) -> Str { ... }
```
```
@public(for="some/path/to/file.spp")
@inline(when="release")
fun foo[T, U: Copy](a: T, b: U) -> Void where [T: Add[Rhs=U]] { ... }
```

### AST Reduction
There is an intermediary stage in the compilation process called 
"AST Reduction", where functions are changed into objects that have the correct `Fun[Ref|Mut|Mov]` class 
superimposed over the type. This also supports overloading:

#### Original function declarations:
```
fun foo(a: Str) -> Void { ... }
fun foo(a: BigNum) -> Void { ... }
```

#### AST reduced function declarations:
```
cls __Mock_foo {}

sup FunRef[Void, (Str)] on __Mock_foo {
    fun call_ref(&self, a: Str) -> Void { ... }
}

sup FunRef[Void, (BigNum)] on __Mock_foo {
    fun call_ref(&self, a: BigNum) -> Void { ... }
}

let foo = __Mock_foo {};
```

## Function parameters
Function parameters always require a type annotation. This is a design decision, so that it is clear what the type 
of the parameters will be. It also allows overload resolution to be done, as if there were 2 methods of the same 
name with "auto" parameters, it would be impossible to know which one to call. Parameters are immutable by default, 
and require the `mut` keyword to be used to make them mutable, the same as variable declarations do.

### Parameter classifications
Parameters can be either required, optional, or variadic. The order of parameters must be in this order too.

#### The `self` parameter
The `self` parameter can only be used on `sup` methods, not normal functions in the module scope. Applying a 
convention to the `self` parameter is done slightly different, because a type is not required for the `self` 
parameter: it is always `Self`. The convention dictates how the environment of the function is captured.

| `self` convention | Description                                        |
|-------------------|----------------------------------------------------|
| `self`            | Consume the environment of the function immutably. |
| `mut self`        | Consume the environment of the function mutably.   |
| `&self`           | Immutably borrow the environment of the function.  |
| `&mut self`       | Mutably borrow the environment of the function.    |

#### Required parameters
Required parameters are parameters that must be specified when calling a function. They are declared by simply 
declaring a parameter with a type annotation. Here, `a` and `b` are required parameters:

```
fun foo(a: Str, b: Str) -> Void { ... }
```

#### Optional parameters
Optional parameters are parameters that can be omitted when calling a function. They are declared by declaring a 
required parameter, and giving it a default value. The default value must match the type of the parameter, which is 
kept in to keep the language consistent.

Unlike Python, the default value for each parameter is fetched at _call time_, not at _function declaration_ time. 
Optional parameters cannot be `&` or `&mut`, but can be `mut`. Optional parameters cannot be borrows, because 2nd 
class borrows only allow borrows to be taken at function call site or yield, neither of which are applicable to 
optional parameter default values.

In the following example, `b` is an optional parameter:

```
fun foo(a: Str, b: Str = "default") -> Void { ... }
```

#### Variadic parameter
A function can have 1 variadic parameter, which is a parameter that can take any number of arguments. A variadic 
parameter is declared like a required parameter, but with the `..` prefix, before the parameter name. The type of 
the parameter will be a tuple of its types.

For the variadic `(..a: Str)`, the type of the parameter `a` will be a 
tuple of strings. If the type of the variadic parameter is a variadic generic parameter, then each item in the tuple 
can be a different type. This is known at compiler time per function invocation.

Variadic parameter types can be borrows, because default values cannot be provided to variadic parameters, so the 
lifetime of the borrow can be guaranteed to be valid.

### Function parameter conventions
Function parameters can have conventions. These allow for borrows to be passed into functions, or for values to be 
moved into the function. Each convention taken at the function call site per argument must match the convention of 
the corresponding function parameter. There are 3 conventions: by-mov (move), by-ref (immutable borrow), and by-mut 
(mutable borrow).

#### By-mov (move)
This is the default convention, and is used when no convention is specified. It moves the value into the function, 
unless the `Copy` type has been superimposed over the argument type, in which case the value is _copied_ into the 
function. Either way, an owned value is passed into the function.

#### By-ref (immutable borrow)
This convention borrows the value immutably, and passes the borrow into the function. This is useful for large 
values, or values that are not `Copy`, as it avoids copying the value. This is the convention used when a `&` is 
prefixed to the parameter. The value cannot be mutated in-place. The mutability of the variable itself (ie can it be 
re-assigned), is controlled separately by the `mut` keyword prefixing the entire parameter.

#### By-mut (mutable borrow)
This convention borrows the value mutably, and passes the borrow into the function. This is useful for large values,
or values that are not `Copy`, as it avoids copying the value. However, it allows the function to take temporary 
ownership of the argument, so must be used only when absolitely required, in order to confirm with memory borrowing 
rules.

This is the convention used when a `&mut` is prefixed to the parameter. The value can be mutated in-place. 
Again, the mutability of the variable itself (ie can it be re-assigned), is controlled separately by the `mut`
keyword prefixing the entire parameter.


## Function return type
A single return type is required for each function. This is declared after the parameter list, and is separated by
the `->` token. The return type can be any type, including `Void`, which is required if no value is returned from
the function. The return type is never inferred. This is a design decision, so that it is clear what the return type
of the function will be, and reinforces the consistency of the language.

Whilst only 1 value can be returned from a function, this includes a tuple of values, which can be de-structured at
the call site. This is useful for returning multiple values from a function, without having to create a new type
to hold them.

### Returning a value
The `ret` keyword is used to return a value out of a function. An expression will follow the `ret` keyword if the
function returns a value. If the function returns `Void`, then the `ret` keyword is optional, and can be omitted. It 
may still be required, though, if it is not the final statement in the method (ie in a nested block).

Only owned values may be returned. This is explained in [2nd class borrows](7-2-2nd-Class-Borrows.md) in more detail.

#### Returning a single value:
```
fun foo() -> Str {
    ret "Hello, world!";
}
```

#### Returning multiple values wrapped in a tuple:
```
fun foo() -> (Str, Str) {
    ret ("Hello", "world");
}
```

## Function types
The 3 function types, as mentioned earlier are the `FunRef`, `FunMut` and `FunMov` function types. These all have 
slightly different intrinsics, and are required for the memory model. All of these classes superimpose the `Fun` class,
allowing for some behaviour to be shared between the 3 classes.

| Function type         | Description                         |
|-----------------------|-------------------------------------|
| `FunRef[Out, (Args)]` | Immutable borrow of the environment |
| `FunMut[Out, (Args)]` | Immutable borrow of the environment |
| `FunMov[Out, (Args)]` | Consume the environment             |

### Class methods
Class methods are functions inside `sup` blocks. The type of each method is determined by the convention of the 
`self` parameters:

| `self` convention | Method type |
|-------------------|-------------|
| `self`            | `FunMov`    |
| `mut self`        | `FunMov`    |
| `&self`           | `FunRef`    |
| `&mut self`       | `FunMut`    |

#### Static methods
Class methods that omit the `self` parameter are static methods. They must be called from the type, not from an 
instance of the type.

### Free functions
Functions in the global namespace are always `FunRef`, as their environment is the global namespace, which cannot be 
consumed, and cannot be mutated (this would be inherently unsafe).

### Lambdas & Closures
Lambdas' types are slightly more complicated due to potential environment capture. See
[lambdas](9-1-Lambdas-High-Order-Functions.md) for more detailed information on determining the type of captures.

## Function operators
For functions that return `Bool` values, the classes `std.ops.And`, `std.ops.Or` and `std.ops.Not` are superimposed, 
allowing for functions to be combined for easier chaining. For example, given functions `foo` and `bar` that return
`Bool` values, the function `let baz = foo && bar` combines the functions into a single function that returns 
logical and of the 2 functions.

Here are the superimpositions for the 3 operators:

```
sup [Out: Bool, ..Args] And on Fun[Out, (Args)] {
    fun and(self, that: Self) -> Self {
        ret fun(args: Args) -> Bool { ret self(args) && that(args) }
    }
}

sup [Out: Bool, ..Args] Or on Fun[Out, (Args)] {
    fun or(self, that: Self) -> Self {
        ret fun(args: Args) -> Bool { ret self(args) || that(args) }
    }
}

sup [Out: Bool, ..Args] Not on Fun[Out, (Args)] {
    fun not(self) -> Self {
        ret fun(args: Args) -> Bool { ret self(args).not() }
    }
}
```

## Function overloading
Functions can be overloaded with the same identifier, but different parameter types. The compiler will use [AST 
Reduction](#ast-reduction) to create a mock class and superimpose the correct `Fun[Ref|Mut|Mov]` class over the mock
class. This allows for functions to be overloaded, and for the correct function to be called at the call site.

Function parameter types and count can be overloaded for functions. The return type cannot be overloaded, as all 
type information comes on the right-hand-side of the expression, so the compiler would not know which overload is 
required, without specifying generics of the entire function which would then render automatic overload resolution 
obsolete anyway.

Parameter names and order cannot be overloaded, because argument names are not required, so specifying only values 
for the arguments would not be enough to determine which overload to call. The mutability and conventions of 
parameters cannot be overloaded either.

## Function overloading resolution
There are a number of checks that occur in order to detect the correct overload. These are:
1. Infer any generics from constraints or parameter types.
2. Inject "self" argument if the function is a non-static instance.
3. Check for any non-matching argument/parameter names for this overload.
4. Check that there are enough parameters left over for number of arguments.
5. Give each "normal" argument a name from the leftover parameters.
6. Check that each argument's convention & type matches the parameter's convention & type.

## Function recursion
Function recursion is supported, and all recursive functions are re-written to be tail call recursive. This allows 
for the tail call optimization to be applied to all recursive functions, and allows for infinite recursion to be 
used without stack overflow; the limiter becomes time rather than space, as the stack frame is replaced with the 
new stack frame, rather than a new one being created and added. See the topic on [recursion](9-5-Recursion.md) for more
detail.

## Calling functions
Functions and methods are called with parenthesis around the group of arguments. Arguments can be
[normal](#normal-arguments) or [named](#named-arguments), and can have a convention attached to them.

### Named arguments
Named arguments are arguments that are specified with a name, followed by a `=`, followed by an expression. When
overload resolution is taking place, any function overloads that don't have parameters with the argument names are
disregarded.

### Normal arguments
Normal arguments are just an expression. During function overload resolution, if a candidate function is being
considered based on the [named arguments](#named-arguments), then the normal arguments are then named against the rest
of the parameters, in order left to right. If the convention- & type-checking is successful, then the overload candidate
can be considered for the final overload resolution.

## Partial functions
Partial functions are functions that have some parameters omitted. This is useful for creating functions that are
partially applied, and can be used in higher order functions. Partial functions can be created in a couple of ways.
Either a [lambda](9-1-Lambdas-High-Order-Functions.md#lambdas) can be created where the
[captures](9-1-Lambdas-High-Order-Functions.md#captures) are the fixed parameters, or `_` tokens can be used as
placeholders. Note that for overloaded functions, this could lead to ambiguities because `_` doesn't have a type.
