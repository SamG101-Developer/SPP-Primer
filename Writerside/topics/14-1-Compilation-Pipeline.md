# 14.1. Compilation Pipeline

The S++ Compiler is a multi-stage compiler that compiles S++ code into LLVM IR. The compilation pipeline is as follows:

1. Lexical Analysis (tokenization)
2. Syntactic Analysis (parsing)
3. Preprocessing (maps functions to `sup Fun___ on ...` etc.)
4. Symbol Generation (for functions, classes, etc.)
5. Semantic Analysis + Type Inference
6. Code Generation (LLVM IR)
7. LLVM IR -> Object File -> Executable

Stages 3, 4 and 5 are all under "Semantic Analysis" in the compiler source code, because they all apply to the ASTs 
post-parsing. While the "Symbol Generation" stage could be omitted and merged into "Semantic Analysis", performing 
the generation as a pre-pass allows the order of definitions not to matter, which is a nice feature. This means 
forward declarations are not necessary, allowing for cleaner code.
