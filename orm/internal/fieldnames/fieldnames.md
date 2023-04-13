[View code on GitHub](https://github.com/cosmos/cosmos-sdk/blob/main/orm/internal/fieldnames/fieldnames.go)

The `fieldnames` package in the `cosmos-sdk` project provides functionality for working with a list of fields that can be used as a map key. The `FieldNames` struct represents a list of fields with a comparable type, which is used primarily to lookup indexes. 

The package provides three methods for creating a `FieldNames` instance: `CommaSeparatedFieldNames`, `FieldsFromNames`, and `Names`. 

The `CommaSeparatedFieldNames` method takes a string of comma-separated field names and returns a `FieldNames` instance. If the field names contain spaces, the method normalizes them by splitting the string by commas, trimming the spaces from each part, and then joining them back together with commas. 

The `FieldsFromNames` method takes an array of `protoreflect.Name` values and returns a `FieldNames` instance. This method is useful when working with protocol buffer messages, as it allows you to create a `FieldNames` instance from an array of field names. 

The `Names` method returns an array of `protoreflect.Name` values that the `FieldNames` instance represents. If the `FieldNames` instance is empty, the method returns `nil`. 

Overall, the `fieldnames` package provides a simple way to work with a list of fields that can be used as a map key. This functionality is likely used throughout the `cosmos-sdk` project to lookup indexes and perform other operations on protocol buffer messages. 

Example usage:

```
import (
    "github.com/cosmos/cosmos-sdk/codec"
    "github.com/cosmos/cosmos-sdk/store/types"
    "github.com/cosmos/cosmos-sdk/x/auth/types"
)

// Define a list of field names to use as a map key
fieldNames := fieldnames.CommaSeparatedFieldNames("address,account_number,sequence")

// Create a new codec
c := codec.New()

// Create a new store
store := types.NewMemoryStore()

// Create a new account
acc := types.NewBaseAccountWithAddress(addr)

// Encode the account using the codec
accBytes := c.MustMarshalBinaryBare(acc)

// Save the account to the store using the field names as a key
store.Set(fieldNames.Names(), accBytes)
```
## Questions: 
 1. What is the purpose of the `FieldNames` type and how is it used in the `cosmos-sdk` project?
- The `FieldNames` type represents a list of fields with a comparable type which can be used as a map key, and it is primarily used to lookup indexes in the `cosmos-sdk` project.

2. What is the difference between the `CommaSeparatedFieldNames` and `FieldsFromNames` functions?
- The `CommaSeparatedFieldNames` function creates a `FieldNames` instance from a list of comma-separated fields, while the `FieldsFromNames` function creates a `FieldNames` instance from an array of field names.

3. What does the `Names` method of the `FieldNames` type return?
- The `Names` method of the `FieldNames` type returns the array of names that the `FieldNames` instance represents.