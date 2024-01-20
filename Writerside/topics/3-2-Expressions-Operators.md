# 3.2. Expressions &amp; Operators

## Expressions

## Operators
S++ has a large number of operators, which allow for increased readability and minimalism in code. There are binary 
operators, postfix operators, but no unary operators (with 1 minor exception mentioned later).

### Binary operators
| Operator | Name                            | Class                  | Precedence |
|----------|---------------------------------|------------------------|------------|
| `=`      | Assignment                      | `std.ops.Assign`       | 0          |
| `??=`    | Null coalescing assignment      | `N/A`                  | 0          |
| `\|\=`   | Logical OR assignment           | `std.ops.OrAssign`     | 0          |
| `&&=`    | Logical AND assignment          | `std.ops.AndAssign`    | 0          |
| `<<=`    | Bitwise left shift assignment   | `std.ops.BitShlAssign` | 0          |
| `>>=`    | Bitwise right shift assignment  | `std.ops.BitShrAssign` | 0          |
| `<<<=`   | Bitwise left rotate assignment  | `std.ops.BitRolAssign` | 0          |
| `>>>=`   | Bitwise right rotate assignment | `std.ops.BitRorAssign` | 0          |
| `+=`     | Addition assignment             | `std.ops.AddAssign`    | 0          |
| `-=`     | Subtraction assignment          | `std.ops.SubAssign`    | 0          |
| `\|=`    | Bitwise OR assignment           | `std.ops.BitOrAssign`  | 0          |
| `^=`     | Bitwise XOR assignment          | `std.ops.BitXorAssign` | 0          |
| `*=`     | Multiplication assignment       | `std.ops.MulAssign`    | 0          |
| `/=`     | Division assignment             | `std.ops.DivAssign`    | 0          |
| `%=`     | Remainder assignment            | `std.ops.RemAssign`    | 0          |
| `%%=`    | Modulo assignment               | `std.ops.ModAssign`    | 0          |
| `**=`    | Exponentiation assignment       | `std.ops.PowAssign`    | 0          |
| `&=`     | Bitwise AND assignment          | `std.ops.BitAndAssign` | 0          |
| `??`     | Null coalescing                 | `N/A`                  | 1          |
| `\|\`    | Logical OR                      | `std.ops.Or`           | 2          |
| `&&`     | Logical AND                     | `std.ops.And`          | 3          |
| `==`     | Equality                        | `std.ops.Eq`           | 4          |
| `!=`     | Inequality                      | `std.ops.Ne`           | 4          |
| `>`      | Greater than                    | `std.ops.Gt`           | 4          |
| `<`      | Less than                       | `std.ops.Lt`           | 4          |
| `>=`     | Greater than or equal to        | `std.ops.Ge`           | 4          |
| `<=`     | Less than or equal to           | `std.ops.Le`           | 4          |
| `<=>`    | Comparison                      | `std.ops.Cmp`          | 4          |
| `<<`     | Bitwise left shift              | `std.ops.BitShl`       | 5          |
| `>>`     | Bitwise right shift             | `std.ops.BitShr`       | 5          |
| `<<<`    | Bitwise left rotate             | `std.ops.BitRol`       | 5          |
| `>>>`    | Bitwise right rotate            | `std.ops.BitRor`       | 5          |
| `+`      | Addition                        | `std.ops.Add`          | 6          |
| `-`      | Subtraction                     | `std.ops.Sub`          | 6          |
| `\|`     | Bitwise OR                      | `std.ops.BitOr`        | 6          |
| `^`      | Bitwise XOR                     | `std.ops.BitXor`       | 6          |
| `*`      | Multiplication                  | `std.ops.Mul`          | 7          |
| `/`      | Division                        | `std.ops.Div`          | 7          |
| `%`      | Remainder                       | `std.ops.Rem`          | 7          |
| `%%`     | Modulo                          | `std.ops.Mod`          | 7          |
| `**`     | Exponentiation                  | `std.ops.Pow`          | 7          |
| `&`      | Bitwise AND                     | `std.ops.BitAnd`       | 7          |

The precedence of binary operators is a lot simpler than other languages, meaning there is less to remember. Both 
logical operators are short-circuiting too, optimizing code. All operators, except `**` are evaluated left-to-right, 
and the precedence issue found in C-derived languages, where `&` has a higher precedence than comparison operators, 
is fixed.
