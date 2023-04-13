[View code on GitHub](https://github.com/cosmos/cosmos-sdk/blob/main/x/auth/tx/config/textual.go)

The code above is part of the cosmos-sdk project and is located in the `tx` package. This file provides two functions that create a new `textual.SignModeHandler` instance. The `textual` package is used to handle the signing of transactions in the Cosmos SDK. 

The first function, `NewTextualWithGRPCConn`, creates a new `textual.SignModeHandler` instance where the metadata queries are done via gRPC using the provided GRPC client connection. This function takes a `grpc.ClientConnInterface` as an argument and returns a new `textual.SignModeHandler` instance and an error. The `textual.SignModeHandler` instance is created using the `textual.NewSignModeHandler` function, which takes a `textual.SignModeOptions` struct as an argument. The `CoinMetadataQuerier` field of the `textual.SignModeOptions` struct is set to a function that queries the metadata of a given coin denomination. This function uses the provided GRPC client connection to query the metadata of a given coin denomination. 

The second function, `NewTextualWithBankKeeper`, creates a new `textual.SignModeHandler` instance using the given `BankKeeper` to retrieve coin metadata. This function takes a `BankKeeper` as an argument and returns a new `textual.SignModeHandler` instance and an error. The `textual.SignModeHandler` instance is created using the `textual.NewSignModeHandler` function, which takes a `textual.SignModeOptions` struct as an argument. The `CoinMetadataQuerier` field of the `textual.SignModeOptions` struct is set to a function that queries the metadata of a given coin denomination. This function uses the provided `BankKeeper` to query the metadata of a given coin denomination. 

Both functions return a new `textual.SignModeHandler` instance that can be used to sign transactions in the Cosmos SDK. These functions are used in the larger project to provide a way to query the metadata of a given coin denomination when signing transactions. 

Example usage of `NewTextualWithGRPCConn`:

```
import (
    "google.golang.org/grpc"
    "cosmossdk.io/x/tx"
)

// create a new grpc client connection
conn, err := grpc.Dial("localhost:8080", grpc.WithInsecure())
if err != nil {
    // handle error
}

// create a new textual.SignModeHandler instance
handler, err := tx.NewTextualWithGRPCConn(conn)
if err != nil {
    // handle error
}

// use the handler to sign a transaction
// ...
```

Example usage of `NewTextualWithBankKeeper`:

```
import (
    "cosmossdk.io/x/tx"
    "cosmossdk.io/x/bank"
)

// create a new bank keeper
keeper := bank.NewKeeper(...)

// create a new textual.SignModeHandler instance
handler, err := tx.NewTextualWithBankKeeper(keeper)
if err != nil {
    // handle error
}

// use the handler to sign a transaction
// ...
```
## Questions: 
 1. What is the purpose of the `NewTextualWithGRPCConn` function?
- The `NewTextualWithGRPCConn` function returns a new `Textual` instance that queries metadata via gRPC using the provided GRPC client connection.

2. What is the difference between `NewTextualWithGRPCConn` and `NewTextualWithBankKeeper`?
- `NewTextualWithGRPCConn` uses a GRPC client connection to retrieve coin metadata, while `NewTextualWithBankKeeper` uses a `BankKeeper` to retrieve coin metadata.

3. What is the purpose of the `metadataExists` function?
- The `metadataExists` function parses the error and only propagates the error if it's different than a "not found" error.