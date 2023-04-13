[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/authz/msgs.go)

This code defines three message types (`MsgGrant`, `MsgRevoke`, and `MsgExec`) that are used in the Cosmos SDK project for authorization purposes. 

`MsgGrant` is used to grant authorization to a `Grantee` to perform certain actions on behalf of the `Granter`. The `Authorization` field specifies the type of authorization granted and the `Expiration` field specifies the time when the authorization expires. 

`MsgRevoke` is used to revoke authorization that was previously granted to a `Grantee`. The `MsgTypeUrl` field specifies the type of authorization that is being revoked. 

`MsgExec` is used to execute a set of messages on behalf of a `Grantee`. The `Msgs` field contains the messages to be executed. 

All three message types implement the `sdk.Msg` interface, which is used to define messages that can be sent and received by the Cosmos SDK. They also implement the `LegacyMsg` interface, which is used for backwards compatibility with older versions of the SDK. 

The `NewMsgGrant` function creates a new `MsgGrant` message with the specified `Granter`, `Grantee`, `Authorization`, and `Expiration`. The `SetAuthorization` and `GetAuthorization` functions are used to set and get the `Authorization` field of a `MsgGrant` message. 

The `NewMsgRevoke` function creates a new `MsgRevoke` message with the specified `Granter`, `Grantee`, and `MsgTypeUrl`. 

The `NewMsgExec` function creates a new `MsgExec` message with the specified `Grantee` and `Msgs`. The `GetMessages` function is used to get the messages contained in a `MsgExec` message. 

The `UnpackInterfaces` functions are used to unpack the interfaces contained in the messages. 

Overall, these message types are used to implement authorization in the Cosmos SDK. They allow for the granting and revocation of permissions to perform certain actions, as well as the execution of messages on behalf of another account.
## Questions: 
 1. What is the purpose of the `authz` package?
- The `authz` package provides functionality for authorization and permission control in the Cosmos SDK.

2. What is the difference between `MsgGrant` and `MsgRevoke`?
- `MsgGrant` is used to grant authorization to a `Grantee` by a `Granter`, while `MsgRevoke` is used to revoke authorization previously granted by a `Granter` to a `Grantee`.

3. What is the purpose of the `UnpackInterfaces` method in `MsgExec` and `MsgGrant`?
- The `UnpackInterfaces` method is used to unpack the `cdctypes.Any` values in the `MsgExec` and `MsgGrant` messages into their respective types, allowing them to be used in the Cosmos SDK.