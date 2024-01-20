# 5.2. Primitive Types

In S++, there are no primitive types. All types are first-class, and can be used as types for variables, attributes
and parameters etc. This allows the language to remain orthogonal, and prevents any unintended interactions between
different features.

There are some types in S++ that _mock_ primitive types, and connect to LLVM types, allowing for the compiler to
generate efficient code. These types are as follows:

## Numeric types
The numeric types in S++ have 3 different classes of types: unsigned integers, signed integers, and floating point.
All of these allow from `8` to `256` bits, allowing for micro optimization of memory usage. None of these types are
instantiable, directly -- use the [numeric postfix literals]() to create instances of these types. The types are as
follows:

### Numeric type classes:
#### Unsigned Integers

| Type   | Size (bits) | Min | Max     | Precision | Description              |
|--------|-------------|-----|---------|-----------|--------------------------|
| `U8`   | 8           | 0   | 2^8 - 1 | 8 bits    | Unsigned 8-bit integer   |
| `U16`  | 16          | 0   | 2^16- 1 | 16 bits   | Unsigned 16-bit integer  |
| `U32`  | 32          | 0   | 2^32- 1 | 32 bits   | Unsigned 32-bit integer  |
| `U64`  | 64          | 0   | 2^64- 1 | 64 bits   | Unsigned 64-bit integer  |
| `U128` | 128         | 0   | 2^128-1 | 128 bits  | Unsigned 128-bit integer |
| `U256` | 256         | 0   | 2^256-1 | 256 bits  | Unsigned 256-bit integer |

#### Signed Integers

| Type   | Size (bits) | Min    | Max      | Precision | Description            |
|--------|-------------|--------|----------|-----------|------------------------|
| `I8`   | 8           | -2^7   | 2^7 - 1  | 7 bits    | Signed 8-bit integer   |
| `I16`  | 16          | -2^15  | 2^15 - 1 | 15 bits   | Signed 16-bit integer  |
| `I32`  | 32          | -2^31  | 2^31 - 1 | 31 bits   | Signed 32-bit integer  |
| `I64`  | 64          | -2^63  | 2^63 - 1 | 63 bits   | Signed 64-bit integer  |
| `I128` | 128         | -2^127 | 2^127-1  | 127 bits  | Signed 128-bit integer |
| `I256` | 256         | -2^255 | 2^255-1  | 255 bits  | Signed 256-bit integer |

#### Floating Point Numbers

| Type   | Size (bits) | Min    | Max      | Precision | Description          |
|--------|-------------|--------|----------|-----------|----------------------|
| `F8`   | 8           | -2^7   | 2^7 - 1  | 7 bits    | Signed 8-bit float   |
| `F16`  | 16          | -2^15  | 2^15 - 1 | 15 bits   | Signed 16-bit float  |
| `F32`  | 32          | -2^31  | 2^31 - 1 | 31 bits   | Signed 32-bit float  |
| `F64`  | 64          | -2^63  | 2^63 - 1 | 63 bits   | Signed 64-bit float  |
| `F128` | 128         | -2^127 | 2^127-1  | 127 bits  | Signed 128-bit float |
| `F256` | 256         | -2^255 | 2^255-1  | 255 bits  | Signed 256-bit float |

### Instantiating numeric types
Numeric literals allow for type postfixes to be used to specify the type of the literal. The postfixes follow the
regex `_[U|I|F][8|16|32|64|128|256]`, where the first character is the type class, and the second character is the
size of the type. For example, `1_U8` is an unsigned 8-bit integer, and `1_I64` is a signed 64-bit integer. If no
literal is used, the smallest numeric type **is not used**, instead either [`BigNum`]() or [`BigDec`]() is used.

## Boolean type
The `Bool` type is the boolean type in S++, which certain expressions must evaluate to, for example in `loop`
expression conditions, or `case` expression conditions (when applied to with patterns). The `Bool` type has 2 values:
`true` and `false` -- the `Bool` type itself isn't instantiable.

The `true` and `false` types are program-long and constant, meaning that they are not stored in memory, and are
instead directly encoded into the instructions that use them. Semantically, they work as if [`Copy`]() has been
[superimposed]() on them. The `Bool` type is mapped to the LLVM `bool` type.

## Void type
The `Void` is the only type that has no instances. This is because it is a "nothing" type, and can not be used for 
variables or attributes. It represents the absence of a value, and is used as the return type of functions that 
don't return a value. A `Void` parameter doesn't take a value; this is needed for when a generic argument is `Void`, 
and the corresponding generic parameter is used as a parameter type.
