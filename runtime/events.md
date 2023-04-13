[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/runtime/events.go)

The `runtime` package in the `cosmos-sdk` project contains code related to the execution of smart contracts on the Cosmos blockchain. The `EventService` and `Events` types in this file are used to manage events emitted by smart contracts during their execution.

The `EventService` type implements the `event.Service` interface, which defines a method for retrieving an `event.Manager` instance. The `EventManager` method of `EventService` returns an instance of the `Events` type, which implements the `event.Manager` interface. The `Events` type is a wrapper around the `sdk.EventManagerI` interface, which is used to manage events emitted by smart contracts.

The `NewEventManager` function is a convenience function for creating a new `event.Manager` instance. It takes a `context.Context` argument and returns an instance of the `Events` type.

The `Emit` method of the `Events` type is used to emit a typed event that is defined in the protobuf file. The `protoiface.MessageV1` argument is a protobuf message that represents the event to be emitted. The `EmitKV` method is used to emit a key-value pair event. The `eventType` argument is a string that identifies the type of event being emitted, and the `attrs` argument is a variadic slice of `event.Attribute` values that represent the key-value pairs of the event. The `EmitNonConsensus` method is similar to `Emit`, but is used to emit events that are not part of the consensus protocol.

Overall, these types and functions provide a way for smart contracts to emit events during their execution, which can be used by other parts of the system to track and respond to changes on the blockchain. For example, a client application might use these events to update its user interface in response to changes on the blockchain.
## Questions: 
 1. What is the purpose of the `EventService` struct and how is it used?
- The `EventService` struct is used to implement the `event.Service` interface and contains an `Events` field. It is used to manage events in the Cosmos SDK.

2. What is the difference between `Emit` and `EmitKV` methods in the `Events` struct?
- `Emit` is used to emit a typed event that is defined in the protobuf file, while `EmitKV` is used to emit a key value pair event.

3. What is the significance of the `UnwrapSDKContext` function used in this code?
- The `UnwrapSDKContext` function is used to extract the `sdk.Context` from the `context.Context` passed as an argument to the functions in this code. This allows access to the `sdk.EventManager` used to manage events in the Cosmos SDK.