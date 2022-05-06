
# InterChain Transactions for EVM Smart Contracts in Cosmos


InterChain Transactions, interchain compatibility, and composability, interchain applications are the next major feature that any blockchain will need to have, unless they want to disappear.

The following demo is done with tools from the Cosmos ecosystem, but if Ethereum 2 will implement the IBC precompile that I demoed in a previous video, then today's example could be possible also on Ethereum. Bridging these two ecosystems: Ethereum and Cosmos will bring the next generation of blockchains: modular, flexible and interconnected.

Cosmos has recently added interchain accounts to its sdk. This means you can use one Cosmos chain to control a shadow account on another Cosmos chain. Interchain accounts can be used now with any Cosmos transactions. A user can make interchain transactions limited by what the blockchain developers have decided as features.

Today I am showing you a prototype of how you can use interchain accounts for EVM-powered Cosmos chains. This is the first time anyone designed and implemented such a demo.
The Ethereum Virtual Machine gives freedom and responsibility to any developer to use interchain transactions.
You will see part 1 of a Replay Bridge smart contract, built on a fork of Evmos, with interchain accounts integration and an interchain accounts precompile.
So, any contract could use this interchain account precompile, within the security measures that we will talk about in a later video.

This is a diagram of the prototype that you will see next.
A normal user or a smart contract, like the bridge contract mentioned earlier, uses the interchain accounts precompile to send a transaction.
This transaction is then sent to the InterTx module, which is a Cosmos module that I programmed. The InterTx module signs the EVM transaction with an abstract account that corresponds to the InterChainAccount of the account that triggers this transaction, wraps this transaction into a Cosmos message and submits it to the InterChainAccount module to be relayed by IBC, to chain 2.
Here, the message is received by the InterchainAccount module and then sent to the InterTx module. The Ethereum Tx is unwrapped and sent to the EVM module to be executed. The gas for executing the transaction on chain2 is paid from the InterChainAccount balance. The receipt is then sent back to chain1, and to the account that triggered this transaction.

And this is the demo.
I have 2 Evmos chains here: a controller chain on the top -chain1 and a host chain on the bottom - chain2. and a relayer between them.
And I have an interchain account already created between the chains. 
I have a bridge contract deployed on the chain1 evmos-9000_1 and a target contract deployed on chain2 evmos-9000_2.
And we will copy the address for the target contract.
We can see that the target contract has a state with a value of 0. We will be changing this state with an interchain transaction from chain 1.

For demonstration purposes, this example is made to be flexible. We take the target contract address and the chain id for the second chain.
Value of 0, gas limit of 100000
The calldata that we want to run on the target contract on chain2, which calls the set function with a value of 2. 

We trigger the transaction.

And we see the IBC packets being relayed and being processed.

And now we get a value of 2 on the second chain.


You have seen a prototype for sending transactions from one EVM chain to another
Uses Interchain Accounts and IBC
Can be used as a base for:
trustless bridging
state mirroring
multi-chain dApps
multi-chain singleton OS
Usable by Ethereum 2 with the IBC Precompile (developed and demoed by me previously)







