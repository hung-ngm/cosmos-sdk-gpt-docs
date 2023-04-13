[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/auth/keeper/genesis.go)

The `keeper` package in the `cosmos-sdk` project contains code related to managing accounts and their state. The file provided contains two methods: `InitGenesis` and `ExportGenesis`.

The `InitGenesis` method initializes the state of the account store from the provided `GenesisState` data. It first sets the parameters of the account keeper using the `SetParams` method. Then, it unpacks the accounts from the `GenesisState` data using the `UnpackAccounts` method and sanitizes them using the `SanitizeGenesisAccounts` method. After that, it sets the accounts in the account store using the `SetAccount` method. It also ensures that the global account number matches the largest account number by iterating over the accounts and setting the account number using the `NextAccountNumber` method. Finally, it retrieves the module account for the fee collector using the `GetModuleAccount` method.

The `ExportGenesis` method returns a `GenesisState` for a given context and keeper. It first retrieves the parameters of the account keeper using the `GetParams` method. Then, it iterates over all the accounts in the account store using the `IterateAccounts` method and appends them to a slice of `GenesisAccount` types. Finally, it returns a new `GenesisState` using the `NewGenesisState` method with the retrieved parameters and the slice of `GenesisAccount` types.

These methods are used in the larger `cosmos-sdk` project to manage the state of accounts and their parameters. The `InitGenesis` method is called when initializing the state of the account store from the `GenesisState` data, while the `ExportGenesis` method is called when exporting the current state of the account store to a `GenesisState` for storage or transfer. Here is an example of how these methods might be used:

```go
// create a new account keeper
ak := keeper.NewAccountKeeper(...)

// initialize the account store from the genesis state data
ak.InitGenesis(ctx, genesisState)

// export the current state of the account store to a genesis state
exportedGenesis := ak.ExportGenesis(ctx)
```
## Questions: 
 1. What is the purpose of the `InitGenesis` function?
- The `InitGenesis` function is used to initialize the store state from genesis data, and it also transfers old coins from the `FeeCollectionKeeper` to the new fee collector account.

2. What does the `ExportGenesis` function do?
- The `ExportGenesis` function returns a `GenesisState` for a given context and keeper, which includes the parameters and genesis accounts.

3. What is the role of the `AccountKeeper` type in this code?
- The `AccountKeeper` type is the receiver of the `InitGenesis` and `ExportGenesis` functions, and it is responsible for managing accounts and their associated data in the cosmos-sdk.