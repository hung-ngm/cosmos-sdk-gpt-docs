[View code on GitHub](https://github.com/cosmos/cosmos-sdk/blob/main/x/slashing/keeper/keeper.go)

The `keeper` package in the `cosmos-sdk` project contains the implementation of the `Keeper` struct, which is responsible for managing the slashing store. The `Keeper` struct contains the store key, binary codec, legacy amino codec, staking keeper, and authority. It provides methods for adding and retrieving address-pubkey relations, slashing validators, and jailing validators.

The `NewKeeper` function creates a new `Keeper` instance with the given binary codec, legacy amino codec, store key, staking keeper, and authority. The `GetAuthority` method returns the authority of the `x/slashing` module. The `Logger` method returns a module-specific logger.

The `AddPubkey` method adds an address-pubkey relation to the store. It takes a context and a public key as input, marshals the public key using the binary codec, and stores the relation in the key-value store. The `GetPubkey` method retrieves the public key from the store using the address as input. It returns an error if the address is not found in the store.

The `Slash` method attempts to slash a validator with the given consensus address, fraction, power, and distribution height. It delegates the slash to the staking module to make the necessary validator changes. It specifies no interaction reason. The `SlashWithInfractionReason` method attempts to slash a validator with the given consensus address, fraction, power, distribution height, and interaction reason. It delegates the slash to the staking module to make the necessary validator changes. It specifies an interaction reason. Both methods emit a `Slash` event with the validator's address, power, reason, and burned coins.

The `Jail` method attempts to jail a validator with the given consensus address. It delegates the jail to the staking module to make the necessary validator changes. It emits a `Jail` event with the validator's address.

Overall, the `keeper` package provides functionality for managing the slashing store and delegating slashing and jailing to the staking module. It is an important component of the `cosmos-sdk` project's consensus mechanism. Below is an example of how to use the `AddPubkey` method:

```
import (
    "github.com/cosmos/cosmos-sdk/crypto/keys/ed25519"
    "github.com/cosmos/cosmos-sdk/types"
    "github.com/cosmos/cosmos-sdk/x/slashing/keeper"
)

func main() {
    cdc := codec.New()
    legacyAmino := codec.NewLegacyAmino()
    storeKey := types.NewKVStoreKey("slashing")
    stakingKeeper := staking.NewKeeper(...)
    authority := "gov"
    slashingKeeper := keeper.NewKeeper(cdc, legacyAmino, storeKey, stakingKeeper, authority)

    privKey := ed25519.GenPrivKey()
    pubKey := privKey.PubKey()
    addr := pubKey.Address()

    err := slashingKeeper.AddPubkey(ctx, pubKey)
    if err != nil {
        panic(err)
    }

    retrievedPubKey, err := slashingKeeper.GetPubkey(ctx, addr)
    if err != nil {
        panic(err)
    }

    if !pubKey.Equals(retrievedPubKey) {
        panic("retrieved public key does not match original public key")
    }
}
```
## Questions: 
 1. What is the purpose of the `Keeper` struct and what does it contain?
- The `Keeper` struct is responsible for managing the slashing store and contains the store key, binary codec, legacy amino, staking keeper, and authority address.

2. What is the difference between `Slash` and `SlashWithInfractionReason` functions?
- `Slash` attempts to slash a validator without specifying an infraction reason, while `SlashWithInfractionReason` specifies an infraction reason.

3. What is the purpose of the `deleteAddrPubkeyRelation` function?
- The `deleteAddrPubkeyRelation` function deletes the address-pubkey relation from the slashing store.