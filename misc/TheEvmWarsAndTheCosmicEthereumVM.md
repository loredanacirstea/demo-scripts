# The EVM Wars & the Cosmic Ethereum VM


We need an Ethereum Virtual Machine playground, where more community members can test and try out their EVM proposals.

The process of changing the EVM for Ethereum is hard. Mainly because the core developers are reluctant to introduce changes in a system that already holds billions. Which is understandable.
But this means that innovation is stifled and especially innovation that comes from independent people and projects who are not paid by the Ethereum Foundation. Because those who could have ground-breaking ideas encounter too much difficulty to implement, test, show and gather public for their work.

Of course, you can have both worlds and you can have a playground for EVMs, where it is easy to spin up a chain with a customized EVM (with, for example, additional opcodes and precompiles). But still take advantage of the security of the underlying system.

The old idea of Ethereum 2.0 with different execution engines wanted to offer this and it was amazing! But the plan has been delayed.

And this is where Evmos comes in. Evmos brings the EVM under the Cosmos ecosystem. But they want to do that in a modularized way, that anyone could use to spin their own custom EVM easily and be part of the Cosmos ecosystem and what it offers.

So, the Ethereum module would function on a chain with Tendermint consensus and IBC support - or the Inter-Blockchain Communication protocol. IBC gives the module a secure way to communicate with other blockchains and bridge data from one to another.
I will implement this one-way or even two-way communication between the EVM and the IBC.

Ok, but what does this mean for Ethereum? A new epoch that I would call the "The EVM wars". And the best EVM models and ideas from the community could be part of the next generation of Ethereum. 

For the past years I have been trying to push the boundaries of the Ethereum Virtual Machine by researching and implementing a decentralized type system - dType, a functional interpreted language based on recursion - Taylor, dTypeDB - a typed database, tools for continuous voting, for a volunteer-based project - The Laurel.

This work has pushed us to think about ways to make the EVM better. And in previous videos I have presented a series of precompiles proposals that will be expanded in the future. And Evmos is the first serious project that might allow us to do just that.

Here is a high-level walkthrough of the architecture that includes the EVM module. This is what Evmos offers for free: think of the EVM module as this M1 module here, which is a self-contained state machine, similar to other modules - like the authorization module, staking or governance modules and so on.

Modules each have their own 1 or more stores, for storing state. In the case of the EVM module, the stores are handled by the go-ethereum module. The EVM module built on top of go-ethereum, or geth and right now, follows the strict rules of the vanilla, Ethereum-core implementation.
In general, modules can write in the stores of other modules too, following the object capabilities model.

And they can communicate with other modules, by routing messages through the BaseApp component.

Transactions grouped by blocks are received from the networking and consensus layer provided by Tendermint and are extracted in BaseApp.
The communication interface between Tendermint and the chain logic is done through the ABCI - the Application BlockChain Interface. Some of the most important messages are CheckTx, DeliverTx, StartBlock, EndBlock and Query. Queries have a different pathway than the messages that effectively change the transactions and blocks. 

Queries are decoded and go through the grpcQueryRouter, to the query service of the module they were intended for.

The other messages are decoded and sent through the MsgServiceRouter to the message service of the module they are intended for. There, they will be procesed by the module itself and in the case of the EVM module, go-ethereum handles most of that processing, under the hood.

Each module also has its own UI and it can communicate with the BaseApp through an internal gRPC query service.

In future videos we will look in more depth into the EVM module of Evmos and how it is implemented.

You have seen an example of architecture that allows using the Ethereum Virtual Machine as part of the Cosmos ecosystem. 
Evmos offers:
* Trustless communication with other chains on IBC
* PoS today
* Fast finality guarantees
* Community governance
* Tokenomics and strategic token policies
* It can host other engines
  * and EVM variants (see precompiles videos)
  * and can also integrate CosmWasm - a Wasm-based engine for smart contracts.

But if you want to know more about Evmos, you can go to their site or pay them a visit to ETH Denver if you are going.

The next generation of mechanisms for governing humanity will be based on decentralization of effort and responsibility. What started with Bitcoin was continued by Ethereum 1 and it is furthered by Evmos ahead of Ethereum 2. So, let's decentralize together the effort on Research & Development for the EVM.


