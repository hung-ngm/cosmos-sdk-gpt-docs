[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/evidence/types/msgs.go)

The `types` package in the `cosmos-sdk` project contains various types and interfaces used throughout the project. This specific file defines a message type called `MsgSubmitEvidence` that is used to submit evidence of misbehavior on the blockchain. 

The `MsgSubmitEvidence` message type implements several interfaces, including `sdk.Msg`, `legacytx.LegacyMsg`, `types.UnpackInterfacesMessage`, and `exported.MsgSubmitEvidenceI`. This allows the message to be used in different contexts throughout the SDK.

The `NewMsgSubmitEvidence` function creates a new `MsgSubmitEvidence` message with a signer/submitter and an `exported.Evidence` object. The function first checks if the evidence object can be marshaled into a `proto.Message`. If it can, the function creates a new `types.Any` object with the marshaled message and returns a new `MsgSubmitEvidence` object with the submitter and evidence.

The `GetSignBytes` function returns the raw bytes that a signer is expected to sign when submitting a `MsgSubmitEvidence` message. It uses the `ModuleCdc` codec to marshal the message into JSON and then sorts the JSON bytes before returning them.

The `GetSigners` function returns the single expected signer for a `MsgSubmitEvidence` message. It parses the submitter address from the message and returns it as a slice of `sdk.AccAddress`.

The `GetEvidence` function returns the evidence object contained in the `MsgSubmitEvidence` message. It first checks if the evidence is nil and returns nil if it is. Otherwise, it attempts to unpack the evidence object from the `types.Any` object using the `AnyUnpacker` interface. If successful, it returns the unpacked evidence object.

The `GetSubmitter` function returns the submitter address contained in the `MsgSubmitEvidence` message. It parses the submitter address from the message and returns it as an `sdk.AccAddress`.

The `UnpackInterfaces` function unpacks the evidence object from the `types.Any` object using the `AnyUnpacker` interface. It first creates a new `exported.Evidence` object and then unpacks the `types.Any` object into it. If successful, it returns nil.

Overall, this file defines a message type and several functions that are used to create, sign, and unpack `MsgSubmitEvidence` messages. These messages are used to submit evidence of misbehavior on the blockchain and are an important part of the Cosmos SDK's governance and security features.
## Questions: 
 1. What is the purpose of the `MsgSubmitEvidence` type?
- The `MsgSubmitEvidence` type is used to submit evidence of misbehavior on the blockchain.

2. What is the significance of the variables prefixed with an underscore?
- The variables prefixed with an underscore are used to ensure that the `MsgSubmitEvidence` type implements certain interfaces.

3. What is the purpose of the `UnpackInterfaces` method?
- The `UnpackInterfaces` method is used to unpack the `Evidence` field of the `MsgSubmitEvidence` type into an `exported.Evidence` interface.