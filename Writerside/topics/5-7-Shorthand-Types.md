# 5.7. Shorthand Types

There are 5 non-function types that have shorthand syntax in S++:

| Full Type       | Shorthand Notation | Example      |
|-----------------|--------------------|--------------|
| `std.Opt[T]`    | `?`                | `Str?`       |
| `std.Var[..Ts]` | `                  | `            | `Str | Int` |
| `std.Tup[..Ts]` | `()`               | `(Str, Int)` |
| `std.Arr[T]`    | `[]`               | `[Str]`      |

There are no shorthand types for the 3 function types, because there isn't an intuitive way to have a massively shorter
version of the function type, whilst retaining the type of the function, with `FnMut` being the hardest, as `&mut` is 4
characters long:

- `FnMut[Void, (Str, Str)]`
- `(&mut, Str, Str) -> Void`
- `&mut(Str, Str) -> Void`
