[View code on GitHub](https://github.com/cosmos/cosmos-sdk/blob/main/x/feegrant/key.go)

The `feegrant` package in the `cosmos-sdk` project provides functionality for granting fee allowances to other accounts. This is useful in scenarios where an account wants to allow another account to spend its funds for a limited time or up to a certain amount. 

The package defines several constants, including `ModuleName`, `StoreKey`, `RouterKey`, and `QuerierRoute`, which are used in various places throughout the project. 

The package also defines several helper functions for working with fee allowances. The `FeeAllowanceKey` function takes a granter and grantee address and returns a canonical key to store a grant from the granter to the grantee. The `FeeAllowancePrefixByGrantee` function returns a prefix to scan for all grants to a given address. The `FeeAllowancePrefixQueue` function returns a canonical key to store a grant key. The `AllowanceByExpTimeKey` function returns a key with `FeeAllowanceQueueKeyPrefix` and expiry. The `ParseAddressesFromFeeAllowanceKey` and `ParseAddressesFromFeeAllowanceQueueKey` functions extract and return the granter and grantee from a given key. 

Overall, the `feegrant` package provides a useful set of tools for managing fee allowances in the `cosmos-sdk` project. Here is an example of how to use the `FeeAllowanceKey` function:

```
granter := sdk.AccAddress([]byte("my_granter_address"))
grantee := sdk.AccAddress([]byte("my_grantee_address"))
key := FeeAllowanceKey(granter, grantee)
```
## Questions: 
 1. What is the purpose of the `feegrant` package in the `cosmos-sdk` project?
- The `feegrant` package is a module that manages fee allowances for accounts in the Cosmos SDK.

2. What is the format of the key used to store a fee grant from a granter to a grantee?
- The key format is `<0x00><len(grantee_address_bytes)><grantee_address_bytes><len(granter_address_bytes)><granter_address_bytes>`.

3. How are the granter and grantee addresses extracted from a fee allowance queue key?
- The granter and grantee addresses are extracted from the key using the `ParseAddressesFromFeeAllowanceQueueKey` function, which parses the key format of `<0x01><expiration_bytes(fixed length)><granteeAddressLen (1 Byte)><granteeAddress_Bytes><granterAddressLen (1 Byte)><granterAddress_Bytes>`.