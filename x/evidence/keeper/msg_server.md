[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/evidence/keeper/msg_server.go)

The code above is a part of the `cosmos-sdk` project and is located in the `keeper` package. It defines a `msgServer` struct that implements the `types.MsgServer` interface. The purpose of this code is to handle the submission of evidence in the Cosmos network.

The `NewMsgServerImpl` function returns an implementation of the `types.MsgServer` interface for the provided `Keeper`. This function takes a `Keeper` as an argument and returns a new `msgServer` instance.

The `SubmitEvidence` method is used to submit evidence to the network. It takes a context and a `MsgSubmitEvidence` message as arguments. The method first checks if the submitter address is valid. If the address is invalid, it returns an error. It then checks if the evidence is valid and if it passes the basic validation. If the evidence is invalid, it returns an error. Finally, it submits the evidence to the network using the `SubmitEvidence` method of the `Keeper`.

Here is an example of how this code can be used:

```
keeper := NewKeeper(...)
msgServer := NewMsgServerImpl(keeper)

msg := &types.MsgSubmitEvidence{
    Submitter: "cosmos1abc...",
    Evidence:  evidence,
}

response, err := msgServer.SubmitEvidence(context.Background(), msg)
if err != nil {
    // handle error
}

// use response
```

In summary, this code provides a way to submit evidence to the Cosmos network. It ensures that the evidence is valid and submits it to the network using the `Keeper`.
## Questions: 
 1. What is the purpose of the `keeper` package and how does it relate to the `cosmos-sdk` project?
- The `keeper` package is being imported and used in this file to implement the `MsgServer` interface for the `cosmos-sdk` project. It likely contains functionality related to managing state and data within the project.

2. What is the `SubmitEvidence` method doing and what types of errors can it return?
- The `SubmitEvidence` method is implementing the `MsgServer.SubmitEvidence` method and is responsible for validating and submitting evidence. It can return errors related to invalid addresses, missing evidence, and failed validation.

3. What is the purpose of the `NewMsgServerImpl` function and how is it used?
- The `NewMsgServerImpl` function returns an implementation of the `MsgServer` interface for the provided `Keeper`. It is used to create a new instance of the `msgServer` struct, which is then used to handle incoming messages related to submitting evidence.