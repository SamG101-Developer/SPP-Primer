# 4.2. Conditional Branching

S++ re-invents "condition branching" by combining a standard "if", "match" and "ternary" expression all into 1 
structure. This improves the simplicity of the language and provides 1 way to do all conditional branching. The 
branching expression is named the "case" expression.

### How to use the "case" expression
#### Basic
```s++
case person then
    == john { "hello john" }
    == jane { "hello jane" }
else { "hello stranger" }
```

#### Different condition operators
```s++
case age then
    <  0 { "error" }
    == 0 { "newborn" }
    <  18 { "child" }
    <  60 { "adult" }
else { "senior" }
```

#### Ternary
```s++
let x = case person then ==  john { "hello john" } else { "hello stranger" }
```

#### Pattern matching (struct, tuple)
```s++
case person then
    == Person(name="john", ..) { "hello john" }
    == Person(name="jane", ..) { "hello jane" }
else { "hello stranger" }
```
```s++
case tuple then
    == (1, 2) { "tuple is (1, 2)" }
    == (3, 4) { "tuple is (3, 4)" }
else { "tuple is something else" }
```

#### Binding (struct, tuple)
```s++
case person then
    == Person { name="john", age, .. } { "hello john, you are ${age} years old" }
    == Person { name="jane", age, .. } { "hello jane, you are ${age} years old" }
else { "hello stranger" }
```
```s++
case tuple then
    == (a, 1) { "tuple is ($a, 1)" }
    == (b, 2) { "tuple is ($b, 2)" }
else { "tuple is something else" }
```

#### Partial conditions
```s++
case person == then
    Person(name="john", ..) { "hello john" }
    Person(name="jane", ..) { "hello jane" }
else { "hello stranger" }
```

#### Guards
```s++
case person then
    == Person(name="john", age, ..) && age > 18 { "hello john, you are ${age} years old" }
    == Person(name="jane", age, ..) && age > 18 { "hello jane, you are ${age} years old" }
else { "hello stranger" }
```

#### Multiple conditions
```s++
case person then
    == john | jane { "hello john or jane" }
    == jack | jill { "hello jack or jill" }
else { "hello stranger" }
```

#### Unrelated conditions
```s++
case true == then
    func1().attribute1 > 4 { "func1 returned true" }
    func2().attribute2 < 5 { "func2 returned true" }
else { "both returned false" }
```
