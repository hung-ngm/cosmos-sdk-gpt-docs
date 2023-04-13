[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/x/bank/keeper/invariants.go)

The code above is a part of the `cosmos-sdk` project and is located in the `keeper` package. The purpose of this code is to register and run invariants for the `bank` module of the `cosmos-sdk`. 

The `RegisterInvariants` function registers two invariants for the `bank` module: `NonnegativeBalanceInvariant` and `TotalSupply`. The `AllInvariants` function runs all the invariants of the `bank` module. 

The `NonnegativeBalanceInvariant` function checks that all accounts in the application have non-negative balances. It takes a `ViewKeeper` as an argument and returns an `sdk.Invariant`. It iterates over all balances in the application and checks if any of them are negative. If a negative balance is found, it increments a counter and adds a message to the error message. If the counter is greater than zero, it returns an error message indicating the number of negative balances found and the addresses of the accounts with negative balances. 

The `TotalSupply` function checks that the total supply reflects all the coins held in accounts. It takes a `Keeper` as an argument and returns an `sdk.Invariant`. It calculates the expected total supply by iterating over all balances in the application and adding them up. It then queries the actual total supply from the `Keeper` and compares it to the expected total supply. If they are not equal, it returns an error message indicating the expected and actual total supplies. 

The `AllInvariants` function runs all the invariants of the `bank` module. It takes a `Keeper` as an argument and returns an `sdk.Invariant`. It simply calls the `TotalSupply` invariant and returns its result. 

Overall, this code is important for ensuring the correctness of the `bank` module in the `cosmos-sdk`. It provides a way to check that all accounts have non-negative balances and that the total supply is correct. These invariants are crucial for maintaining the integrity of the blockchain and ensuring that transactions are processed correctly. 

Example usage of these functions can be seen in the `bank` module tests in the `cosmos-sdk` project. For example, in the `keeper_test.go` file, there are tests that check that the `NonnegativeBalanceInvariant` and `TotalSupply` invariants are working correctly.
## Questions: 
 1. What is the purpose of the `RegisterInvariants` function?
- The `RegisterInvariants` function is used to register the bank module invariants.

2. What does the `NonnegativeBalanceInvariant` function do?
- The `NonnegativeBalanceInvariant` function checks that all accounts in the application have non-negative balances.

3. What is the purpose of the `TotalSupply` function?
- The `TotalSupply` function checks that the total supply reflects all the coins held in accounts.