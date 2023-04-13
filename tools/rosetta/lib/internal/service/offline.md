[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/tools/rosetta/lib/internal/service/offline.go)

The `service` package in the `cosmos-sdk` project contains code related to the Rosetta API implementation. The code in this file defines an offline network that implements a subset of the construction API. 

The `NewOffline` function instantiates an instance of the offline network. It takes in a `NetworkIdentifier` and a `Client` as arguments and returns an instance of `OfflineNetwork` and an error. The `OfflineNetwork` struct implements the `DataAPI` interface in offline mode, which means that all the methods return errors because they cannot be used when offline. 

The purpose of this code is to provide a way to test the construction API of the Rosetta implementation when the network is offline. By implementing the `DataAPI` interface in offline mode, the code can simulate the behavior of the construction API without actually submitting transactions to the network. 

Here is an example of how this code might be used in the larger project:

```go
import (
    "context"
    "github.com/coinbase/rosetta-sdk-go/types"
    "cosmossdk.io/tools/rosetta/lib/types"
    "cosmossdk.io/tools/rosetta/service"
)

func main() {
    // Instantiate an instance of the offline network
    network := &types.NetworkIdentifier{
        Blockchain: "cosmos",
        Network:    "testnet",
    }
    client := // create a client
    offlineNetwork, err := service.NewOffline(network, client)
    if err != nil {
        // handle error
    }

    // Use the offline network to test the construction API
    metadataRequest := &types.ConstructionMetadataRequest{}
    metadataResponse, err := offlineNetwork.ConstructionMetadata(context.Background(), metadataRequest)
    if err != nil {
        // handle error
    }
    // ...
}
```
## Questions: 
 1. What is the purpose of the `NewOffline` function?
   
   The `NewOffline` function instantiates an instance of an offline network that supports a subset of the construction API but not the DataAPI.

2. What is the `OfflineNetwork` struct and what does it do?
   
   The `OfflineNetwork` struct implements an offline data API that constantly returns errors because it cannot be used if offline.

3. What is the purpose of the `crgerrs.ToRosetta` function used in the various methods of the `OfflineNetwork` struct?
   
   The `crgerrs.ToRosetta` function is used to convert errors from the `crgerrs` package to errors that conform to the Rosetta API specification.