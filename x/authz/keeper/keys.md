[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/authz/keeper/keys.go)

This file contains the implementation of the `keeper` package for the `cosmos-sdk` project. The package provides functionality for managing authorization grants. The package defines two store prefixes, `GrantKey` and `GrantQueuePrefix`, which are used to store authorization grants and grant queue items, respectively. 

The `grantStoreKey` function returns the store key for a given authorization grant. The key is constructed by concatenating the granter address, grantee address, and message type. The `parseGrantStoreKey` function is used to parse the granter address, grantee address, and message type from the authorization key. 

The `GrantQueueKey` function returns the store key for a given grant queue item. The key is constructed by concatenating the expiration time, granter address, and grantee address. The `parseGrantQueueKey` function is used to parse the expiration time, granter address, and grantee address from the grant queue key. 

The `GrantQueueTimePrefix` function returns the store key prefix for all grant queue items with a given expiration time. The `firstAddressFromGrantStoreKey` function is used to parse the granter address from an authorization key. 

Overall, this package provides functionality for managing authorization grants and grant queue items in the `cosmos-sdk` project. The functions defined in this package can be used by other modules in the project to manage authorization grants. For example, the `authz` module in the `cosmos-sdk` project uses this package to manage authorization grants. 

Example usage of `grantStoreKey`:
```
granter := sdk.AccAddress([]byte("granter"))
grantee := sdk.AccAddress([]byte("grantee"))
msgType := "msgType"
key := grantStoreKey(grantee, granter, msgType)
```

Example usage of `parseGrantStoreKey`:
```
granterAddr, granteeAddr, msgType := parseGrantStoreKey(key)
```

Example usage of `GrantQueueKey`:
```
expiration := time.Now().Add(time.Hour)
granter := sdk.AccAddress([]byte("granter"))
grantee := sdk.AccAddress([]byte("grantee"))
key := GrantQueueKey(expiration, granter, grantee)
```

Example usage of `parseGrantQueueKey`:
```
exp, granter, grantee, err := parseGrantQueueKey(key)
```
## Questions: 
 1. What is the purpose of the `keeper` package and how does it relate to the `cosmos-sdk` project as a whole?
- The `keeper` package likely contains functionality related to managing and storing authorization grants within the `cosmos-sdk` project.
- It is not clear from this code alone how the `keeper` package fits into the larger `cosmos-sdk` project.

2. What is the format of the keys used to store grants and grant queue items?
- Grants are stored with the key prefix `0x01` followed by the granter address, grantee address, and message type.
- Grant queue items are stored with the key prefix `0x02` followed by the expiration time, granter address, and grantee address.

3. What is the purpose of the `GrantQueueTimePrefix` function?
- The `GrantQueueTimePrefix` function returns a byte slice that can be used to query the grant queue for all items with a given expiration time.
- This function is likely used to facilitate pruning of expired grant queue items.