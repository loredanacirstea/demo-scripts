# Eventual Transactions for Cosmos SDK + EVM

In a previous video, we talked about abstract accounts and how they can be used to enable smart contracts to send and pay for transactions.
We also talked about cron transactions and how they use abstract accounts to send transactions as blockchain cronjobs.

Now, we will talk about eventual transactions. These are transactions that are triggered by blockchain events. From events emitted by a smart contract.

For example, a user sends a transaction calling a function of this EventfulContract. This contract emits a SendTransaction event, which is treated as a standard trigger for the client to programmatically send a transaction with data provided in the event arguments. The TargetContract address is an indexed even argument.
So, the transaction is processed by the EVM module, the state change is applied to the EventfulContract storage, the logs are added to the transaction receipt.
 The event is detected in a post-transaction processing hook, authorization is verified and the transaction is prepared by the abstract accounts module and broadcasted. It then enters the same process as any transaction, where its validity is checked first, then broadcasted to other peers, then included in a block, and executed as part of the chain. The transaction execution applies the state changes to the TargetContract and the transaction receipt is stored in the blockchain state.

And this is the prototype demo, with the EventfulContract interface and TargetContract. These are the contracts that we will use. To make it simple to understand, we have the TargetContract that stores a variable that can be read and updated.

The EventfulContract has a function that simply emits a SendTransaction event. Depending on whether the eventful transaction will be paid by the EventfulContract or the transaction origin, this event can contain additional signatures.

I deployed these two contracts. And now, let's call the EventfulContract with the address of the TargetContract, a value of 0, gasLimit 200000 and the calldata needed to change the TargetContract value from 0 to 3, using the signature of the set function.

We execute and confirm the transaction. We see the event was picked up by the node. And we wait for the eventual transaction to be processed.
Now, the value in the TargetContract is 3.


You have seen a mechanism for eventual transactions, that is
Trustless: using Abstract Accounts
You have seen transaction automation with respect to events
Based on the assumption of block-level finality
This may lead to:
- vicious “transactional explosions” that are hard to foresee; these eventual transactions require fees, just like any other transaction, so extra care is needed when event dependencies are created.
- but also to virtuous “circular economies” of dependent contracts
