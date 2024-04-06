# 6.3. Strings

In S++, there is only 1 string type, `Str`. This is a lot simpler that having Rust's `String` and `&str` types, or
C++'s `std::string`, `std::string_view` and `const char*` types, etc.

The `Str` type contains an optional generic parameter, `Backend`, which defaults to
`std.str_backend.VectorStringBackend`. The `Backend` generic type is the underlying construct used to store and
manipulate the
string's data, such as a vector-string or a rope-string etc. These backend classes provide the core functionality of
string manipulation, such as creating substrings or replacing parts of the string etc. The methods on the `Str` class
abstract over the backend by calling certain functions that are required to be implemented by the backend.

## String literals

The string literal syntax is `"<string>"`. This is the only way to create a string, because the initializer for the
`Str` class would need a string, which would be given as "...", rendering the string constructor obsolete.

## Char literal

There is no char literal in S++, because either the `[I|U]8` type can be used, or a 1-character string literal can be
used. This means that the `'` token is not used for anything.

## String backends
- `std.str_backend.VectorStringBackend`
- `std.str_backend.RopeStringBackend`
- TODO
