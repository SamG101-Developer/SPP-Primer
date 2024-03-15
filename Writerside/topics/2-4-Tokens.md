# 2.4. Tokens

| Token   | Primary Use                              | Secondary Use                   | Tertiary Use                          |
|---------|------------------------------------------|---------------------------------|---------------------------------------|
| `&&`    | Logical AND                              | Pattern guard                   |                                       |
| `&&=`   | Logical AND Assignment                   |                                 |                                       |
| `\|\|`  | Logical OR                               |                                 |                                       |
| `\|\|=` | Logical OR Assignment                    |                                 |                                       |
| `&`     | Bitwise AND                              | Borrowing a value               | Intersection Types (Constraints)      |
| `&=`    | Bitwise AND Assignment                   |                                 |                                       |
| `\|`    | Bitwise OR                               | Multiple patterns               | Union Types                           |
| `\|=`   | Bitwise OR Assignment                    |                                 |                                       |
| `^`     | Bitwise XOR                              |                                 |                                       |
| `^=`    | Bitwise XOR Assignment                   |                                 |                                       |
| `<<`    | Bitwise Left Shift                       |                                 |                                       |
| `<<=`   | Bitwise Left Shift Assignment            |                                 |                                       |
| `>>`    | Bitwise Right Shift                      |                                 |                                       |
| `>>=`   | Bitwise Right Shift Assignment           |                                 |                                       |
| `<<<`   | Bitwise Left Rotate                      |                                 |                                       |
| `<<<=`  | Bitwise Left Rotate Assignment           |                                 |                                       |
| `>>>`   | Bitwise Right Rotate                     |                                 |                                       |
| `>>>=`  | Bitwise Right Rotate Assignment          |                                 |                                       |
| `==`    | Equality                                 |                                 |                                       |
| `!=`    | Inequality                               |                                 |                                       |
| `>`     | Greater Than                             |                                 |                                       |
| `>=`    | Greater Than or Equal                    |                                 |                                       |
| `<`     | Less Than                                |                                 |                                       |
| `<=`    | Less Than or Equal                       |                                 |                                       |
| `<=>`   | Comparison                               |                                 |                                       |
| `+`     | Addition                                 | Positive number literal         |                                       |
| `+=`    | Addition Assignment                      |                                 |                                       |
| `-`     | Subtraction                              | Negative number literal         |                                       |
| `-=`    | Subtraction Assignment                   |                                 |                                       |
| `*`     | Multiplication                           | Reduce all from a namespace     |                                       |
| `*=`    | Multiplication Assignment                |                                 |                                       |
| `/`     | Division                                 |                                 |                                       |
| `/=`    | Division Assignment                      |                                 |                                       |
| `%`     | Remainder                                |                                 |                                       |
| `%=`    | Remainder Assignment                     |                                 |                                       |
| `%%`    | Modulo                                   |                                 |                                       |
| `%%=`   | Modulo Assignment                        |                                 |                                       |
| `**`    | Exponentiation                           |                                 |                                       |
| `**=`   | Exponentiation Assignment                |                                 |                                       |
| `()`    | Grouping Expressions                     |                                 |                                       |
| `[]`    | Grouping Generic Params/Args/Constraints | Grouping Lambda Captures        | Array Literal                         |
| `{}`    | Grouping Blocks                          |                                 |                                       |
| `??`    | Null Coalescing                          |                                 |                                       |
| `?`     | Early Return                             |                                 |                                       |
| `..`    | Variadic parameters                      | Unpacking/Destructuring/Folding | Skip Rest of Arguments in Destructure |
| `.`     | Runtime Member Access                    | Namespace Access                |                                       |
| `:`     | Type Annotation / Constraints            |                                 |                                       |
| `,`     | Separator                                |                                 |                                       |
| `=`     | Assignment                               |                                 |                                       |
| `->`    | Function Return Type                     |                                 |                                       |
| `@`     | Annotation                               |                                 |                                       |
| `_`     | Placeholder                              |                                 |                                       |