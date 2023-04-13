[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/types/denom.go)

The `types` package contains various types and functions used throughout the Cosmos SDK. This specific file contains functions related to denominations and their units. 

The `denomUnits` variable is a map that contains a mapping of denomination to their respective unit multipliers. The `baseDenom` variable is the denomination of the smallest unit registered. 

The `RegisterDenom` function registers a denomination with a corresponding unit. If the denomination is already registered, an error will be returned. This function is used to register new denominations and their respective units. 

The `GetDenomUnit` function returns the unit for a given denomination if it exists. A boolean is returned if the denomination is registered. This function is used to get the unit of a given denomination. 

The `GetBaseDenom` function returns the denomination of the smallest unit registered. This function is used to get the denomination of the smallest unit. 

The `ConvertCoin` function attempts to convert a coin to a given denomination. If the given denomination is invalid or if neither denomination is registered, an error is returned. This function is used to convert a coin to a different denomination. 

The `ConvertDecCoin` function attempts to convert a decimal coin to a given denomination. If the given denomination is invalid or if neither denomination is registered, an error is returned. This function is used to convert a decimal coin to a different denomination. 

The `NormalizeCoin` function tries to convert a coin to the smallest unit registered and returns the original one if it fails. This function is used to normalize a coin to the smallest unit. 

The `NormalizeDecCoin` function tries to convert a decimal coin to the smallest unit registered and returns the original one if it fails. This function is used to normalize a decimal coin to the smallest unit. 

The `NormalizeCoins` function normalizes and truncates a list of decimal coins. This function is used to normalize and truncate a list of decimal coins. 

Overall, this file provides functions related to denominations and their units, which are used throughout the Cosmos SDK to handle different denominations and their conversions.
## Questions: 
 1. What is the purpose of the `denomUnits` map and how is it used in the package?
- The `denomUnits` map contains a mapping of denomination to their respective unit multipliers. It is used to register and retrieve units for a given denomination.

2. How does the `ConvertCoin` function work and what does it return?
- The `ConvertCoin` function attempts to convert a `Coin` to a given denomination by multiplying the amount by the source unit and dividing by the destination unit. It returns a new `Coin` with the converted amount and the given denomination.

3. What is the purpose of the `NormalizeCoins` function and how does it work?
- The `NormalizeCoins` function normalizes and truncates a list of `DecCoin`s to the smallest unit registered. It does this by calling `NormalizeDecCoin` on each `DecCoin`, truncating the result, and appending it to a list of `Coin`s. The resulting list of `Coin`s is returned as a `Coins` object.