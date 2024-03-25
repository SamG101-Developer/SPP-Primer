# 14.1. Compilation Pipeline

The S++ Compiler is a multi-stage compiler that compiles S++ code into LLVM IR. The compilation pipeline is as follows:

1. Lexical Analysis (tokenization)
2. Syntactic Analysis (parsing)
3. Pre-Semantic Analysis
    1. Preprocessing (maps functions to `sup Fun___ on ...` etc.)
    2. Symbol Generation (for functions, classes, etc.)
4. Semantic Analysis
5. Code Generation (LLVM IR)
6. LLVM IR -> Object File -> Executable

Stages 3, 4 and 5 are all under "Semantic Analysis" in the compiler source code, because they all apply to the ASTs
post-parsing. While the "Symbol Generation" stage could be omitted and merged into "Semantic Analysis", performing
the generation as a pre-pass allows the order of definitions not to matter, which is a nice feature. This means
forward declarations are not necessary, allowing for cleaner code.

Preprocessing is an important stage of the compilation process, as by splitting the semantic analysis into three stages,
a number of currently seen inconveniences are avoided. For example, the order of function and class declarations don't
matter and circular imports are allowed.

## Lexical Analysis

Lexical analysis takes the string of characters that make up the source code and converts them into tokens. Tokens are
matched directly against operators and keywords, and by regex for the lexemes.

## Syntactic Analysis

Syntactic analysis takes the tokens and converts them into an Abstract Syntax Tree (AST). The parser is very flexible,
allowing easy changes to future editions of the language. The ASTs are then passed to the preprocessor.

## Pre-Semantic Analysis

In the preprocessing stage of pre-semantic analysis, two major things happen: The `self` types are substituted for the
actual types they represent, and functions are converted to classes with `Fun[Ref|Mut|Mov]` superimposed over them.

The `self` substitution can be done in either the preprocessing or generation stage, as long as it is done before
semantic analysis. This is because, for the same reason as symbol generation, it allows for order of declarations to not
matter.

Function conversion allows for functions to be first class objects by not creating a special symbol construct
for them. Also, as callable objects can be created by superimposing a `Fun___` class over a function, it makes sense to
treat normal functions like this, creating one way to call functions.

```s++
fun function(a: Str, b: Str) -> Str {
    ret a + b
}

fun function(a: U64, b: U64) -> U64 {
    ret a + b
}
```

```s++
cls MOCK_function { }

sup FunRef[Str, (Str, Str)] on MOCK_function {
    fun call(self, a: Str, b: Str) -> Str {
        ret a + b
    }
}

sup FunRef[U64, (U64, U64)] on MOCK_function {
    fun call(self, a: U64, b: U64) -> U64 {
        ret a + b
    }
}

let function = MOCK_function();
```

In the generation stage, the ASTs are passed to the symbol generator, which creates stage 1 symbols; these are for top
level constructs, including classes, functions, global constants, sup-blocks and their methods, and typedefs. Scopes are
also generated at this stage.

## Semantic Analysis

Semantic analysis analyses the semantics of every AST in the tree. This includes type checking, memory checking,
variables existing, and a number of other checks. All the checks can be seen in the `.do_semantic_analysis()` methods of
the ASTs. Type inference is used heavily at this stage too.

## Code Generation

Code generation takes the ASTs and generates LLVM IR. This is done by traversing the ASTs and generating the IR for each
node. No additional checks are done at this stage, as semantic analysis will have picked them up, and any additional
checks here can be done in the semantic analysis stage.

## LLVM IR -> Object File -> Executable

The LLVM IR is then passed to the LLVM compiler, which generates an object file.
