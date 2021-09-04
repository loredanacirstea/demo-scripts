
# The ups and downs of opcode costs. Part 1: Explaining EIP-2200, with EVM assembly


Storage costs on Ethereum. Once upon a time, things were simpler: if you wanted to occupy a free storage slot in a smart contract, you would pay 20000 gas units. If you wanted to change the value in an occupied storage slot, you would pay 5000 gas units. If you wanted to free a storage slot, you would get a refund of 15000 gas units. If you wanted to read a storage slot, you would pay 200 gas units.

Now, calculating storage costs in Ethereum is significantly more complicated. We have several EIPs that have changed and will change the way SSTORE and SLOAD are priced, like 2200, 2929, 2930, 3529.

The gas cost of a transaction must be a marker for the memory and computational resources needed to execute that transaction. These can change with time, especially when there is a growing user-base and much more state to read and write. And states are stored in slots.

In this video we will go into detail, into the storage costs rules brought by EIP-2200.

We will be using the terms original value, current value, and new value. The definitions of these terms are in EIP-1283, but we will see them in practice.

1)
Here is a first example. We are using EVM assembly code.
This first part is the smart contract constructor code. And the second part is the runtime part of the contract, which will be executed when a transaction happens.

I am deploying this short contract on my local testnet. And then, debug the transaction that executes this runtime code. So, we have all the execution steps here. We also have this transaction logged here, so we can replay it at any time.

Let's go to the first SSTORE. In this case, the original value is 0 - the 0x20 slot is empty. Our current value is also 0. The new value, in this case, is 0x3333. We are in ... this case (EIP2200) and it is simple: we pay the full storage costs for 1 slot: 20.000.

Then, we have another SSTORE. The original value is still 0 because this was the initial value when be began this transaction. The current value of the slot is now 0x3333. And the new value is the same as the current value. We are in this ... case, where nothing is changed, but the cost for an SLOAD (the reading operation), is deducted.

2)
Another example. Now, we have an SSTORE operation in the contract constructor, using the 0x20 slot. This means that after we deploy the contract, this storage slot will be occupied.
When we make a transaction now, our original value is 5. The current value is also 5. And the new value 0x3333. So, we are in this case, where we pay 5000 gas units for resetting the storage slot to another value.

3)
Next. We start in a similar way as before, but now we store 0. So, we effectively free the storage slot. We are in this case and we are refunded 15000. 

Now, another storage operation. The original value is still 5. The current value is now 0. And we want to store on the same slot, the value 0x04. We are in this case. The previous refund that we were given is now removed. And we pay for an additional SLOAD.

Another store on the same slot. Original value 5, current value 4, we change it to 0, effectively freeing the slot again. This time, because the slot was dirty - it was changed before in this transaction, we are refunded 15000 - SLOAD gas costs. We are in this case.

Next, we reset the slot value to 5. The same as our original value. And we are refunded the reset gas - SLOAD gas. But we still pay an SLOAD gas cost. We are in this case.

4)
The last case. I am looking at the second SSTORE. The original value is 0, the current value is 6 and the new value 0. So, we start with a free slot and we are resetting the slot to 0 in the same transaction. For the second operation, we are refunded 20000 - the SLOAD gas.

And these are all the cases. We had 4 smart contracts for testing.
And we have seen what happens when you do a simple SSTORE, setting a new value when you change a value when you set the value to 0 and clear the slot. And then, all the cases where you can have multiple SSTORE operations in the same transaction.

This was EIP-2200. If you want more videos explaining the rest of the EIPs and how they influence storage costs, leave a comment below.

