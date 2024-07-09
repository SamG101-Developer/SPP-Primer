# 2.3. Keywords

S++ uses a small keyword set of just 23 keywords, significantly less than C++'s 95 and Rust's 39. This is to make the
language easier to learn and understand, and to make the code more readable. Keywords of the same group have the same
length, to make the code more aligned.

All keywords have a specific use, with potential sub-uses, and there are no non-obvious keyword ambiguities. For
example, in Rust there are the `&` and `&mut` operators, and `mut`, `ref` and `move` keywords, which all have different
uses, some that can only be used in certain places, and some cases where multiple can be used in the same place with
different non-obvious semantics. S++ addresses this by having clear and distinct uses for each keyword and operators.

## Module Level Keywords

#### `mod`

The `mod` keyword is used to declare a module. Every `.spp` file included in a project must be declared as a
module. The module name must reflect the directory of the file, up to and including the `src` directory. For example,
the file `src/foo/bar.spp` must have the module name `src.foo.bar`. The module declaration must be the first line of the
file.

#### `cls`

The `cls` keyword is used to declare a [class](10-1-Classes-Objects.md#class-declaration). Only the state of a class
is defined in a `cls` block (the attributes). Class blocks can only be declared at the module level, and the order of
declaration does not matter.

#### `sup`

The `sup` keyword is used to define behaviour on a class, known as
[superimposition](10-1-Classes-Objects.md#superimposition). Methods and typedefs can be superimposed over a class, or
another class can be superimposed over a class.

Class superimposition is similar to inheritance in other languages;
see [inheritance](10-2-Inheritance-Polymorphism.md#inheritance) for more information. Superimposition blocks can only be
declared at the module level, and the order of declaration does not matter.

#### `fun`

The `fun` keyword is used to declare a [function](3-3-Functions.md#function-declaration). Functions can be declared
in the module scope, or inside a `sup` block. Functions cannot be declared inside other functions because
[closures](9-1-Lambdas-High-Order-Functions.md) are used instead, with a nearly identical syntax. Order of declaration
does not matter.

#### `use`

The `use` keyword is used to declare a [type-alias](5-6-Aliasing.md), which can include bringing in a type from another
module. This might look like `use OldType as NewType` or `use some.module.(X as Type1, Y as Type2)`. Type-aliases can
be declared in any scope, including the module scope. Order of declaration does not matter in the module or sup scope,
but follows normal program flow within a runtime scope, i.e. a function body.

## Variable Keywords

#### `let`

The `let` keyword is used to declare a [variable](3-1-Variables-Mutability.md). This is only used within a runtime
scope. Variables are defaulted to immutable.

#### `mut`

The `mut` keyword has a few different uses, all relating to
["mutability"](3-1-Variables-Mutability.md#mutability-of-a-variable). It's a "modifier" keyword - it is used in three
places:

- `let mut`: mutable variable declaration.
- `mut param`: mutable parameter declaration.
- `&mut`: mutable borrow.

## Control Flow Keywords

#### `case`

The `case` keyword is used to declare a [conditional branching block](4-1-Conditional-Branching.md), otherwise known as
the traditional `if` expression. The keyword `case` was chosen to keep consistent keyword length with other control flow
keywords. The `case` condition is followed by a number of [pattern blocks](4-1-Conditional-Branching.md#patterns).

#### `else`

The `else` keyword can be used in a few different situations. It can be used in
[condition branching](4-1-Conditional-Branching.md) to declare the "else" branch, which will be executed if none of the
other branches are executed.

It can also be used in a [loop](4-2-Conditional-Looping.md) to declare the "else" branch, which will be executed if the
condition of the `loop` expression is already false. The final use is in object initializer expressions, where it is
used to declare the default value of an object, to fill in attributes that don't
have default values given.

#### `loop`

The `loop` keyword is used to declare a [conditional loop](4-2-Conditional-Looping.md), otherwise known as the
traditional `while` loop. The keyword `loop` was chosen to keep consistent keyword length with other control flow
keywords. The `loop` expression can be followed by an `else` block, which will be executed if the condition of the
`loop` expression is already false.

#### `with`

The `with` keyword is used to declare a [context block](4-3-Contextual-Blocks.md), taken from Python. The `with` keyword
must be followed with an expression whose inferred type superimposes the `std.Ctx` type. On entering the block, the
`.enter()` method is called on the value, and on exiting the block, the `.exit()` method is called on the value.

## Control Flow Exit Keywords

#### `ret`

The `ret` keyword is used to exit a subroutine function, returning a value. The value must be of the same type as the
function's return type. There can be any number of return statements in a function. See
[functions](3-3-Functions.md#returning-a-value) for more information.

#### `gen`

The `gen` keyword is used to suspend a coroutine function, yielding a value. The value must be of the same type as the
function's return type's `Yield` generic type parameter. There can be any number of yield statements in a function.
Values can be received when suspending a coroutine function, and the value received must be of the same type as the
function's return type's `Send` generic type parameter. See [coroutines](11-2-Concurrency-Coroutines.md) for more
information.

## Type Helper Keywords

#### `where`

The `where` clause is used to clearly list constraints on generic types. It allows for multiple constraints on multiple
types, and can be used in functions, classes, superimpositions or type-aliases. Shorter constraints can be written
inline in the generic type list, but the `where` clause is used for longer constraints.

#### `is`

The `is` keyword is used to check if a value is a certain type inside a [union type](5-5-Union-Types.md#). It is seen
commonly in pattern matching.

#### `as`

The `as` keyword is used for aliasing typedefs, for example, `use std.{Opt as Optional, Ret as Return}`. This is taken
from Rust.

## Type Keywords

#### `true`

The `true` keyword is used to represent the boolean value `true`, a program-long constant.

#### `false`

The `false` keyword is used to represent the boolean value `false`, a program-long constant.

#### `self` (val)

The `self` keyword is used to referer to the current instance of a class within the class itself. It is used to access
attributes and methods of the class.

#### `Self` (type)

The `Self` keyword is used to refer to the current type within a class. It is replaced at compile time with the actual
type of the class, and is purely used to shorthand the type of the class. It can be used to access type-aliases of the
class too.

## Logical Operator Keywords

#### `and`

The `and` keyword, taken from Python, is used to represent the logical `and` operator, used in binary expressions.

#### `or`

The `or` keyword, taken from Python, is used to represent the logical `or` operator, used in binary expressions.

#### `not`

The `not` keyword, taken from Python, is used to represent the logical `not` operator. Unlike most languages which
use `not` as a unary operator, S++ uses it as a postfix operator: `a().b.not`, as the `not` applies to the final part of
an expression.

## Miscellaneous Keywords

#### `on`

The `on` keyword is used to superimpose a class over another class. It is used
for [class superimposition](10-1-Classes-Objects.md#superimposition).

#### `in`

The `in` keyword is used for looping through an iterator. It is paired with the `loop` keyword.

#### `then`

The `then` keyword is required by the parser, following a `case` condition, to separate the condition from the patterns
that follow per branch. **This is likely to be changed in the future**.

#### `async`

The `async` keyword is used as a function call modifier, to call a function is an asynchronous manner. This is used in
conjunction with `await`, which is not a keyword, but a method on the `Fut` type.
