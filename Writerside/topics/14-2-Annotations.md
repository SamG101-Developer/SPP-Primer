# 14.2. Annotations

Annotations can be applied over classes, functions and attributes. They allow code to be injected at the token level,
and can be used for a variety of purposes, such as simplifying stateless superimposition. Annotations are applied by
using the `@` symbol, followed by the annotation name, and then the arguments in parentheses. The arguments are
separated by commas, and can be any expression.

```
cls A {
    a: U32
    b: U32
}

sup Copy on A { }

sup Eq on A { }
```

becomes

```
@superimpose([Copy, Eq])
cls A {
    a: U32
    b: U32
}
```

## Annotation helpers

There are a number of methods that can be called that traverse the token stream, making it easier for common operations
to be applied. For example, when annotating a class, the `quote::current_type` method can be used to get the current
type being annotated.

## Creating annotations

To create an annotation, a method must be defined that accepts a token stream, and returns a modified token stream. The
annotation method can be used to modify the token stream in any way, such as adding or removing tokens, or changing the
order of tokens.

A method being used as an annotation must be marked with the `@annotation` annotation, otherwise it cannot be used as an
annotation. This isn't technically required for the compiler to apply the annotation, but it is required as a design
decision, to make it clear that the method is an annotation.

```
@annotation
fun superimpose(tokens: &mut Vec[Token], types: Vec[Str]) -> Void {
    # Modify the token stream here
    # Add "sup ... on ..." blocks
    
    let current_type = quote::current_type(tokens)
    types.for_each((type: Str) -> Void {
        let superimpose = "sup " + type + " on " + current_type + " { }"
        let tokens = quote::lex(superimpose)
        tokens.emplace_tail(tokens)
    })
}
```
