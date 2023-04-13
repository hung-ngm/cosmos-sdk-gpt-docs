[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/depinject/internal/codegen/import.go)

The `codegen` package contains code generation utilities for the Cosmos SDK project. The `AddOrGetImport` function is used to add a new import to a Go source file and return the unique import prefix for that path. 

The function takes a `pkgPath` string as input, which represents the package path of the import to be added. If the `pkgPath` is empty or equal to the `codegenPkgPath` (a constant defined elsewhere in the package), the function returns an empty string. 

If the `pkgPath` is not already in the `pkgImportMap` (a map that stores information about previously added imports), a new `ast.ImportSpec` is created with the `Path` field set to the `pkgPath`. The `defaultPkgPrefix` function is called to generate a default import prefix for the package based on the last part of the package path. This prefix is then passed to the `doCreateIdent` function (also defined elsewhere in the package) to ensure that it is a valid Go identifier. If the generated identifier is different from the default prefix, it is set as the `Name` field of the `ImportSpec`.

The `ImportSpec` is then added to the `File`'s `Imports` slice, and an entry is added to the `pkgImportMap` with the `ImportSpec` and the generated import prefix. The generated import prefix is also added to the `idents` map (which stores all the identifiers used in the file) to ensure that it is not used again.

If the `pkgPath` is already in the `pkgImportMap`, the function simply returns the existing import prefix.

This function is used in various code generation tasks throughout the Cosmos SDK project to ensure that all necessary imports are added to the generated code. For example, in the `authz` module, the `AddOrGetImport` function is used to add imports for the `proto` and `protoauth` packages:

```
g.AddOrGetImport("github.com/gogo/protobuf/proto")
g.AddOrGetImport("github.com/cosmos/cosmos-sdk/x/authz/types/protoauth")
```

Overall, the `AddOrGetImport` function is a useful utility for generating Go code that requires imports from external packages.
## Questions: 
 1. What is the purpose of the `FileGen` type and how is it used in this package?
- The `FileGen` type is not defined in this file, but it is used as a receiver for the `AddOrGetImport` method. It is likely used to generate code files.
2. What is the `pkgImportMap` field of the `FileGen` type and how is it populated?
- The `pkgImportMap` field is a map that associates package paths with `importInfo` structs. It is populated by the `AddOrGetImport` method when a new import is added.
3. What is the purpose of the `defaultPkgPrefix` function and how is it used?
- The `defaultPkgPrefix` function takes a package path and returns the last part of it (after the last "/"). It is used to generate a default import prefix for the package if one is not provided.