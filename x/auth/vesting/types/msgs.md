[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/auth/vesting/types/msgs.go)

This file contains code for creating three different types of messages that can be used in the cosmos-sdk project. These messages are used to create different types of vesting accounts, which are accounts that hold funds that are released over time according to a predetermined schedule. 

The first message type is `MsgCreateVestingAccount`, which creates a vesting account that releases funds at a specific time in the future. This message takes in the sender's address, the recipient's address, the amount of funds to be vested, the end time for vesting, and a boolean indicating whether the vesting should be delayed. The `NewMsgCreateVestingAccount` function creates a new instance of this message type with the given parameters. The `GetSignBytes` function returns the bytes that must be signed by all expected signers for this message type, and the `GetSigners` function returns the expected signers for this message type.

The second message type is `MsgCreatePermanentLockedAccount`, which creates a vesting account that releases funds all at once after a certain period of time. This message takes in the sender's address, the recipient's address, and the amount of funds to be vested. The `NewMsgCreatePermanentLockedAccount` function creates a new instance of this message type with the given parameters. The `GetSignBytes` function and the `GetSigners` function for this message type are similar to those for `MsgCreateVestingAccount`.

The third message type is `MsgCreatePeriodicVestingAccount`, which creates a vesting account that releases funds in periodic intervals over a certain period of time. This message takes in the sender's address, the recipient's address, the start time for vesting, and an array of `Period` structs that specify the amount of funds to be released at each interval. The `NewMsgCreatePeriodicVestingAccount` function creates a new instance of this message type with the given parameters. The `GetSignBytes` function and the `GetSigners` function for this message type are also similar to those for `MsgCreateVestingAccount`.

Overall, these message types provide a way for users to create different types of vesting accounts in the cosmos-sdk project. These accounts can be used to hold funds that are released over time according to a predetermined schedule, which can be useful for managing funds in a variety of contexts.
## Questions: 
 1. What is the purpose of the `legacytx` package being imported?
- The `legacytx` package is being imported to allow for compatibility with legacy transactions.

2. What is the difference between `MsgCreateVestingAccount` and `MsgCreatePermanentLockedAccount`?
- `MsgCreateVestingAccount` creates an account that vests over time, while `MsgCreatePermanentLockedAccount` creates an account that is permanently locked.

3. What is the purpose of the `GetSignBytes` function in each of the message types?
- The `GetSignBytes` function returns the bytes that all expected signers must sign over for the message, which is used for signature verification.