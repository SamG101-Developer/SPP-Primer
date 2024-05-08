# 5.2. Type Inference & Declarations

Every expression can be type-inferred. This means that type declarations on local variables are never needed, 
because it adds extra noise and provides no additional information. Because of this, the design decision to 
syntactically emit type declarations from initialized local variables was implemented.

Type declarations are needed in places where inference is not possible. This includes and is limited to:
- Function parameters, so that function overloading can be done based on types.
- Function return type. This was a design decision to make functions clearer to read.
- Attribute types, so that the compiler can allocate the correct amount of memory for the attribute and class.
- Uninitialized variables, because they don't start with any value, so can't be inferred.

All type declarations are done by adding `: [Type]` after the identifier. This is the same as Rust. The only 
exception to using `: [Type]` is the function return type, which uses the `-> [Type]` syntax. This is to keep lambda 
syntax clean and clear, and because the lambda syntax mirrors the function syntax, the `->` is used for functions too.

| Statement          | Legal? | Description                                                      |
|--------------------|--------|------------------------------------------------------------------|
| `let a = "5"`      | Yes    | Type is inferred to be `Str`                                     |
| `let a: Str`       | Yes    | Type is explicitly declared to be `Str` with **no value**        |
| `let a: Str = "5"` | No     | Type is already inferred, so explicit declaration is not allowed |
