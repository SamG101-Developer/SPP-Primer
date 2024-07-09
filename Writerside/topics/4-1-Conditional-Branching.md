# 4.1. Conditional Branching

S++ re-invents "condition branching" by combining a standard "if", "match/switch" and "ternary" expression all into one
structure. This improves the simplicity of the language and provides one way to do conditional branching. The branching
expression is named the `case` expression, and uses the `then` keyword to separate the condition from the patterns.

## How to use the "case" expression

### Patterns

#### Basic

```
case person then
    == john { "hello john" }
    == jane { "hello jane" }
else { "hello stranger" }
```

#### Different condition operators

```
case age then
    <  0 { "error" }
    == 0 { "newborn" }
    <  18 { "child" }
    <  60 { "adult" }
else { "senior" }
```

#### Ternary

```
let x = case person then ==  john { "hello john" } else { "hello stranger" }
```

#### Pattern matching (struct, tuple)

```
case person then
    == Person(name="john", ..) { "hello john" }
    == Person(name="jane", ..) { "hello jane" }
else { "hello stranger" }
```

```
case tuple then
    == (1, 2) { "tuple is (1, 2)" }
    == (3, 4) { "tuple is (3, 4)" }
else { "tuple is something else" }
```

#### Binding (struct, tuple)

```
case person then
    == Person (name="john", age, ..) { "hello john, you are ${age} years old" }
    == Person (name="jane", age, ..) { "hello jane, you are ${age} years old" }
else { "hello stranger" }
```

```
case tuple then
    == (a, 1) { "tuple is ($a, 1)" }
    == (b, 2) { "tuple is ($b, 2)" }
else { "tuple is something else" }
```

#### Partial conditions

```
case person == then
    Person(name="john", ..) { "hello john" }
    Person(name="jane", ..) { "hello jane" }
else { "hello stranger" }
```

#### Guards

```
case person then
    == Person(name="john", age, ..) and age > 18 { "hello john, you are ${age} years old" }
    == Person(name="jane", age, ..) and age > 18 { "hello jane, you are ${age} years old" }
else { "hello stranger" }
```

#### Multiple conditions

```
case person then
    == john, jane { "hello john or jane" }
    == jack, jill { "hello jack or jill" }
else { "hello stranger" }
```

#### Unrelated conditions

```
case true == then
    func1().attribute1 > 4 { "func1 returned true" }
    func2().attribute2 < 5 { "func2 returned true" }
else { "both returned false" }
```
