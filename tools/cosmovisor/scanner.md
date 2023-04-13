[View code on GitHub](https://github.com/cosmos/cosmos-sdk/blob/main/tools/cosmovisor/scanner.go)

The `cosmovisor` package contains a file watcher that monitors a file for updates and triggers an action when an update is detected. The file watcher is used to monitor an upgrade plan file that contains information about a planned upgrade to the system. The file watcher is initialized with a logger, the path to the upgrade plan file, and an interval at which to check for updates. 

The `newUpgradeFileWatcher` function creates a new instance of the file watcher and returns an error if the file path is invalid or the directory containing the file does not exist. The `MonitorUpdate` method starts the file watcher and returns a channel that is closed when an update is detected. The `CheckUpdate` method checks if an update is available by reading the upgrade plan file and comparing the height of the upgrade to the current height. If an update is available, the `needsUpdate` flag is set to true and the `MonitorUpdate` method returns a channel that is closed to signal that an update is available.

The `parseUpgradeInfoFile` function is used to parse the upgrade plan file and returns an error if the file cannot be opened or the file contents are invalid. The upgrade plan file is expected to be in JSON format and contain information about the planned upgrade, including the upgrade name and height. The upgrade name is normalized to lowercase to prevent case sensitivity errors.

Overall, the file watcher is a useful tool for monitoring files for updates and triggering actions when an update is detected. In the context of the larger project, the file watcher is used to monitor the upgrade plan file and trigger an upgrade when a new upgrade is available. This helps to ensure that the system is always up-to-date and running the latest version of the software.
## Questions: 
 1. What is the purpose of the `fileWatcher` struct and how is it used?
- The `fileWatcher` struct is used to monitor a file for updates and check if there is a new upgrade request. It is used to check if there is a new upgrade request and if it has the same name as the currently running upgrade.
2. What is the purpose of the `MonitorUpdate` function and what does it return?
- The `MonitorUpdate` function is used to monitor the file for updates and check if there is a new upgrade request. It returns a channel that signals when an update is detected.
3. What is the purpose of the `parseUpgradeInfoFile` function and what does it return?
- The `parseUpgradeInfoFile` function is used to parse the upgrade info file and return the upgrade plan. It returns the upgrade plan and an error if there is an issue with the file.