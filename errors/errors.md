[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/errors/errors.go)

The `errors` package provides a way to define and handle errors in the Cosmos SDK project. It defines a root error type called `Error` that is used to categorize issues. Each instance created during the runtime should wrap one of the declared root errors. This allows error tests and returning all errors to the client in a safe manner. 

The `Register` function returns an error instance that should be used as the base for creating error instances during runtime. Popular root errors are declared in this package, but extensions may want to declare custom codes. This function ensures that no error code is used twice. Attempt to reuse an error code results in panic. The `RegisterWithGRPCCode` function is a version of `Register` that associates a gRPC error code with a registered error.

The `ABCIError` function resolves an error code/log from an abci result into an error message. If the code is registered, it will map it back to the canonical error, so we can do eg. `ErrNotFound.Is(err)` on something we get back from an external API. This should only be used in clients, not in the server side. The server (abci app / blockchain) should only refer to registered errors.

The `Error` type represents a root error. All popular root errors are declared in this package. If an extension has to declare a custom root error, always use `Register` function to ensure error code uniqueness. The `New` function is an alias for `Register`.

The `Is` method checks if given error instance is of a given kind/type. This involves unwrapping given error using the `Cause` method if available. The `Wrap` function extends given error with an additional information. If the wrapped error does not provide `ABCICode` method (ie. stdlib errors), it will be labeled as internal error. The `Wrapf` function extends given error with an additional information. This function works like `Wrap` function with additional functionality of formatting the input as specified.

The `Recover` function captures a panic and stops its propagation. If panic happens it is transformed into an `ErrPanic` instance and assigned to given error. Call this function using defer in order to work as expected.

The `WithType` function is a helper to augment an error with a corresponding type message. The `IsOf` function checks if a received error is caused by one of the target errors. It extends the `errors.Is` functionality to a list of errors.
## Questions: 
 1. What is the purpose of the `Register` function?
- The `Register` function returns an error instance that should be used as the base for creating error instances during runtime. It ensures that no error code is used twice and should only be used during a program startup phase.

2. What is the purpose of the `ABCIError` function?
- The `ABCIError` function resolves an error code/log from an abci result into an error message. If the code is registered, it will map it back to the canonical error, so we can do eg. ErrNotFound.Is(err) on something we get back from an external API. This should only be used in clients, not in the server side.

3. What is the purpose of the `Recover` function?
- The `Recover` function captures a panic and stops its propagation. If a panic happens, it is transformed into an `ErrPanic` instance and assigned to the given error. It should be called using defer in order to work as expected.