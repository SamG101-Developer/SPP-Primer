# 6.4. Tuples

Tuples are first-class objects, like in Rust.

## Type Syntax

Tuples have a special type syntax, which is a comma-separated list of types surrounded by parentheses. For example, the
type `(Str, Bool)` is a tuple of a `Str` and a `Bool`. This is the same as in Rust. Tuple types map to the `std.Tup[Ts]`
class.

## Tuple Literals

| Number of Elements | Tuple Value | Tuple Type         | Mapped To                 |
|--------------------|-------------|--------------------|---------------------------|
| 0                  | `()`        | `()`               | `std.Tup[]`               |
| 1                  | `(1,)`      | `(BigNum)`         | `std.Tup[BigNum]`         |
| 2                  | `(1, 2)`    | `(BigNum, BigNum)` | `std.Tup[BigNum, BigNum]` |

## Tuple Operations

### Folding

Tuples allow for `folding`, an operation which merges all elements of a tuple into a single value, via a function. There
are 2 types of folding:

- [binary folding](#binary-folding)
- [function folding](#function-folding).

#### Binary folding

Binary folding allows for a tuple to be folded into a single value, via a binary function. The binary function is
continuously applied to the current value and the next element in the tuple, until the end of the tuple is reached. The
order of the operations (left binary fold or right binary fold) depends on the syntax used:

###### Left binary fold

```s++
fun main() -> Void {
    let tuple = (1, 2, 3, 4, 5)
    let sum = .. + tuple
    std.print(sum) // 15
}
```

###### Right binary fold

```s++
fun main() -> Void {
    let tuple = (1, 2, 3, 4, 5)
    let sum = tuple + ..
    std.print(sum) // 15
}
```

The `.. + tuple` and `tuple + ..` syntax are derived from the `C++`
[binary fold expressions](https://en.cppreference.com/w/cpp/language/fold).

#### Function folding

Function folding allows for tuples to be folded into a single values, via a function. The function is continuously
applied to the next elements in the tuples, and returns a tuple of all the values returned by the function. This
operation is called a `fold` because whilst this operation doesn't merge all the elements of a tuple into a single
value, it does fold all the items of the tuple into the function.

Multiple tuples can be in the folded function, as long as they have the same number of elements as each other, so that
the function is called that number of times, with no ambiguities. However, there could be a case where it is not desired
that one of the tuples be folded, and should be passed as a normal tuple argument. This is fine and doesn't affect the
folding implementation, because argument vs parameter type checking determines which tuples to fold:

- If the target parameter is a tuple, then the corresponding tuple argument won't be folded.
- If the target parameter is a string, and the corresponding parameter is a tuple of strings, then that tuple will be
  folded into the function call.

### Unpacking

Tuple unpacking allows for a tuple to be unpacked into multiple arguments within a function. This only calls the
function once, but passed the tuple as multiple arguments. This works in the same way as C++'s `std::apply` function.

```s++
fun function_1(x: (U8, U8, U8)) -> U8 {
    let (a, b, c) = x
    return a + b + c
}

fun function_2(x: U8, y: U8, z: U8) -> U8 {
    return x + y + z
}

fun main() -> Void {
    let tuple_1 = (1, 2, 3)
    let tuple_2 = (4, 5, 6)
    
    let result_1 = function_1(tuple1)    # Pass the tuple as 1 argument (normal)
    let result_2 = function_2(..tuple2)  # Pass the tuple as 3 arguments (unpacking)
}
```

### Destructuring

Tuple destructuring allows for a tuple to be de-structured into multiple variables. This is similar to tuple unpacking,
but instead of passing the tuple as multiple arguments, it assigns each element of the tuple to a variable. Placeholders
can be used to ignore elements of the tuple.

```s++
fun main() -> Void {
    let tuple = (1, 2, 3, 5)
    
    let (a, b, c, d) = tuple
    let (a, _, c, _) = tuple
    let (a, ..b, d)  = tuple
    let (a, .., d)   = tuple
}
```

### Indexing

Tuples can be indexed using the `.n` operator, where `n` is a number. This will mark the object as partially moved,
because it is the same as moving an attribute, only the attributes of tuples are numerically accessed.

#### Tuple value indexing

```s++
fun main() -> Void {
    let tuple = (1, 2, 3)
    
    let a = tuple.0
    let b = tuple.1
    let c = tuple.2
}
```

#### Tuple type indexing

```s++
fun main() -> Void {
    use (U8, U8, U8) as TupleType
    use TupleType.0 as TupleType0
    use TupleType.1 as TupleType1
    use TupleType.2 as TupleType2
}
```
