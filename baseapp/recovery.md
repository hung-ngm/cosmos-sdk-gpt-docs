[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/baseapp/recovery.go)

This file contains code related to error handling and recovery for the Cosmos SDK. It defines several types and functions that are used to create middleware chains for handling errors that occur during the execution of transactions.

The `RecoveryHandler` type is a function that takes an object and returns an error. It is used to handle recovery objects that are passed through the middleware chain. The `recoveryMiddleware` type is a function that takes a recovery object and returns a new middleware function and an error. The `processRecovery` function is used to process a middleware chain for a given recovery object. It takes the recovery object and the first middleware function in the chain as arguments and returns an error if any of the middleware functions return an error.

The `newRecoveryMiddleware` function is used to create a new middleware function that wraps a `RecoveryHandler` function and the next middleware function in the chain. The `newOutOfGasRecoveryMiddleware` function creates a standard middleware function for handling out-of-gas errors that occur during the execution of a transaction. It takes the gas limit, the current context, and the next middleware function in the chain as arguments. The `newDefaultRecoveryMiddleware` function creates a default middleware function that is added to the end of the chain. It handles any errors that were not handled by the previous middleware functions and returns an error that indicates that a panic occurred.

These functions are used to create middleware chains that are used to handle errors that occur during the execution of transactions. The middleware chains are created in the `app.runTx` method, which is responsible for executing transactions. The middleware functions are called in the order that they are added to the chain, and each function has the opportunity to handle the error or pass it on to the next function in the chain. The `newOutOfGasRecoveryMiddleware` and `newDefaultRecoveryMiddleware` functions are added to the chain by default, but additional middleware functions can be added as needed.

Example usage:

```go
func myRecoveryHandler(recoveryObj interface{}) error {
    // handle the recovery object
}

func myMiddleware(recoveryObj interface{}) (recoveryMiddleware, error) {
    // handle the recovery object and return the next middleware function
}

func myAppRunTx(tx sdk.Tx, ...) (sdk.Result, error) {
    // create the middleware chain
    middleware := newOutOfGasRecoveryMiddleware(gasWanted, ctx, newDefaultRecoveryMiddleware())
    middleware = newRecoveryMiddleware(myRecoveryHandler, middleware)
    middleware = newRecoveryMiddleware(myMiddleware, middleware)

    // execute the middleware chain
    err := processRecovery(nil, middleware)
    if err != nil {
        // handle the error
    }

    // execute the transaction
    result, err := app.runTx(tx, ...)
    if err != nil {
        // handle the error
    }

    return result, nil
}
```
## Questions: 
 1. What is the purpose of the `processRecovery` function?
   - The `processRecovery` function processes a chain of recovery middleware for a recovery object and stops processing when a non-nil error is returned or when the chain is processed.

2. What is the difference between `RecoveryHandler` and `recoveryMiddleware`?
   - `RecoveryHandler` is a function that handles a recovery object and returns a non-nil error if the object was processed. `recoveryMiddleware` is a wrapper for `RecoveryHandler` that creates a chain of middleware for handling recovery objects.

3. What is the purpose of the `newOutOfGasRecoveryMiddleware` function?
   - The `newOutOfGasRecoveryMiddleware` function creates a standard middleware for handling out-of-gas errors in the `app.runTx` method. It wraps the error in a `sdkerrors.ErrOutOfGas` error and includes information about the gas usage.