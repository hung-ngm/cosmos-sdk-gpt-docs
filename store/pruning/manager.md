[View code on GitHub](https://github.com/cosmos/cosmos-sdk/blob/main/store/pruning/manager.go)

The `pruning` package in the `cosmos-sdk` project contains the `Manager` type, which is responsible for handling the logic needed to determine when to prune old heights of the store based on the strategy described by the pruning options. The `Manager` type is an abstraction that provides a way to prune the store based on a given strategy. It has methods to set and get the pruning options, handle heights, and load pruning heights from the database as a crash recovery.

The `Manager` type has a `pruneHeights` field, which is a slice of `int64` values representing the heights to be pruned at the next pruning interval. The `pruneSnapshotHeights` field is a linked list of `int64` values representing the heights that are multiples of `snapshotInterval` and kept for state sync snapshots. The `snapshotInterval` field is an unsigned integer that represents the interval at which the snapshots are taken.

The `HandleHeight` method determines if the previous height needs to be kept for pruning at the right interval prescribed by the pruning strategy. It returns the previous height if it was kept to be pruned at the next call to `Prune()`, 0 otherwise. The `HandleHeightSnapshot` method persists the snapshot height to be pruned at the next appropriate height defined by the pruning strategy. The `GetFlushAndResetPruningHeights` method returns all heights to be pruned during the next call to `Prune()`. It also flushes and resets the pruning heights.

The `SetOptions` method sets the pruning strategy on the manager, and the `GetOptions` method fetches the pruning strategy from the manager. The `SetSnapshotInterval` method sets the interval at which the snapshots are taken. The `ShouldPruneAtHeight` method returns true if the given height should be pruned, false otherwise.

The `loadPruningHeights` function loads the pruning heights from the database as a crash recovery. The `int64SliceToBytes` function converts a slice of `int64` values to a byte slice. The `listToBytes` function converts a linked list of `int64` values to a byte slice.

In summary, the `Manager` type in the `pruning` package provides an abstraction to handle the logic needed for determining when to prune old heights of the store based on the strategy described by the pruning options. It provides methods to set and get the pruning options, handle heights, and load pruning heights from the database as a crash recovery. The `Manager` type is used in the larger project to manage the pruning of the store based on a given strategy.
## Questions: 
 1. What is the purpose of the `Manager` struct and how does it work?
- The `Manager` struct is an abstraction that handles the logic for determining when to prune old heights of the store based on the strategy described by the pruning options. It has methods for setting and getting the pruning strategy, handling heights and snapshots, and loading pruning heights from the database. It uses mutexes to synchronize access to the prune heights and prune snapshot heights, and flushes updates to disk to prevent data loss in case of a crash.

2. What is the purpose of the `NegativeHeightsError` type and when is it returned?
- The `NegativeHeightsError` type is returned when a negative height is provided to the `Manager`. It is used to indicate that the operation failed to get pruned heights due to an invalid input height.

3. How does the `HandleHeight` method determine whether a height should be pruned or not?
- The `HandleHeight` method determines whether a height should be pruned based on the pruning strategy and the value of the `KeepRecent` option. If the pruning strategy is not "nothing" and the height is greater than `KeepRecent`, it calculates the prune height as the difference between the height and `KeepRecent`. If the `snapshotInterval` is zero or the prune height is not a multiple of `snapshotInterval`, it adds the prune height to the list of prune heights to be pruned at the next pruning interval.