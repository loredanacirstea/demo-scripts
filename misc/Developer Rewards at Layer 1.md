# Developer Rewards at Layer 1 (a better EIP-1559)

Crypto value propositions for projects revolve around mining or staking rewards, creating a token for the project that may or may not have intrinsic value or retaining fees at smart contract level.
Tokens and smart contract fees add friction and increase gas costs.
But there is another way - reward developers at layer1 level, from the gas cost that the user already needs to pay.

This is a sustainable idea that is planned by the Evmos team (an EVM-based Cosmos chain) and I am currently implementing it.

Ethereum has introduced EIP 1559, where the dynamic block base fee, multiplied by the transaction's used gas is burned. So, instead of being burned entirely, you can send some of that gas to the contract deployer.
This can amount to an acceptable and deserved revenue stream for frequently used smart contracts.

This is a dapp with two contracts with the same functionality. The contract on the left has been registered in the developer program and the contract on the right, has not.
Both contracts were deployed by the same address.
And we can get the deployer's current balance plus the difference between his current balance and his previous balance.

We are running on a local evmos node with developer fee rewards enabled.

Now, let's make a transaction that will just set a variable in storage.
We will use a priority fee of 1 gwei - this goes the miners, or validators in this Evmos's case.

This is the amount of gas used. 
This is the effective gas price paid and it is the sum between the block's base fee and the priority fee for the validator.

On a local testnet we generally get low base fees, because it decreases with each block that does not contain transactions. On Ethereum mainnet, the base fee is around 100 gwei right now, which is 100 billion wei.

The base fee multiplied by gasUsed is what is burned by Ethereum. On Evmos instead, this fee is split between validators and developers and of course, part of it could also be burned if decided by governance.

In this implementation, 50% of this amount goes to the contract deployer. So, if we query the deployer balance, we should see a diff with this expected amount. And here it is. The contract deployer got half the fee.

Now, let's try the second contract, that has not been registered.
And we see no change in the deployer's balance.

We can try out another function that stores multiple variables. So, in this case, the gas used is higher and the developer reward is higher.
And we can see the deployer balance was increased with the expected amount.

You have seen an example of how developer rewards work.

With governance of percentages, you can change how much the developer, validator receive from this base fee-based amount. Or how much of it gets burned.

The developer can select the wallet address where his funds are collected.
And this feature is generalizable for any contract
It should be of interest to Ethereum and all EVM-compatible chains: EIP-1559 burned fee will benefit developers instead of being lost.
It is a fairer implementation, that rewards those who bring value to the chain in a frictionless way. And if Ethereum will be interested, I would love to implement this for the community.

Based on this idea, I will present some personal contributions in future videos:
the same type of rewards, but for EVM precompiles
and a developer claim & challenge mechanism for bytecode source

The last idea is a proposal to send the rewards to the rightfull deployer in case the code was stolen and deployed by an effort thief.
















