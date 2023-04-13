[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/core/intermodule/client.go)

The `intermodule` package contains the `Client` and `Invoker` interfaces that are used for inter-module communication in the Cosmos SDK project. The `Client` interface is used to send messages and queries between modules, provided that the request is valid and can be authenticated. It extends the `grpc.ClientConnInterface` interface, which is used to establish a connection to a gRPC server.

The `InvokerByMethod` method resolves an `Invoker` function for the provided method name. The `Invoker` function is used to invoke a specific method route for inter-module communication. If the method name is not found, an error is returned.

The `InvokerByRequest` method resolves an `Invoker` function for the provided request type. This method only works for messages (`Msg`), as they are routed based on type name in transactions already. For queries, the `InvokerByMethod` method should be used instead. If the request type is not found, an error is returned.

The `DerivedClient` method returns an inter-module client for the ADR-028 derived module address for the provided key. This method is used to create a new client that is derived from the current client, but with a different module address. This is useful for cases where a module needs to communicate with another module that is derived from the current module.

The `Address` method returns the ADR-028 address of the client against which messages will be authenticated. This method is used to get the address of the current client, which is used for authentication purposes.

Overall, the `intermodule` package provides a set of interfaces that are used for inter-module communication in the Cosmos SDK project. These interfaces are used to send messages and queries between modules, and to authenticate these requests. The `Client` interface is extended from the `grpc.ClientConnInterface` interface, which is used to establish a connection to a gRPC server. The `Invoker` interface is used to invoke a specific method route for inter-module communication. The `DerivedClient` method is used to create a new client that is derived from the current client, but with a different module address. The `Address` method is used to get the address of the current client, which is used for authentication purposes.
## Questions: 
 1. What is the purpose of this code and how does it fit into the overall cosmos-sdk project?
- This code defines an interface for an inter-module client that allows modules to send messages and queries to other modules in the cosmos-sdk project, provided that the request is valid and authenticated.

2. What is the difference between InvokerByMethod and InvokerByRequest?
- InvokerByMethod resolves an invoker for a provided method, while InvokerByRequest resolves an invoker for a provided request type. InvokerByRequest only works for Msg's, while InvokerByMethod should be used for queries.

3. What is the ADR-028 derived module address and how is it used in the DerivedClient method?
- The ADR-028 derived module address is used to derive a new inter-module client for a specific module, based on a provided key. The DerivedClient method returns a new Client interface for the derived module address.