[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/staking/keeper/power_reduction.go)

The code above is a part of the `keeper` package in the `cosmos-sdk` project. It contains two functions that are used to convert tokens to consensus power and vice versa. 

The `TokensToConsensusPower` function takes in a `sdk.Context` and a `math.Int` representing the number of tokens to be converted. It then calls the `TokensToConsensusPower` function from the `sdk` package, passing in the tokens and the result of calling `PowerReduction` on the `Keeper` instance `k` and returns the result as an `int64`. The purpose of this function is to convert the number of tokens to the potential consensus-engine power that they represent. 

The `TokensFromConsensusPower` function takes in a `sdk.Context` and an `int64` representing the consensus power to be converted. It then calls the `TokensFromConsensusPower` function from the `sdk` package, passing in the power and the result of calling `PowerReduction` on the `Keeper` instance `k` and returns the result as a `math.Int`. The purpose of this function is to convert the consensus power back to the number of tokens that it represents. 

These functions are likely used in the larger `cosmos-sdk` project to handle the conversion of tokens to consensus power and vice versa in the context of the consensus engine. They may be used, for example, in the staking module to convert the number of tokens staked by a validator to the consensus power that they have in the network. 

Example usage of these functions:

```
import (
    "cosmos-sdk/x/staking/keeper"
    "cosmos-sdk/math"
    sdk "github.com/cosmos/cosmos-sdk/types"
)

func myFunc(k keeper.Keeper, ctx sdk.Context, tokens math.Int) {
    consensusPower := k.TokensToConsensusPower(ctx, tokens)
    // do something with consensusPower
    tokensAgain := k.TokensFromConsensusPower(ctx, consensusPower)
    // tokensAgain should be equal to tokens
}
```
## Questions: 
 1. What is the purpose of the `TokensToConsensusPower` and `TokensFromConsensusPower` functions?
- These functions are used to convert tokens to potential consensus-engine power and vice versa.

2. What is the `Keeper` type and where is it defined?
- The `Keeper` type is used in this code as a receiver for the `TokensToConsensusPower` and `TokensFromConsensusPower` functions. It is likely defined in another file within the `cosmos-sdk` project.

3. What is the `math.Int` type and where is it imported from?
- The `math.Int` type is used as a parameter and return type for the `TokensToConsensusPower` and `TokensFromConsensusPower` functions. It is imported from the `cosmossdk.io/math` package.