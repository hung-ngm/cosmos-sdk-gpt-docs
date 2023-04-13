[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/consensus/keeper/keeper.go)

The `keeper` package in the `cosmos-sdk` project contains the implementation of the consensus module. The `Keeper` struct is defined with fields for storeService, event, authority, and ParamsStore. The `NewKeeper` function initializes a new `Keeper` instance with the provided `storeService`, `authority`, and `event`. It also creates a new `ParamsStore` instance using the provided `storeService` and `codec`. 

The `Params` function is used to query the consensus module's parameters. It retrieves the parameters from the `ParamsStore` and returns them in a `QueryParamsResponse`. 

The `UpdateParams` function is used to update the consensus module's parameters. It first checks that the `msg.Authority` matches the `Keeper`'s `authority`. It then converts the `msg` to a `ConsensusParams` struct and validates it. If the `ConsensusParams` struct is valid, it is stored in the `ParamsStore`. Finally, an event is emitted with the updated parameters and the `MsgUpdateParamsResponse` is returned.

This code is used to manage the consensus parameters of the `cosmos-sdk` blockchain. It provides functions to query and update the consensus parameters. The `ParamsStore` is used to store the consensus parameters, and the `UpdateParams` function ensures that only the authorized `authority` can update the parameters. This package is an important part of the `cosmos-sdk` project as it ensures that the blockchain's consensus parameters are properly managed. 

Example usage:

```
// create a new Keeper instance
keeper := NewKeeper(cdc, storeService, authority, em)

// query the consensus parameters
params, err := keeper.Params(ctx, &types.QueryParamsRequest{})
if err != nil {
    // handle error
}
fmt.Println(params)

// update the consensus parameters
msg := &types.MsgUpdateParams{
    Authority: "my_authority",
    Params:    myParams,
}
res, err := keeper.UpdateParams(ctx, msg)
if err != nil {
    // handle error
}
fmt.Println(res)
```
## Questions: 
 1. What is the purpose of the `Keeper` struct and what does it contain?
- The `Keeper` struct is used to manage the consensus module's state and contains a `storeService` for key-value store access, an `event` service for emitting events, an `authority` string, and a `ParamsStore` item for storing consensus parameters.

2. What is the purpose of the `Params` function and what does it return?
- The `Params` function is used to query the consensus module's parameters and returns a `QueryParamsResponse` containing the parameters.

3. What is the purpose of the `UpdateParams` function and what does it do?
- The `UpdateParams` function is used to update the consensus module's parameters and emits an event with the updated parameters. It returns a `MsgUpdateParamsResponse`.