# 1. Getting Started

#### Origins & History

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
languages, but with all the unnecessary and non-orthogonal parts removed, forcing a consistent and readable syntax.

#### Language Philosophy & Core Principles

- **Performance**: S++ is designed to be a high-performance language, with a focus on runtime performance. This is
  achieved by compiling S++ to native code, using LLVM as a backend. This means that S++ is able to achieve the
  performance of C++ and Rust.

- **Readability**: S++ is designed to be a readable language, achieving this by using a simple syntax inspired from
  the C family of languages, but with a number of unnecessary parts of the syntax removed. All code follows the
  left-to-right reading rule, so to understand a line of code, you never have to look ahead.

- **Orthogonal**: S++ is designed to be an orthogonal language, where functions, arrays, and other usually primitive
  types are all treated as first-class types, meaning there are no unintended interactions between different features.

- **Versatile**: S++ is designed to be a versatile language, with a focus on being able to be used for any purpose.
  This is achieved by having a number of different paradigms, including OOP, FP, and procedural programming, as well
  as having a number of different features, including generics, closures, and first-class functions.

- **Efficient**: S++ is designed to be an efficient language, both efficient for the user to program in, and
  efficient for the computer to execute. This is achieved by removing unnecessary features, and forcing type inference,
  to reduce how much the user has to type.

- **Safety** S++ is designed to be a safe language, by using second-class borrows, enforcing the law of exclusivity, and
  tracking ownership through blocks. These three features combined allow for safe programming, without complex lifetime
  analysis or the use of a garbage collector.

#### Language Features

- Strong, static, affine type system
- Powerful type inference
- All types are 1st-class objects (arrays, tuples, functions, etc.)
- Safe memory management without garbage collection
- Superimposition-based type inheritance
- Generics & constraints
- Advanced pattern matching
- Zero-cost abstractions
