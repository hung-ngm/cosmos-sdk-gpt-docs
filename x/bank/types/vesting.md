[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/bank/types/vesting.go)

The `types` package in the `cosmos-sdk` project contains an interface called `VestingAccount` that is used for account vesting. Vesting is a mechanism that allows for the gradual release of funds over a period of time, rather than all at once. This is commonly used in situations where an individual or organization is granted a large sum of money, but the funds are subject to certain conditions or restrictions.

The `VestingAccount` interface defines several methods that are used to manage vesting accounts. The `LockedCoins` method returns the set of coins that are not spendable, which are defined as the vesting coins that are not delegated. To get the spendable coins of a vesting account, the total balance must first be retrieved and the locked tokens can be subtracted from the total balance. Note that the spendable balance can be negative.

The `TrackDelegation` method performs internal vesting accounting necessary when delegating from a vesting account. It accepts the current block time, the delegation amount, and the balance of all coins whose denomination exists in the account's original vesting balance. The `TrackUndelegation` method performs internal vesting accounting necessary when a vesting account performs an undelegation.

Finally, the `GetOriginalVesting`, `GetDelegatedFree`, and `GetDelegatedVesting` methods are used to retrieve information about the vesting account. `GetOriginalVesting` returns the original vesting balance of the account, `GetDelegatedFree` returns the amount of delegated coins that are not vesting, and `GetDelegatedVesting` returns the amount of delegated coins that are vesting.

Overall, the `VestingAccount` interface is an important component of the `cosmos-sdk` project, as it provides a way to manage vesting accounts and ensure that funds are released gradually over time. Developers can use this interface to create custom vesting accounts that meet the specific needs of their applications. For example, a project that requires a long-term investment strategy could use vesting accounts to ensure that funds are not released all at once, but rather over a period of several years.
## Questions: 
 1. What is the purpose of the `VestingAccount` interface?
- The `VestingAccount` interface is used for account vesting.

2. What is the `LockedCoins` method used for?
- The `LockedCoins` method returns the set of coins that are not spendable (i.e. locked), defined as the vesting coins that are not delegated.

3. What is the purpose of the `TrackDelegation` method?
- The `TrackDelegation` method performs internal vesting accounting necessary when delegating from a vesting account. It accepts the current block time, the delegation amount and balance of all coins whose denomination exists in the account's original vesting balance.