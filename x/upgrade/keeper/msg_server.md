[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/upgrade/keeper/msg_server.go)

This code is a part of the cosmos-sdk project and it defines a message server for the upgrade module. The upgrade module is responsible for managing software upgrades in the Cosmos network. The message server is implemented as a struct called `msgServer` which has a reference to a `Keeper` struct. The `Keeper` struct is responsible for managing the state of the upgrade module.

The `NewMsgServerImpl` function returns an implementation of the `types.MsgServer` interface for the provided `Keeper`. The `types.MsgServer` interface defines the methods that a message server should implement. In this case, the `msgServer` struct implements the `SoftwareUpgrade` and `CancelUpgrade` methods.

The `SoftwareUpgrade` method is called when a software upgrade is scheduled. It takes a `MsgSoftwareUpgrade` message as input and returns a `MsgSoftwareUpgradeResponse` message and an error. The `MsgSoftwareUpgrade` message contains information about the upgrade plan and the authority that is responsible for authorizing the upgrade. The method first checks if the authority in the message matches the authority in the `Keeper`. If they don't match, it returns an error. Then it validates the upgrade plan and schedules the upgrade using the `ScheduleUpgrade` method of the `Keeper`. If there is an error, it returns the error.

The `CancelUpgrade` method is called when a software upgrade is cancelled. It takes a `MsgCancelUpgrade` message as input and returns a `MsgCancelUpgradeResponse` message and an error. The `MsgCancelUpgrade` message contains information about the authority that is responsible for cancelling the upgrade. The method first checks if the authority in the message matches the authority in the `Keeper`. If they don't match, it returns an error. Then it clears the upgrade plan using the `ClearUpgradePlan` method of the `Keeper`.

Overall, this code provides an implementation of the message server for the upgrade module. It allows users to schedule and cancel software upgrades in the Cosmos network. The `Keeper` struct is responsible for managing the state of the upgrade module and the `msgServer` struct provides an interface for interacting with the upgrade module. Here is an example of how to use this code:

```
// create a new Keeper
k := NewKeeper()

// create a new message server
msgServer := NewMsgServerImpl(k)

// schedule a software upgrade
plan := types.NewUpgradePlan(...)
msg := types.NewMsgSoftwareUpgrade(...)
response, err := msgServer.SoftwareUpgrade(ctx, msg)

// cancel a software upgrade
msg := types.NewMsgCancelUpgrade(...)
response, err := msgServer.CancelUpgrade(ctx, msg)
```
## Questions: 
 1. What is the purpose of this code file?
- This code file contains the implementation of the upgrade MsgServer interface for the provided Keeper.

2. What is the significance of the `authority` field in the `SoftwareUpgrade` and `CancelUpgrade` functions?
- The `authority` field is used to validate the signer of the message. If the `authority` field does not match the signer of the message, an error is returned.

3. What is the role of the `ScheduleUpgrade` and `ClearUpgradePlan` functions?
- The `ScheduleUpgrade` function is used to schedule a software upgrade plan, while the `ClearUpgradePlan` function is used to clear the current upgrade plan.