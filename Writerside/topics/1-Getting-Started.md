# 1. Getting Started

#### Origins & History

S++ is a new programming language designed to be a modern, safe, and fast systems programming language, with
a focus on performance and readability. It has a strong type system, and an ownership model based on second-class
borrows, the Law of Exclusivity, and ownership tracking, allowing for safe programming without a garbage collector.

There are concepts from other languages, (Rust, C++, Python, Go, Java) that flow through S++, as well as some features
not found in other languages. The safety mechanisms are inspired by Rust, but with second-class borrows, meaning that
lifetime analysis is not required for safe programming. Rust also inspires the type system, but with a new way to
inherit types - superimposition. The type inference is so strong that it is syntactically disallowed to specify types
for initialized variable declarations. The general language syntax is inspired by the C family of languages, but with a
focus on consistency, readability and orthogonality, meaning that there are several "normalizations" that remove special
cases and quirks found in C++/Rust. There are a number of keywords not found in other languages, but with the core of
the keywords being a mix of Rust and Python.

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
  to reduce how much the user has to type. Also, only the stack is ever used for memory allocation, meaning that
  memory leaks are impossible.

- **Safety** S++ is designed to be a safe language, by using second-class borrows, enforcing the law of exclusivity, and
  tracking ownership through blocks. These thee features combined allow for safe programming, without complex lifetime
  analysis or the use of a garbage collector.

#### Language Features

- Strong, static, affine type system
- Strong type inference
- All types are 1st-class objects
- Safe memory management
- Superimposition-based type inheritance
- Generics & constraints
- Advanced pattern matching
- Zero-cost abstractions
