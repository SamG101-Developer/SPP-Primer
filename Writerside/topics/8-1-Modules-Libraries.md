# 8.1. Modules & Libraries

## Modules
In S++, the directory structure of the project defines the module structure, which in turn defined the namespace
structure: they are all the same. This heavily simplifies the process of importing modules, as the module name reflects
namespacing too.

All modules are accessible via the global namespace by default, like in Rust, but specific types from a namespace can be
aliased into the global namespace using the `use` keyword, like `use some.module.{X as Type1, Y as Type2}`.

### Entry point
A `main.spp` file is required in the root of the `src` directory. This is the entry module of the program. The `main`
file must contain a `fun main() -> Void` function, which is the entry point of the program. This function is called
automatically when the program is run.
