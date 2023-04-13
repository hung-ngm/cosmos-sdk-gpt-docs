[View code on GitHub](https://github.com/cosmos/cosmos-sdk/blob/main/store/streaming/streaming.go)

The `streaming` package provides functionality for streaming data in the Cosmos SDK project. This file contains functions for managing plugins that can be used for streaming data. 

The `HandshakeMap` variable is a map that contains a handshake configuration for each supported streaming type. The `PluginMap` variable is a map that contains a plugin for each supported gRPC plugin. 

The `GetPluginEnvKey` function returns an environment variable key for a given plugin name. 

The `NewStreamingPlugin` function creates a new streaming plugin. It takes in a plugin name and a log level as arguments. It creates a new logger using the `hclog` package and then launches the streaming process. It uses the `plugin` package to create a new client and connect to the plugin via RPC. It then requests the streaming plugin and returns it. 

The `toHclogLevel` function converts a string log level to an `hclog.Level`. 

This code is used to manage plugins for streaming data in the Cosmos SDK project. Developers can use this code to create new streaming plugins and manage existing ones. For example, a developer could use this code to create a new plugin for streaming data from a specific data source. They could then use this plugin in their Cosmos SDK application to stream data from that source.
## Questions: 
 1. What is the purpose of this code and how does it fit into the cosmos-sdk project?
- This code is part of the `streaming` package in the cosmos-sdk project and provides functionality for launching and connecting to streaming plugins via RPC.

2. What are the supported gRPC plugins and how are they used?
- The supported gRPC plugins are defined in the `PluginMap` variable and currently only include the `abci` plugin. They are used to create a new streaming plugin via RPC.

3. How are handshake configs used and what is their purpose?
- Handshake configs are used to define the handshake protocol between the host and the plugin. In this code, the `HandshakeMap` variable contains a map of each supported streaming's handshake config, with the `abci` plugin being the only one currently supported.