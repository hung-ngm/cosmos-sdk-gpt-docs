[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/authz/keeper/msg_server.go)

The code above is a part of the `cosmos-sdk` project and is located in the `keeper` package. The purpose of this code is to implement the `authz.MsgServer` interface, which provides methods for creating, revoking, and executing authorization grants. 

The `Grant` method creates a new grant by validating the grantee and granter addresses, validating the grant message, creating an account if it does not exist, and saving the grant. The `Revoke` method revokes a grant by deleting it from the store. The `Exec` method executes a grant by validating the grantee address, validating the messages, and dispatching the actions. 

This code is used in the larger `cosmos-sdk` project to provide authorization functionality. It allows users to create and revoke grants, which can be used to authorize actions on their behalf. For example, a user could create a grant that allows a third-party application to execute transactions on their behalf. This grant could be revoked at any time, giving the user control over their account. 

Here is an example of how this code could be used to create a grant:

```
import (
    "context"
    "github.com/cosmos/cosmos-sdk/x/authz"
    "github.com/cosmos/cosmos-sdk/types"
)

func createGrant(ctx context.Context, keeper authz.Keeper, grantee types.AccAddress, granter types.AccAddress, authorization authz.Authorization, expiration int64) error {
    msg := authz.NewMsgGrant(grantee.String(), granter.String(), authorization, expiration)
    _, err := keeper.Grant(ctx, msg)
    return err
}
```

This function creates a new grant by calling the `Grant` method on the `authz.Keeper` object. It takes a context, the keeper, the grantee and granter addresses, an authorization object, and an expiration time. If the grant is created successfully, it returns nil. Otherwise, it returns an error.
## Questions: 
 1. What is the purpose of this code file?
- This code file contains the implementation of the `MsgServer` interface for the `authz` module in the Cosmos SDK, specifically the `Grant`, `Revoke`, and `Exec` methods.

2. What are the parameters and return values of the `Grant` method?
- The `Grant` method takes in a context and a pointer to a `MsgGrant` struct, and returns a pointer to a `MsgGrantResponse` struct and an error.

3. What is the purpose of the `validateMsgs` function?
- The `validateMsgs` function is used to validate the basic structure of messages in a slice of `sdk.Msg` objects, and returns an error if any of the messages fail validation.