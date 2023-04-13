[View code on GitHub](https://github.com/cosmos/cosmos-sdk/blob/main/depinject/internal/codegen/func.go)

The `FuncGen` struct and its associated methods are part of the `codegen` package in the `cosmos-sdk` project. This package is used for generating and patching Go code, and `FuncGen` specifically is a utility for working with function declaration abstract syntax trees (ASTs).

The `FuncGen` struct has two fields: a pointer to a `FileGen` struct and a pointer to an `ast.FuncDecl` struct. The `FileGen` struct is used to generate and patch Go source files, while the `ast.FuncDecl` struct represents a function declaration in the AST.

The `newFuncGen` function is a constructor for the `FuncGen` struct. It takes a `FileGen` pointer and an `ast.FuncDecl` pointer as arguments, and returns a new `FuncGen` pointer. This function initializes the `FuncGen` struct by setting its `FileGen` and `Func` fields to the provided arguments.

Additionally, `newFuncGen` reserves the identifiers for the function's parameters and results by iterating over the `Params` and `Results` fields of the `ast.FuncDecl` struct. It does this by adding each identifier to a map called `idents`, which is a field of the `FuncGen` struct.

Overall, the `FuncGen` struct and its associated methods are used to manipulate function declaration ASTs in the context of generating and patching Go source files. For example, a developer using the `cosmos-sdk` project might use `FuncGen` to programmatically add or modify function declarations in their codebase. Here is an example of how `FuncGen` might be used to add a new function to a Go source file:

```go
// create a new FileGen
fileGen := NewFileGen("example.go")

// create a new FuncGen
funcGen := fileGen.AddFunction("exampleFunction", "string", []*Field{
    NewField("arg1", "int"),
    NewField("arg2", "bool"),
})

// add a statement to the function body
funcGen.AddStatement("return arg1 + arg2")

// write the modified source code to a file
fileGen.WriteFile("example.go")
```

In this example, we create a new `FileGen` and use its `AddFunction` method to create a new function declaration with the name "exampleFunction", a return type of "string", and two parameters of type "int" and "bool". We then use the `AddStatement` method of the resulting `FuncGen` to add a return statement to the function body. Finally, we write the modified source code to a file using the `WriteFile` method of the `FileGen`.
## Questions: 
 1. What is the purpose of the `FuncGen` struct?
- The `FuncGen` struct is a utility for generating/patching golang function declaration ASTs.

2. What is the role of the `newFuncGen` function?
- The `newFuncGen` function creates a new instance of `FuncGen` and reserves parameter idents and results.

3. What package is being imported in this file?
- The `go/ast` package is being imported in this file.