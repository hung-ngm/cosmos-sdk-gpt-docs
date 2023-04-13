[View code on GitHub](https://github.com/cosmos/cosmos-sdk/blob/main/orm/internal/codegen/codegen.go)

The code above is a Go package called `codegen` that contains two functions: `ORMPluginRunner` and `QueryProtoPluginRunner`. These functions are used to generate code for the Cosmos SDK project, specifically for the Object Relational Mapping (ORM) and Query Protocol Buffer (Proto) plugins.

The `ORMPluginRunner` function takes a `protogen.Plugin` object as input and generates ORM-related code for each file in the project that has tables or singletons defined. It sets the `SupportedFeatures` field of the `Plugin` object to indicate that it supports optional fields in Proto3. For each file that has tables or singletons, it creates a new generated file with a name that includes the original file's name and the suffix `.cosmos_orm.go`. It then calls the `gen` method of a `fileGen` object to generate ORM-related code for the file. If an error occurs during the generation process, it is returned.

The `QueryProtoPluginRunner` function is similar to `ORMPluginRunner`, but it generates Query Proto-related code instead. It also takes a `protogen.Plugin` object as input and sets the `SupportedFeatures` field to indicate that it supports optional fields in Proto3. For each file that has tables or singletons, it creates a new file with a name that includes the original file's name and the suffix `_query.proto`. It then calls the `gen` method of a `queryProtoGen` object to generate Query Proto-related code for the file. If an error occurs during the generation process, it is returned.

The `hasTables` function is a helper function that takes a `protogen.File` object as input and returns a boolean indicating whether the file has tables or singletons defined. It does this by iterating over each message in the file and checking if it has either a `TableDescriptor` or `SingletonDescriptor` extension.

Overall, these functions are used to generate code for the ORM and Query Proto plugins in the Cosmos SDK project. They take a `protogen.Plugin` object as input and generate code for each file in the project that has tables or singletons defined. The generated code is used to facilitate communication between the Cosmos SDK and a database, as well as to define the structure of queries that can be made to the database.
## Questions: 
 1. What is the purpose of this code and what does it do?
- This code is a Go package called `codegen` that contains two functions: `ORMPluginRunner` and `QueryProtoPluginRunner`. These functions generate code for ORM and query proto files respectively, based on the input protobuf files.

2. What external packages or dependencies does this code rely on?
- This code relies on several external packages, including `google.golang.org/protobuf/compiler/protogen`, `google.golang.org/protobuf/proto`, `google.golang.org/protobuf/types/pluginpb`, and `github.com/cosmos/cosmos-sdk/orm`. 

3. What is the expected input format for this code, and what is the expected output?
- The expected input format for this code is a set of protobuf files that define tables and singletons. The expected output is generated Go code for ORM and query proto files, which can be used to interact with the database and query data.