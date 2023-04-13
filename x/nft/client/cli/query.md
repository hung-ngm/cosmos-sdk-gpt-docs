[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/nft/client/cli/query.go)

The code is a part of the cosmos-sdk project and provides a command-line interface (CLI) for querying the NFT (Non-Fungible Token) module. The NFT module is used for creating and managing unique digital assets on the Cosmos blockchain. The CLI provides various commands for querying NFTs, such as querying NFT classes, NFTs, owners, balances, and supply.

The `GetQueryCmd` function returns a `cobra.Command` that contains all the query commands for the NFT module. The `GetCmdQueryClass`, `GetCmdQueryClasses`, `GetCmdQueryNFT`, `GetCmdQueryNFTs`, `GetCmdQueryOwner`, `GetCmdQueryBalance`, and `GetCmdQuerySupply` functions implement the query commands for querying NFT classes, all NFT classes, an NFT, all NFTs, an NFT owner, an NFT balance, and NFT supply, respectively.

For example, the `GetCmdQueryNFTs` function returns a `cobra.Command` that queries all NFTs of a given class or owner address. The function takes an `address.Codec` as input and returns a `cobra.Command`. The command takes two optional flags, `--owner` and `--class-id`, to filter the NFTs by owner or class ID. The function uses the `nft.NewQueryClient` function to create a new query client and the `nft.QueryNFTsRequest` to query all NFTs of a given class or owner address. The function then returns the result in the protobuf format using the `clientCtx.PrintProto` function.

Overall, the code provides a convenient way to query the NFT module using the CLI. It can be used by developers and users to retrieve information about NFTs on the Cosmos blockchain.
## Questions: 
 1. What is the purpose of the `GetQueryCmd` function?
- The `GetQueryCmd` function returns a `cobra.Command` that contains all the query commands for the NFT module.

2. What is the purpose of the `GetCmdQueryNFTs` function?
- The `GetCmdQueryNFTs` function returns a `cobra.Command` that queries all NFTs of a given class or owner address.

3. What is the purpose of the `FlagOwner` and `FlagClassID` constants?
- The `FlagOwner` and `FlagClassID` constants are flag names used in the `GetCmdQueryNFTs` function to specify the owner and class ID of the NFTs to query.