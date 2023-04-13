[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/group/client/cli/prompt.go)

The `cli` package contains command-line interface (CLI) functionality for the Cosmos SDK. The `NewCmdDraftProposal` function generates a draft proposal JSON file that can be used to create a new proposal on the blockchain. The generated proposal JSON file contains only one message (skeleton). 

The function prompts the user to select the proposal type, which can be either `proposalText` or `proposalOther`. If the user selects `proposalText`, the generated proposal JSON file will contain only the metadata. If the user selects `proposalOther`, the function prompts the user to select the proposal message type from a list of available message types. The selected message type is then used to generate the proposal message, which is added to the generated proposal JSON file along with the metadata.

The `Prompt` method of the `proposalType` struct is responsible for prompting the user for the proposal metadata and generating the proposal and its metadata. The method sets the metadata, group policy address, proposer address, and messages field of the proposal. The metadata must be saved on IPFS, so a placeholder is set for the metadata field. The method returns the generated proposal, its metadata, and an error if any.

The `writeFile` function writes the input to the file. It is used to write the generated proposal JSON file and its metadata to disk.

Overall, the `NewCmdDraftProposal` function is a high-level command that allows users to generate a draft proposal JSON file that can be used to create a new proposal on the blockchain. The function is part of the larger Cosmos SDK project and is used to interact with the blockchain through the command-line interface.
## Questions: 
 1. What is the purpose of the `NewCmdDraftProposal` function?
- `NewCmdDraftProposal` generates a draft proposal JSON file that contains only one message (skeleton).

2. What is the purpose of the `proposalType` struct?
- The `proposalType` struct is used to prompt the proposal type values and return the proposal and its metadata.

3. What is the purpose of the `writeFile` function?
- The `writeFile` function writes the input to the file. In this case, it is used to write the generated draft proposal and metadata to their respective files.