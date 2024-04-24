# 3.1. Variables & Mutability

Variables are used in S++, like any other programming language, to store data. A variable has a type, which is
always fully inferred if the variable is given a value at declaration. Otherwise, the type must be specified.
Variables must also conform to snake_case naming conventions; capital letters can not be used in variables eve (they
are reserved for types).

## Declaring a variable

There are 2 ways variable declarations work: with and without a value. If a value is given, the type is inferred. If
no value is given, the type must be specified. Note that a variable that isn't given a value cannot be used until it
is given a value with an [assignment](3-2-Expressions-Operators.md). Within variables-with-values, there are 3
different ways to declare a variable: single, tuple, and struct.

### Single variable declaration

```
fun main() -> Void {
    let x = 123
    let y: Str
}
```

| Variable | Type     | How type is determined |
|----------|----------|------------------------|
| `x`      | `BigNum` | Inferred from RHS      |
| `y`      | `Str`    | Declared as `Str`      |

### Tuple variable declaration

```
fun main() -> Void {
    let (x, y) = (1, false)
    let (a, b): (BigNum, Str)
}
```

| Variable | Type     | How type is determined                  |
|----------|----------|-----------------------------------------|
| `x`      | `BigNum` | Inferred from RHS                       |
| `y`      | `Bool`   | Inferred from RHS                       |
| `a`      | `BigNum` | Declared as `BigNum` (tuple part known) |
| `b`      | `Str`    | Declared as `Str` (tuple part known)    |

- The RHS can be any value as long as it is a tuple, and the number of parts in the tuple matches the number of
  variables being declared.
- Placeholder identifiers, `_`, can be used to ignore certain single parts of the RHS tuple.
- The variadic placeholder, `..`, can be used to capture or ignore a subset of the RHS tuple.

#### Placeholder example:

| Variable declaration                | x | y            | z |
|-------------------------------------|---|--------------|---|
| `let (x, _, _) = (1, 2, 3)`         | 1 | -            | - |
| `let (_, y, _) = (1, 2, 3)`         | - | 2            | - |
| `let (_, _, z) = (1, 2, 3)`         | - | -            | 3 |
| `let (_, _, _) = (1, 2, 3)`         | - | -            | - |
| `let (x, ..y) = (1, 2, 3, 4, 5)`    | 1 | (2, 3, 4, 5) | - |
| `let (x, .._, z) = (1, 2, 3, 4, 5)` | 1 | -            | 5 |

- Note that only 1 variadic placeholder can be used per tuple declaration.

### Struct variable declaration

```
let Point(x, y) = Point(x=1, y=2)
let Point(a, b): Point
```

| Variable | Type     | How type is determined                      |
|----------|----------|---------------------------------------------|
| `x`      | `BigNum` | Inferred from RHS                           |
| `y`      | `BigNum` | Inferred from RHS                           |
| `a`      | `BigNum` | Declared as `BigNum` (attribute type known) |
| `b`      | `BigNum` | Declared as `BigNum` (attribute type known) |

- If not all attributes are declared, the `..` operator must be used to indicate that the remaining attributes are
  being ignored (and not forgotten about).

### Recursive variable destructuring

Variables can be declared with recursive variable destructuring, allowing a mix of tuple, struct and standard variable
declarations. This might look like: `let Vec(pos=(x, ..), dir) = vector`. This would only take the `x` of the `pos`, and
the `dir` attributes of the `vector` variable. There is no limit to the amount of recursion that can be done with
variable declaration destructuring.

## Mutability of a variable

Whenever a variable is declared, it is immutable by default. Immutability by default is a feature taken from Rust,
and allows for safer programming, as there is it prevents unexpected and accidental changes to variables. To make a
variable mutable, the `mut` keyword must be used with the `let` keyword. To make a parameter mutable, prefix its
identifier with the `mut` keyword. Tuple and struct parts must be individually marked as mutable. See the page
on [immutability](9-4-Immutability.md) for more information.

The mutability of a variable is not tied to the variable's type, but to the variable itself, simplifying the language by
a large amount.

### Variable mutability example:

```
fun main() -> Void {
    let mut x = 1                          # x is mutable
    let (mut x, y) = (1, 2)                # x is mutable, y is immutable
    let Point(mut x, y) = Point(x=1, y=2)  # x is mutable, y is immutable
}
```

### Parameter mutability example:

```
fun function_name(mut x: BigNum, z: BigNum) -> Str {
    # x is mutable
    # y is immutable
}
```

## Scope of a variable

A variable is only accessible within the scope it has been declared in. The "scope" is determined by the closest
binding `{ }` block. Static variables do not exist in S++, meaning class variables are always unique to the instance
they are defined in. Global variables can be defined but only mutably in S++. Global variables must be initialized on
definition, and can be accessed from any scope. They cannot be moved, mutably borrowed or partially moved from.

## Assigning to a variable

A variable can be assigned to with the `=` operator. The type of the RHS must match the type of the LHS explicitly,
as not even automatic up-casting is allowed. This is to prevent accidental type conversions, which can be dangerous.
Assignment can only be performed on `mut` variables, or uninitialized variables that haven't got their first value
assigned yet.

### Assignment example:

```
let mut x = 1
x = 2
```

## Re-declaring a variable

Re-declaring variables is allowed, including to change the type of the variable. This is to allow for variables to keep
the same name even after a change in type, as this can be useful for readability. Re-declaring a variable is
essentially the same as declaring a new variable with the same name, but the old variable is removed from scope. The
mutability of the variable can also be changed when re-declaring.

### Re-declaration example:

```
fun main() -> Void {
    let x = 1
    let x = Str.from(x)  # x is now a Str
    let mut x = x        # x is now a mutable Str
}
```

## Shadowing a variable

A variable that has been declared in an outer scope can be shadowed by a variable with the same name in an inner
scope. If a variable is shadowed, then inside the inner scope, the new variable is used, and once the scope has
ended, the original variable is used again. This is useful for re-using variable names, and for readability.

### Shadowing example #1:

```
fun main() -> Void {
    let x = 1
    {
        let x = 2
        std.print(x)  # prints 2
    }
    std.print(x)  # prints 1
}
```

### Shadowing example #2:

```
fun main() -> Void {
    let mut x = 1
    {
        x = 2
        std.print(x)  # prints 2
    }
    std.print(x)  # prints 2
}
```
