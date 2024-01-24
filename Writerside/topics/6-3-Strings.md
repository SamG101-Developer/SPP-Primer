# 6.3. Strings

In S++, there is only 1 string type, `Str`. This is a lot simpler that having Rust's `String` and `&str` types, or 
C++'s `std::string`, `std::string_view` and `const char*` types, etc.

The `Str` type contains an optional generic parameter, `Backend`, which defaults to
`std.str_backend.VectorStringBackend`. The `Backend` generic type is the underlying construct used to store the 
string's data. This can be things like a vector string or a rope string etc. The methods on the `Str` class abstract 
over the backend by calling certain functions that are required to be implemented by the backend.

## String literals
The string literal syntax is `"<string>"`. There is not other way to create strings, except for `Str.new()` which is 
equivalent to `""`.

## Char literal
There is no char literal in S++, because either the `[I|U]8` type can be used, or a 1-character string literal can be
used. This means that the `'` is not used for anything.
