# 3.2. Expressions & Operators

## Expressions
### 

## Operators
S++ has a large number of operators, which allow for increased readability and minimalism in code. There are binary 
operators, postfix operators, but no unary operators (with one minor exception mentioned later).

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

#### Binary comparison operator chaining
In S++, comparison operators can be chained, simplifying code. For example, `1 < 2 < 3` is equivalent to `(1 < 2) && 
(2 < 3)`. This feature is taken from Python, and is beneficial in simplifying code and improving readability. The 
comparison operators that can be chained are: `==`, `!=`, `>`, `<`, `>=`, `<=`. Note that `<=>` and `is` are not 
included, despite being usable for comparison.

#### Binary operator overloading
Operator overloading works similarly to in Rust, where the operator is a function. Classes have generic parameters 
so that the `RHS` and `Out` types can be specified (but default to `Self`), and unique overloads per types being 
operated on can be created. For example, to make a `Vec3D` class add-able to itself, and return another `Vec3D`, the 
`std.ops.Add[Rhs=Vec3D, Out=Vec3D]` class must be superimposed on the type:
```s++
cls Vec3D {
    x: F64;
    z: F64;
    y: F64;
}

sup Add on Vec3D {
    fun add(self, that: Self) -> Self {
        ret Vec3D(x=self.x + that.x, y=self.y + that.y, z=self.z + that.z);
    }
}
```

### Postfix operators
There are 3 postfix operators in S++:

| Postfix Operator | Name                   | Description                                                                               |
|------------------|------------------------|-------------------------------------------------------------------------------------------|
| `(...)`          | `FunMov` function call | Consume the environment of a function, and call it with the specified arguments.          |
| `(...)`          | `FunRef` function call | Immutably borrow the environment of a function, and call it with the specified arguments. |
| `(...)`          | `FunMut` function call | Mutably borrow the environment of a function, and call it with the specified arguments.   |
| `{...}`          | Object instantiation   | Instantiate an object, setting attribute and super-class values to the specified values.  |
| `.`              | Member access          | Access a member of an object.                                                             |
| `?`              | Early return           | If the expression is residual and in the fail state, return the wrapped fail value.       |

#### Postfix operator overloading
The only postfix operators that can be overloaded are the `Fun[Ref|Mut|Mov]` function call operators. These are 
overloaded in the same way as binary operators, but the methods have different signatures. The following example 
shows how to make a `Vec3D` class callable with a certain signature:
```s++
cls Vec3D {
    x: F64;
    z: F64;
    y: F64;
}

sup FunMut[Void, (Str, Str, Str)] on Vec3D {
    fun call_ref(&mut self, x: Str, y: Str, z: Str) -> Void {
        self.x = F64.from(x);
        self.y = F64.from(y);
        self.z = F64.from(z);
    }
}

fun main() -> Void {
    let v = Vec3D(x=0.0, y=0.0, z=0.0);
    v("1.0", "2.0", "3.0");
    std.assert(v.x == 1.0);
}
```

### Unary operators
There are no unary operators like `!`, `--`, `++` etc. Instead, methods are preferred as they are a lot more 
readable. For example, `loop !some_expression().value.is_some() { ... }` is a lot less readable than `loop
some_expression().value.is_some().not() { ... }`. This also encourages the left-to-right reading of expressions too. 
There is the case where [asynchronous function calls]() are made with `async <expr>`, but this isn't an operator.