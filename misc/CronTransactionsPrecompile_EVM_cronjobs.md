# Cron Transactions Precompile for the EVM - cronjobs for the blockchain (demoed on Ethermint)

In a previous video, we talked about abstract accounts and how they can be used to enable smart contracts to send and pay for transactions.

One of their use-cases is having cron transactions that are like cronjobs for the blockchain. Any blockchain can implement cronjobs by adding a hook each time a block is added to the chain.

In the following demo, you will see a cron Precompile that I programmed to enable cron transactions for smart contracts.

Let's first look at what happens in the background. An account (and it can be an externally owned account or a smart contract) uses the cron precompile to register a cron transaction. For this, the contract provides the transaction data, such as target contract address, calldata, value, gasLimit. The cron precompile communicates with the cron module that can register and cancel cron transactions.

The cron module has a hook into an epochs module that announces it when an epoch has passed. The cron module checks if it has jobs to run for that type of epoch and runs them.

If the job is a transaction to be sent, it sends it through the abstract account module, which handles transaction fees and signatures. The abstract account module sends the transaction to the EVM module. The execution receipt is sent back to the cron module and emitted as an event.

This is the demo. We have a dApp with a direct interface to the cron precompile, for simplicity.

We have deployed a target contract that contains a value that can be incremented with the increment function. Right now, this value is 0.

We will register a cron transaction for a 30s epoch, with an id of 1, for this target contract address and this calldata - which is the signature of the increment function. 

Value 0, gasLimit 100000, gasPrice 10.
We confirm the transaction.
We have a log here telling us that the cron transaction has been set. And now we wait for the next 30s epoch to pass.
This is it, it should have executed our increment transaction. We wait for the cron transaction to be included in the next block and now we have a value of 1.
We wait for the next 30s epoch. Here it is.  We wait for the cron transaction to be included in the next block and now the value is 2.

Of course, in a production system, where anyone can register cron transactions, we can enforce longer epoch durations or require governance approvals for shorter durations.

You have seen a demo using trustless protocols
Abstract Accounts (demoed in a previous video) 
and an epochs module implemented with the Cosmos SDK
This epochs module can be implemented in any blockchain, including Ethereum
Transaction automation with respect to time: 
and it can be 1 time every hour, day, week, month, year

Cron transactions are a powerful tool for next-generation blockchains. 






