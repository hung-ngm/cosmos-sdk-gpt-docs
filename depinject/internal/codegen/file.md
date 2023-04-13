[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/depinject/internal/codegen/file.go)

The `FileGen` struct is a utility for generating and patching Go file Abstract Syntax Trees (ASTs) in the `cosmos-sdk` project. It contains the `File` field, which is a pointer to the AST of the file being generated or patched. The `idents` field is a map of all the reserved identifiers in the file, including Go keywords and top-level declaration identifiers. The `codegenPkgPath` field is a string representing the package path of the code generator. The `pkgImportMap` field is a map of package import paths to `importInfo` structs, which contain information about the package imports.

The `NewFileGen` function creates a new `FileGen` instance from a file AST with the provided package path. It initializes the `idents` map with all Go keywords and top-level declaration identifiers in the file. It then iterates over all the declarations in the file and adds their identifiers to the `idents` map. Finally, it iterates over all the import statements in the file and creates an `importInfo` struct for each package import, which is added to the `pkgImportMap` map.

The `PatchFuncDecl` method returns a `FuncGen` instance for the function declaration with the given name or returns `nil`. The `FuncGen` struct is another utility for generating and patching Go function ASTs.

Overall, the `FileGen` struct and its associated functions are used to generate and patch Go file ASTs in the `cosmos-sdk` project. It provides a convenient way to manipulate the ASTs programmatically, which can be useful for code generation and other tasks. Here is an example of how `FileGen` might be used:

```go
package main

import (
	"go/ast"
	"go/parser"
	"go/token"

	"github.com/cosmos/cosmos-sdk/codegen"
)

func main() {
	// Parse the file AST
	fset := token.NewFileSet()
	file, err := parser.ParseFile(fset, "example.go", nil, 0)
	if err != nil {
		panic(err)
	}

	// Create a new FileGen instance
	fileGen, err := codegen.NewFileGen(file, "github.com/cosmos/cosmos-sdk/codegen")
	if err != nil {
		panic(err)
	}

	// Patch the function declaration
	funcGen := fileGen.PatchFuncDecl("ExampleFunc")
	if funcGen == nil {
		panic("function not found")
	}
	funcGen.AddStatement(&ast.ExprStmt{X: &ast.BasicLit{Kind: token.STRING, Value: `"Hello, world!"`}})

	// Print the modified file AST
	ast.Print(fset, file)
}
```
## Questions: 
 1. What is the purpose of the `FileGen` struct?
- The `FileGen` struct is a utility for generating/patching golang file ASTs.

2. What does the `NewFileGen` function do?
- The `NewFileGen` function creates a new `FileGen` instance from a file AST with the provided package path, and initializes the `idents` and `pkgImportMap` fields.

3. What is the purpose of the `PatchFuncDecl` method?
- The `PatchFuncDecl` method returns a `FuncGen` instance for the function declaration with the given name or returns nil.