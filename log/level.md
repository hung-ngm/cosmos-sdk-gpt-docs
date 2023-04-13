[View code on GitHub](https://github.com/cosmos/cosmos-sdk/blob/main/log/level.go)

The `log` package provides functionality for logging messages at different levels of severity. This file contains a function called `ParseLogLevel` that parses a complex log level string and returns a `FilterFunc` that can be used to filter log entries based on their severity level and the module they belong to.

The `ParseLogLevel` function takes a string argument `levelStr` that contains a comma-separated list of module:level pairs, where each module is a string and each level is one of the following: trace, debug, info, warn, error, fatal, or panic. The function returns a `FilterFunc` that takes two string arguments: `key` and `level`. The `key` argument is the module name of the log entry, and the `level` argument is the severity level of the log entry. The `FilterFunc` returns `true` if the log entry should be discarded, and `false` otherwise.

The `ParseLogLevel` function first checks if the `levelStr` argument is empty and returns an error if it is. It then prefixes simple one-word levels with `*` and splits the `levelStr` argument into a list of module:level pairs. For each pair, it checks if the module name is unique and if the severity level is valid. It then creates a map that maps each module name to its corresponding severity level.

The `FilterFunc` returned by `ParseLogLevel` takes the `key` and `level` arguments and looks up the severity level for the module name in the map created by `ParseLogLevel`. If there is no severity level for the module name, it checks if there is a default severity level (`*`) and uses that if it exists. It then compares the severity level of the log entry to the severity level of the module and returns `true` if the severity level of the log entry is less than the severity level of the module.

This function is used in the larger project to filter log entries based on their severity level and the module they belong to. For example, if a developer wants to log only error messages for the `consensus` module and debug messages for the `mempool` module, they can use the `ParseLogLevel` function to create a `FilterFunc` that filters log entries based on these criteria. They can then pass this `FilterFunc` to the logger to filter log entries before they are written to the log.
## Questions: 
 1. What is the purpose of the `log` package in the `cosmos-sdk` project?
- The `log` package provides functions for parsing and filtering log levels.

2. What is the expected format of the input string for the `ParseLogLevel` function?
- The input string should be a comma-separated list of `module:level` pairs, with an optional `*` module for all other modules.

3. What happens if an invalid log level is provided in the input string for `ParseLogLevel`?
- If an invalid log level is provided, the function will return an error indicating the invalid level and the list of levels.