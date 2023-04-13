[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/gov/codec/doc.go)

The `codec` package in the `cosmos-sdk` project provides a singleton instance of Amino codec that is used to register any concrete type that can later be referenced inside a `MsgSubmitProposal` instance so that they can be (de)serialized properly. 

Amino types should be registered inside this codec within the `init` function of each module's `codec.go` file. For example, the following code registers the Amino codec for the `govcodec` and `groupcodec` modules:

```
func init() {
    // ...
    RegisterLegacyAminoCodec(govcodec.Amino)
    RegisterLegacyAminoCodec(groupcodec.Amino)
}
```

The codec instance is put inside this package and not the `x/gov/types` package in order to avoid any dependency cycle. 

In summary, this package provides a centralized location for registering Amino codecs for concrete types used in `MsgSubmitProposal` instances. By registering these codecs, the `MsgSubmitProposal` instances can be properly (de)serialized.
## Questions: 
 1. What is the purpose of this code?
    
    This code provides a singleton instance of Amino codec that should be used to register any concrete type that can later be referenced inside a MsgSubmitProposal instance so that they can be (de)serialized properly.

2. How should Amino types be registered within this codec?
    
    Amino types should be ideally registered inside this codec within the init function of each module's codec.go file using the RegisterLegacyAminoCodec function.

3. Why is the codec instance put inside this package and not the x/gov/types package?
    
    The codec instance is put inside this package and not the x/gov/types package in order to avoid any dependency cycle.