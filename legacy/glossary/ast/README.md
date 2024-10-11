# Abstract Syntax Tree

An AST, or just _Syntax Tree_, is a tree representation of the abstract syntactic structure of source code written in a programming language. Each node of the tree denotes a construct occurring in the source code.

The syntax is "abstract" in the sense that it does not represet every detail appearing in the real syntax, but rather just the structural or content-related details. For instance, grouping parentheses are implicit in the tree structure, so these do not have to be represented as separate nodes. Likewise, a syntactic construct like an if-condition-then expression may be denoted by means of a single node with three branches.

This distinguishes AST from _Concrete Syntax Trees_, traditionally designated _Parse Trees_, which are typically built by a parser during the source code translation and compiling process. Once built, additional information is added to the AST by means of subsequent processing, e.g., contextual analysis.

AST are also used in program analysis and program transformation systems.

## Usage in compilers

AST are data structures widely used in compilers to represent the structure of program code. An AST is usually the result of the _syntax analysis_ phase of a compiler. It often serves as an intermediate representation of the program through several stages that the compiler requires, and has a strong impact on the final output of the compiler.

The AST is used intesively during _semantic analysis_, where the compiler checks for correct usage of the elements of the program and the language. The compiler also generates _symbol tables_ based on the AST during semantic analysis. A complete traversal of the tree allows verification of the correctness of the program.

After verifying correctness, the AST serves as the base for code generation. The AST is often used to generate an _intermediate representation_ (IR), sometimes called an _intermediate language_, for the code generation.
