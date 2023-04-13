[View code on GitHub](https://github.com/cosmos/cosmos-sdk.git/orm/model/ormtable/util.go)

The `ormtable` package in the `cosmos-sdk` project contains two functions: `prefixEndBytes` and `inclusiveEndBytes`. These functions are used to generate byte slices that can be used as the end keys in range queries.

The `prefixEndBytes` function takes a byte slice `prefix` as input and returns a new byte slice that would end a range query for all byte slices with the same prefix. The function first checks if the length of the prefix is zero, in which case it returns `nil`. Otherwise, it creates a new byte slice `end` with the same length as the prefix and copies the prefix into it. The function then enters a loop that checks if the last byte of `end` is equal to `255` (the maximum value for a byte). If it is not, the function increments the last byte of `end` by one and breaks out of the loop. If the last byte of `end` is `255`, the function removes the last byte from `end` and checks if the length of `end` is zero. If it is, the function returns `nil`. Otherwise, the function continues the loop. The loop terminates when the last byte of `end` is not equal to `255`.

Here is an example usage of `prefixEndBytes`:

```
prefix := []byte("hello")
end := prefixEndBytes(prefix)
// use end as the end key in a range query for all byte slices with the prefix "hello"
```

The `inclusiveEndBytes` function takes a byte slice `inclusiveBytes` as input and returns a new byte slice that would end a range query such that the input byte slice would be included in the query. The function simply appends a `0x00` byte to the input byte slice.

Here is an example usage of `inclusiveEndBytes`:

```
bytes := []byte{0x01, 0x02, 0x03}
end := inclusiveEndBytes(bytes)
// use end as the end key in a range query that includes the byte slice {0x01, 0x02, 0x03}
```
## Questions: 
 1. What is the purpose of the `prefixEndBytes` function?
- The `prefixEndBytes` function returns the byte slice that would end a range query for all byte slices with a certain prefix, handling the case where the last byte of the prefix is FF without overflowing.

2. What is the input and output of the `inclusiveEndBytes` function?
- The `inclusiveEndBytes` function takes in a byte slice and returns the byte slice that would end a range query such that the input would be included.

3. What package does this file belong to?
- This file belongs to the `ormtable` package.