# 2.4. Tokens

`{}`

- Define a new scope (`case`, `loop`, `with`, `else`, `cls`, `sup`, `fun`, `use` or unnamed).

`[]`

- Define a generic argument/parameter list.
- Define constraints on a generic parameter in a `where` clause.
- Capture lambda arguments.
- Create an array literal.

`()`

- Define a function argument/parameter list.
- Define a class instantiation argument list.
- Define a parenthesised expression.
- Define a tuple literal.
- De-structure a tuple or a struct.

`:`

- Introduce a type annotation (attribute, parameter, constraint, uninitialized variable).

`_`

- Skip single values in a de-structure operation.
- Shorthand a partial function application.

`..`

- Define a variadic parameter in a function signature.
- Define variadic generic parameters.
- Unpack a tuple argument into multiple parameters.
- Define a binary or function folding operation.
- Bind multiple elements from a tuple into a single variable.
- Skip the rest of the arguments in a de-structure operation.

`?`

- Perform an early return for a residual type in a function.

`.`

- Used when defining a module name.
- Access a member of a namespace or object.

`->`

- Define a function return type.
- Define a lambda return type.

`@`

- Define an annotation (module, function, class, superimposition or sup-typedef)

`+`

- Define a positive number literal.
- Define a binary addition operation.

`-`

- Define a negative number literal.
- Define a binary subtraction operation.

`*`

- Define a binary multiplication operation.
- Import all types from a module.

`**`

- Define a binary exponentiation operation.

`/`

- Define a binary division operation.

`%`

- Define a binary remainder operation.

`%%`

- Define a binary modulo operation.

`&`

- Define a binary bitwise AND operation.
- Define a borrowing operation.
- Combine multiple constraints for a generic parameter.

`|`

- Define a binary bitwise OR operation.
- Define multiple patterns in a `case` expression.
- Define a union type.

`^`

- Define a binary bitwise XOR operation.

`&&`

- Define a logical AND operation.
- Define a pattern guard in a `case` expression.

`||`

- Define a logical OR operation.

`<<`

- Define a binary bitwise left shift operation.

`>>`

- Define a binary bitwise right shift operation.

`<<<`

- Define a binary bitwise left rotate operation.

`>>>`

- Define a binary bitwise right rotate operation.

`<=>`

- Define a comparison operation.

`==`

- Define an equality operation.

`!=`

- Define an inequality operation.

`>`

- Define a greater than operation.

`>=`

- Define a greater than or equal operation.

`<`

- Define a less than operation.

`<=`

- Define a less than or equal operation.

`=`

- Define a named value-argument for a function call, class initialisation, or lambda capture item.
- Define a named type-argument for a generic type.
- Define a default value for an optional function or generic argument.
- Define an initialize variable.
- Define a binding operation in a de-structure expression.
- Define a binding operation for a `with` expression.
- Assign a value to an existing variable.

`+=`

- Define a binary addition assignment operation.

`-=`

- Define a binary subtraction assignment operation.

`*=`

- Define a binary multiplication assignment operation.

`**=`

- Define a binary exponentiation assignment operation.

`/=`

- Define a binary division assignment operation.

`%=`

- Define a binary remainder assignment operation.

`%%=`

- Define a binary modulo assignment operation.

`&=`

- Define a binary bitwise AND assignment operation.

`|=`

- Define a binary bitwise OR assignment operation.

`^=`

- Define a binary bitwise XOR assignment operation.

`&&=`

- Define a logical AND assignment operation.

`||=`

- Define a logical OR assignment operation.

`<<=`

- Define a binary bitwise left shift assignment operation.

`>>=`

- Define a binary bitwise right shift assignment operation.

`<<<=`

- Define a binary bitwise left rotate assignment operation.

`>>>=`

- Define a binary bitwise right rotate assignment operation.

`??`

- Define a null coalescing operation.

`,`
- Separate items in a list.
  - Function call arguments/parameters.
  - Generic type arguments/parameters.
  - Class instantiation arguments.
  - Generic types being constrained in a `where` clause.
  - Items included in a typedef.
  - Items included in a local variable destructuring.
  - Items being assigned to in a regular `=` assignment.
  - Items in a lambda capture list.
  - Items in a tuple type.
  - Items in a tuple literal.
  - Items in an array literal.
