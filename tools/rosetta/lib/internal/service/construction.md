[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/tools/rosetta/lib/internal/service/construction.go)

The `service` package in the `cosmos-sdk` project contains code that implements the Rosetta API for the Cosmos SDK. The Rosetta API is a standard interface for interacting with blockchain nodes, and it provides a set of endpoints for constructing, signing, and submitting transactions. The `service` package contains functions that implement these endpoints for the Cosmos SDK.

The code in this file defines a set of functions that implement the Rosetta API endpoints for constructing, signing, and submitting transactions. These functions take requests from clients, perform the necessary operations to construct, sign, and submit transactions, and return responses to the clients.

The `ConstructionCombine` function takes an unsigned transaction and an array of signatures and combines them to create a signed transaction. The signed transaction is returned to the client, which can then submit it to the network.

The `ConstructionDerive` function takes a public key and returns the account identifier associated with that public key. This function is used to derive the account identifier for a given public key, which is necessary for constructing and signing transactions.

The `ConstructionHash` function takes a signed transaction and returns the network-specific transaction hash for that transaction. This function is used to compute the transaction hash, which is necessary for submitting the transaction to the network.

The `ConstructionMetadata` function returns any information required to construct a transaction for a specific network, such as the chain ID, gas, and memo. This function is used to retrieve the metadata required to construct a transaction.

The `ConstructionParse` function is called on both unsigned and signed transactions to understand the intent of the formulated transaction. This function is used to parse the transaction and extract the operations and account identifiers associated with the transaction.

The `ConstructionPayloads` function takes an array of operations and the response from `ConstructionMetadata` and returns an unsigned transaction blob and a collection of payloads that must be signed by particular account identifiers using a certain signature type. This function is used to construct the transaction payloads that must be signed by the relevant parties.

The `ConstructionPreprocess` function is called prior to `ConstructionPayloads` to construct a request for any metadata that is needed for transaction construction, such as the account nonce. This function is used to preprocess the operations and retrieve any metadata required for transaction construction.

The `ConstructionSubmit` function submits a pre-signed transaction to the node. This function is used to submit the transaction to the network and returns an indication of whether or not the transaction was included in the mempool.

Overall, these functions provide a set of endpoints for constructing, signing, and submitting transactions using the Rosetta API. These functions are used by clients to interact with the Cosmos SDK and perform transactions on the network.
## Questions: 
 1. What is the purpose of the `OnlineNetwork` struct?
- The `OnlineNetwork` struct contains methods that implement the Rosetta API endpoints for transaction construction and submission.

2. What is the `ConstructionMetadata` method doing?
- The `ConstructionMetadata` method retrieves metadata required to construct a transaction for a specific network, such as gas price and gas limit, and suggests a fee based on that metadata.

3. What is the `ConstructionSubmit` method returning?
- The `ConstructionSubmit` method returns a transaction identifier response and metadata indicating whether or not the transaction was included in the mempool.