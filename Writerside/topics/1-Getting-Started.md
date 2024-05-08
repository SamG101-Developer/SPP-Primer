# 1. Getting Started

## Origins & History

S++ was created to primarily capture the speed and safety of Rust and the readability and simplicity of Python. It is
designed to remove all the bad, overly complex and non-orthogonal aspects of every language, and keep everything else.
This includes addressing the issues of Rust's complex syntax & lifetime analysis, C++'s lack of safety and readability,
Python's lack of performance, Go's lack of generics, etc.

S++ is designed to continuously evolve, and will not guarantee backwards compatibility between versions. This will be
visible under the versioning system of the language, with each major version increment representing one or more breaking
changes.

Certain features of S++ are inspired by other languages, but are generally modified to fit the language's design
principles. Examples include a modified borrowed checker (inspired by Rust), context blocks (inspired by Python) and
superimposition-based type inheritance (inspired by Rust). The underlying syntax is loosely based on the C family of
languages, but with all the unnecessary and legacy parts removed, forcing a consistent and readable syntax.

## Language Philosophy & Core Principles

- **Performance**: S++ is designed to be a high-performance language, with a focus on runtime performance. This is
  achieved by compiling S++ to native code, using LLVM as a backend. This means that S++ is able to achieve the
  performance of C++ and Rust.

- **Readability**: S++ was designed with readability in mind. Whilst being loosely inspired by the C-family syntax, a
  number of changes were made with regard to keywords and tokens, and removing legacy syntax. This includes keeping
  keywords of the same "group" the same length, and ensuring a top-to-bottom and left-to-right reading rule for every
  block of code.

- **Orthogonal**: S++ is designed to be an orthogonal language, where functions, arrays, tuples and any other types that
  would usually be treated specially as "primitive" types are all treated as first-class objects, with types such
  as `Arr[T]`, `Tup[..Ts]` and `FunMov/Ref/Mut[Ret, ..Args]`. This enforces consistency and prevents any unintended
  interactions between different features, especially when using these types as generic arguments.

- **Versatile**: S++ is designed to be a versatile language, with a focus on being able to be used for any purpose.
  This is achieved by having a number of different paradigms, including object-oriented, functional, and procedural
  programming.

- **Efficient**: S++ is designed to be both efficient for the user to program in, and efficient for the machine to
  execute. This is achieved by stripping out legacy features in other languages, and forcing type inference to reduce
  how much the user has to type.

- **Safety** S++ is designed to be a safe language, by using second-class borrows, enforcing the law of exclusivity, and
  tracking ownership throughout blocks. Using these three techniques together ensures safety in every aspect of the
  language, without having to use lifetime analysis or a reference counting.

## Language Features

#### Syntax & Semantics

- Braces as block delimiters.
- No semicolons at the end of lines.
- One branching, looping, and contextual block type.
- Isolated scopes and variable shadowing.

#### Types

- Strong, static, affine type system.
- Powerful type inference (type + value not allowed)
- Arrays, functions, tuples etc. are first-class types.
- No implicit type casting under any circumstance.

#### Safety

- Second-class borrowing system.
- Law of exclusivity.
- Ownership tracking.

#### Functional programming

- First-class functions (`FunMov`, `FunRef`, `FunMut`)
- Lambdas with explicit variable capturing.
- Variable declarations default to immutable.

#### Object oriented programming

- Separate state and behaviour of classes.
- Superimposition-based type inheritance.
- Encapsulation with annotations
- Method overloading and overriding.

#### Async/Concurrency/Parallelism

- Asynchronous functions without the colour problem.
- Coroutines that act like Python generators.
- Threading primitives.

#### Exceptions

- The monadic `Ret[T, E]` type is used (like Rust's `Result`)
- Shorthand `?` operator to propagate errors out the function.

#### Other

- Generics & constraints for functions, classes, sups.
- Advanced pattern matching.
- Simple module system with matching namespacing.

## Notes
- S++ is not backwards compatible between major versions.
