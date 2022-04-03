# Let's talk about fees (didactic analysis)

https://www.youtube.com/watch?v=XMlNtI-5ZPQ

Ethereum started with a simple incentivization mechanism for miners to include transactions in a block.

The user would submit a transaction with a maximum gasLimit for executing the transaction, for example, 100k and a gasPrice - for example 9 gwei.
Hence, the maximum fee that the user would pay in this case, would be 900k gwei (900 Szabo)

If the transaction only consumes 50k gas, then the miner is rewarded 50k gas * the gas price - 450k gwei. And the user gets refunded the rest of 50k gas * the gas price.

This is now called a legacy type transaction and it is still supported in Ethereum.

Then EIP-1559 came and said that miners should not get all the transaction costs. They should only get the priority fee that users set aside for them.

So, we start again from 100k gasLimit at a maximum price of 9gwei. Users are refunded the gas that has not been used.
And the rest is split into a base fee and a priority fee.
The base fee is the amount of gasUsed * by the current block's baseFee per gas unit, which is dynamic and can change from block to block, based on how full the blocks are.
The priority fee is the amount of gasUsed * by the priorityFee per gas unit. And this goes entirely to miners, to incentivize them to include your transaction faster.
The base fee is burned.

Now, let's look at how we can split these fees and make the most out of them. The user needs to pay them anyway.
Let's look at the baseFee, that is burned by eip-1559.
For analysis purposes, we can also split this into an intrinsic fee, which is the intrinsic gas cost of the transaction (around 21k gas units) * by the block baseFee per gas. In this case, 147k gwei.
And the cost of the actual code execution - 203k gwei.
We can take the intrinsic cost, which is very similar for each transaction and we can burn it or even fund core development - you can think of it as a core protocol burn or fee.

The execution gas cost can be directed to funding the development efforts for the smart contract called by the transaction. Or it can be split between miners/block proposers and developers.
But there is another category - service maintainers. This becomes especially relevant when you think about precompiles - for example, I previously demoed an IPFS precompile. And you could have a service fee attached to the precompile, that pins the file created and pays for storage.

Developer funding can be done at the protocol level with the advantage of having less friction and no additional fees incurred by users.
Transaction fee distribution to developers is not new - for example, it is currently being implemented on Evmos. But you have now seen a didactic analysis of how it can be done at a high-level, for Ethereum or any EVM-based chain.



