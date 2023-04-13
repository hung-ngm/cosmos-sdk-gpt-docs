[View code on GitHub](https://github.com/cosmos/cosmos-sdk/blob/main/codec/unknownproto/doc.go)

The `unknownproto` package provides functionality to "type check" protobuf serialized byte sequences against an expected `proto.Message`. This is useful for detecting potential issues such as unknown fields in the stream or mismatched wire types for a field, which could indicate mismatched services or even malicious actors.

The package provides an API signature similar to `proto.Unmarshal([]byte, proto.Message)` in the strict case. The `RejectUnknownFieldsStrict` function takes in the protobuf byte sequence, the expected `proto.Message`, and a boolean parameter indicating whether to allow unknown non-critical fields. If any unknown fields or mismatched wire types are detected, an error is returned.

Here's an example usage of `RejectUnknownFieldsStrict`:

```
protoBlob := []byte{...} // protobuf byte sequence
protoMessage := &MyProtoMessage{} // expected proto.Message
if err := RejectUnknownFieldsStrict(protoBlob, protoMessage, false); err != nil {
    // Handle the error.
}
```

It's recommended to use `RejectUnknownFieldsStrict` before invoking `proto.Unmarshal` to enforce the type checking features mentioned above.

By default, the package reports every single field that's unknown, whether it's a non-critical field or not. However, this behavior can be customized by setting the `allowUnknownNonCriticals` boolean parameter to `true` in the `RejectUnknownFields` function:

```
if err := RejectUnknownFields(protoBlob, protoMessage, true); err != nil {
    // Handle the error.
}
```

Overall, the `unknownproto` package provides a useful tool for ensuring the integrity of protobuf serialized byte sequences and detecting potential issues before they cause problems in the larger project.
## Questions: 
 1. What is the purpose of this code and how does it relate to the cosmos-sdk project?
    
    This code implements functionality to "type check" protobuf serialized byte sequences against an expected proto.Message to report unknown fields and mismatched wire types. It is a package called `unknownproto` within the cosmos-sdk project.

2. What is the difference between using `RejectUnknownFieldsStrict` and `RejectUnknownFields`?
    
    `RejectUnknownFieldsStrict` reports every single field that's unknown, whether a non-critical field or not, while `RejectUnknownFields` allows customization of this behavior by setting the boolean parameter `allowUnknownNonCriticals` to true.

3. Why is it recommended to use this package before invoking `proto.Unmarshal`?
    
    It is recommended to use this package before invoking `proto.Unmarshal` if you'd like to enforce the features mentioned above, such as reporting unknown fields and mismatched wire types.