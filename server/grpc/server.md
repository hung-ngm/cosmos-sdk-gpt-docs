[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/server/grpc/server.go)

The `grpc` package in the `cosmos-sdk` project provides functionality for setting up and starting a gRPC server. The `NewGRPCServer` function returns a new instance of a gRPC server that is correctly configured and initialized. The caller is responsible for starting the server using the `StartGRPCServer` function.

The `NewGRPCServer` function takes three arguments: `clientCtx`, `app`, and `cfg`. `clientCtx` is an instance of the `client.Context` struct, which contains information about the client's context, such as the chain ID and interface registry. `app` is an instance of the `types.Application` interface, which represents the application running on the server. `cfg` is an instance of the `config.GRPCConfig` struct, which contains configuration options for the gRPC server, such as the maximum message size.

The `NewGRPCServer` function first sets the maximum send and receive message sizes based on the values in the `cfg` argument. If these values are not set, it uses the default values from the `config` package. It then creates a new instance of a gRPC server using the `grpc.NewServer` function and sets the server codec to use the `ProtoCodec` from the `clientCtx` interface registry. It also sets the maximum send and receive message sizes on the server.

The `app` argument is then used to register the gRPC server with the application. Finally, the function registers the reflection service and the gogo reflection service with the gRPC server. The reflection service allows consumers to build dynamic clients that can write to any Cosmos SDK application without relying on application packages at compile time. The gogo reflection service allows external clients to see what services and methods the gRPC server exposes.

The `StartGRPCServer` function takes four arguments: `ctx`, `logger`, `cfg`, and `grpcSrv`. `ctx` is a context that is properly canceled or closed to indicate the server should be stopped. `logger` is an instance of the `log.Logger` interface, which is used to log messages. `cfg` is an instance of the `config.GRPCConfig` struct, which contains configuration options for the gRPC server, such as the address to listen on. `grpcSrv` is an instance of the `grpc.Server` struct, which represents the gRPC server to start.

The `StartGRPCServer` function first creates a new TCP listener using the address specified in the `cfg` argument. It then starts the gRPC server in a separate goroutine using the `grpcSrv.Serve` function. If the server fails to start, an error is returned. If the server starts successfully, the function blocks until it receives a signal to stop the server or the server fails. If the server is stopped, it is gracefully stopped using the `grpcSrv.GracefulStop` function. If the server fails, an error is returned.
## Questions: 
 1. What is the purpose of the `NewGRPCServer` function?
- The `NewGRPCServer` function returns a gRPC server that is correctly configured and initialized for use with a Cosmos SDK application.

2. What is the purpose of the `reflection` package being imported?
- The `reflection` package allows consumers to build dynamic clients that can write to any Cosmos SDK application without relying on application packages at compile time.

3. What is the purpose of the `StartGRPCServer` function?
- The `StartGRPCServer` function starts the provided gRPC server on the address specified in the configuration and blocks until the server is stopped or an error occurs. It also gracefully stops the server if the provided context is canceled or closed.