# 2.3. Keywords

#### `mod`
The `mod` keyword is used to declare a module. Every `.spp` file included in a project must be declared as a 
module. The module name must reflect the directory of the file, up to and including the `src` directory. For example, the
file `src/foo/bar.spp` must have the module name `src.foo.bar`. The module declaration must be the first line of the
file.

#### `cls`
The `cls` keyword is used to declare a [class](10-1-Classes-Objects.md#class-declaration). Only the state of a class 
is defined in a `cls` block (the attributes). Class blocks can only be declared at the module level, and order of
declaration does not matter.

#### `sup`
The `sup` keyword is used to define behavior on a class, known as
[superimposition](10-1-Classes-Objects.md#superimposition). Methods and typedefs can be superimposed over a class, 
or another class can be superimposed over a class. Class superimposition is similar to inheritance in other 
languages; see [inheritance](10-2-Inheritance-Polymorphism.md#inheritance) for more information. Superimposition blocks
can only be declared at the module level, and order of declaration does not matter.

#### `fun`
The `fun` keyword is used to declare a [function](3-3-Functions.md#function-declaration). Functions can be declared 
in the module scope, or inside a `sup` block. Functions cannot be declared inside other functions, because
[closures](9-1-Lambdas-High-Order-Functions.md) are used instead, with a nearly identical syntax. Order of declaration
does not matter.
