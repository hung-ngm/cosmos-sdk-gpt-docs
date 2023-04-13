[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/crisis/keeper/keeper.go)

The code defines the `Keeper` struct and associated methods for the `x/crisis` module in the Cosmos SDK. The `Keeper` struct contains information about the module's invariants, the store key, the binary codec, the authority, the supply keeper, and the fee collector name. 

The `NewKeeper` function initializes a new `Keeper` object with the given parameters and returns a pointer to it. 

The `GetAuthority` method returns the authority of the `x/crisis` module. 

The `Logger` method returns a module-specific logger for the `x/crisis` module. 

The `RegisterRoute` method registers the routes for each of the invariants. It takes the module name, route, and invariant as parameters and creates a new `InvarRoute` object with them. The `InvarRoute` object is then appended to the `Keeper`'s `routes` slice. 

The `Routes` method returns the `Keeper`'s invariant routes. 

The `Invariants` method returns a copy of all registered `Crisis` keeper invariants. 

The `AssertInvariants` method asserts all registered invariants. It iterates over the `Keeper`'s `routes` slice, gets the invariant context, and checks if the invariant is broken. If the invariant is broken, the method panics. 

The `InvCheckPeriod` method returns the invariant checks period. 

The `SendCoinsFromAccountToFeeCollector` method transfers coins from an account to the fee collector account. It takes the context, sender address, and amount as parameters and calls the `SendCoinsFromAccountToModule` method of the `supplyKeeper` to transfer the coins. 

Overall, this code defines the `Keeper` struct and associated methods for the `x/crisis` module in the Cosmos SDK. The `Keeper` is responsible for registering and asserting invariants, transferring coins to the fee collector account, and providing information about the module's authority and invariant check period.
## Questions: 
 1. What is the purpose of the `Keeper` struct and what are its main fields?
- The `Keeper` struct is responsible for managing the crisis module's state and logic. Its main fields include the `routes` for each of the invariants, the `invCheckPeriod` for how often to check the invariants, the `storeKey` for the module's store, the `cdc` for binary encoding and decoding, the `authority` for executing a `MsgUpdateParams` message, the `supplyKeeper` for managing the module's supply, and the `feeCollectorName` for the name of the FeeCollector ModuleAccount.

2. What is the purpose of the `RegisterRoute` function and how is it used?
- The `RegisterRoute` function is used to register the routes for each of the invariants. It takes in the `moduleName`, `route`, and `invar` as parameters and creates a new `InvarRoute` object. This object is then appended to the `Keeper`'s `routes` slice.

3. What is the purpose of the `AssertInvariants` function and what happens if an invariant fails?
- The `AssertInvariants` function is responsible for asserting all registered invariants. It loops through each `InvarRoute` in the `Keeper`'s `routes` slice and calls its `Invar` function to check if the invariant is still valid. If any invariant fails, the function panics and provides an error message with instructions on how to fix the issue.