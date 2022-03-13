# Generalized Replay Bridge with Ethereum VM, IBC (Cosmos) & Evmos

In previous videos, we have talked about implementing an IBC precompile for the Ethereum Virtual Environment and I have showed you a demo of a prototype built with Evmos.
Evmos brought the EVM and the Cosmos ecosystem together, so it is the best base layer to implement this IBC precompile, which gives access to the InterBlockchain Communication protocol from Cosmos, directly from the EVM.
With it, you will be able to create smart contracts that send messages to other chains with IBC support.

Another important use case is building inter-chain bridges using the already existing IBC infrastructure.
Today, you will see one of the types of bridges that can be done.
A Generalized Replay Bridge between two chains that have support for both the EVM and IBC. And I will demonstrate it on two Evmos chains.

A Generalized Replay Bridge can replay smart contract transactions on one or more chains, keeping state (of any type), in sync across chains. And this can be done selectively, for the smart contract state that you are interested in. For example, for keeping token balances in balance across contracts.

You do not need to replay all transactions of a contract, but only the state changes that matter. So, this technique also works well with rollup systems or with any application-specific chain that wants to keep its most important state in sync with the main chain. 

We have two Evmos chains running. The first one and the second one. And I am running the Hermes relayer, which will relay any packets sent from one chain to another, through IBC. I have already created a channel between them: channel-0.

On each chain, I have deployed a Bridge Main Contract and a TestContract - a smart contract that keeps a state which will be synchronized across chains. The Bridge Contract is the one that will change the state in the TestContract.
So I have a dApp here that works on the first chain and another dApp here that works on the second chain.

Syncing state is done in 3 steps, or 3 transactions: play, replay and finalize.
We will do the play transaction on the first chain: evmos_9000-1.
We need the name of the second chain, evmos_9000-2, the target address which is the address of the TestContract. In this setup, the contracts have the same address on both chains. And the calldata. This will call the "set" function in the TestContract and set a value of 5. The current value is 8 on both chains. 

The play transaction creates a new state hash for this target contract and stores it in a pending state, in the Bridge Main Contract. It also sends an IBC message to the second chain, with this hash. 
We click on play and confirm the transaction. And we see how Hermes picked up the message and now it should be relayed to second chain and we can see it here.

At this point, the value is still eight. And we need to do the replay transaction. Let's see the messages that we have for our chain. This is the IBC precompile interface. We are using channel-0 and we want to query the messages that the Bridge Main Contract has received. And this is the hash that was sent by the play transaction.

Now we do the replay. We get the id from the first chain, the target address is the TestContract address and the calldata is the same as we had in the play transaction.
What the replay transaction does: the Bridge Contract from the second chain checks the IBC messages that it has received, gets the state hash, and compares it with the state hash computed from the previous TestContract state hash and the new calldata. If they match, it applies the calldata to the target contract and sends back an IBC message to the first chain.
Let's do the replay transaction. We see the IBC message sent from this chain, picked up by Hermes, and received by the first chain.

Now, the state should be changed. And  it has a value of 5 on the second chain. On the first chain, the state remains the same: 8.
But now, we can go to the IBC precompile dApp, because the precompile is a smart contract, so we can query and call its functions.
And we want to get the messages for the Bridge Main Contract on the first chain.
And this is the state hash that we have received. It should be the same state hash that this Bridge Contract sent to the other chain, in the play transaction.

So, right now, we need to finalize the sync. 
And we will use the same calldata and we can finalize the sync.
What happens in the finalize transaction, is that ...
And now the value is 5.
The Bridge Main Contract check what IBC messages it has and compares the hash received in that IBC message to the pending hash that was stored when we did the play transaction with the computed hash from this calldata that we provide here. And if all 3 match, it applies the calldata on the target contract.

This is a Generalized Replay Bridge in 3 steps, for any kind of state changes, for any smart contract.

The pending state, also allows us to lock the states from other contracts, that depend on the synced state and implement a semaphore pattern.

The bridge has the same trust assumptions and security as using IBC and the Cosmos SDK
It is generalized: based on transaction replay.
It is extensible: it can be used to bridge more than 2 chains
It is compatible with EVM Data Service (EDS): for data mirroring and data sharding


There is a lot more to be shown, and further demos will follow.
