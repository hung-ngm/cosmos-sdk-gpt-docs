[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/codec/legacy/doc.go)

The `legacy` package in the `cosmos-sdk` project contains a global amino codec (`Cdc`) that is deprecated but still used in several places within the SDK. This package is intended to be removed at some point in the future when the global `Cdc` is removed. The package also contains a utility function `RegisterAminoMsg` that checks the length of a message name before registering the concrete message type with amino.

The `Cdc` codec is used to encode and decode Go structs into binary format for storage or transmission. It is deprecated because it has been replaced by a more efficient and flexible codec in the `codec` package. However, some parts of the SDK still rely on the `Cdc` codec, so it is still included in the `legacy` package for backwards compatibility.

The `RegisterAminoMsg` function is used to register a concrete message type with the amino codec. It first checks the length of the message name to ensure that it is not too long, as amino has a limit on the length of message names. If the name is too long, an error is returned. Otherwise, the message type is registered with the codec using the `amino.RegisterConcrete` function.

Here is an example usage of the `RegisterAminoMsg` function:

```go
import (
    "github.com/cosmos/cosmos-sdk/codec/legacy"
    "github.com/cosmos/cosmos-sdk/types"
)

type MyMsg struct {
    // message fields
}

func init() {
    // register MyMsg with the amino codec
    err := legacy.RegisterAminoMsg(types.NameMsgPair{"myapp/MyMsg", MyMsg{})
    if err != nil {
        panic(err)
    }
}
```

In this example, we define a custom message type `MyMsg` and register it with the amino codec using `RegisterAminoMsg`. The message name is `"myapp/MyMsg"`, which is a concatenation of the application name (`myapp`) and the message type name (`MyMsg`). If the message name is too long, an error will be returned and the registration will fail.

Overall, the `legacy` package provides backwards compatibility for the deprecated `Cdc` codec and includes a utility function for registering message types with the amino codec. However, this package is intended to be removed in the future when the global `Cdc` is no longer used in the SDK.
## Questions: 
 1. What is the purpose of the global amino Cdc and why is it deprecated?
   - The global amino Cdc is used in several places within the SDK, but it is deprecated. The reason for its deprecation is not mentioned in the code.
   
2. What is the significance of the RegisterAminoMsg function and how is it used?
   - The RegisterAminoMsg function checks the length of a message name before registering the concrete message type with amino. It is not clear from the code how this function is used within the SDK.
   
3. When is the legacy package intended to be removed and what will happen when it is removed?
   - The legacy package is intended to be removed at some point in the future when the global Cdc is removed. It is not mentioned in the code what will happen when the legacy package is removed.