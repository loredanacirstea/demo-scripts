# Mythos Evolution: WasmX contract execution for Transient Storage (the first modular, WASM contracts-based blockchain core)

You already know that we have built the most powerful execution engine that runs WebAssembly contracts.

What if we could use this execution engine to actually implement the blockchain itself? This is an idea that we fermented in our minds for years. But now, we can actually implement it. And we are not far from technical success.

Today, I will show you an internal demo of the first stages towards this goal. I have hooked our WasmX execution engine to execute WASM contracts on any kind of data storage. So, you can use it with on-chain data, but you can also use it with off-chain data. We will go into detail in future videos about the different types of chain data, that can be under consensus or not. But today, I will show you a demo where WasmX executes a blockchain core contract, that works with node-specific data.

This means that we can implement the consensus algorithm itself, fully, as a smart contract.

I am using a Solidity contract today. With a simple contract that can store a list of validators and a getter function. And can store the current node address. And a getter function for it.
This contract is added as a genesis precompile to the chain. The Solidity contract is compiled to EVM bytecode, which I then transpile to a WASM contract.

I initialized a local chain with 1 validator. And, through a special GRPC server that is connected to our wasmX execution engine, we can call the SetValidators function for example. And then GetValidators, for the result, which for now remains EVM ABI-encoded. Or, we can call SetCurrentNode and then GetCurrentNode, to get this node's address.

These GRPC methods, call the custom precompiled contract, with the correct calldata and function signature and return the result.

This is a preliminary stage. In future videos, you will see blockchains running on consensus algorithms like dPOS and raft, implemented as smart contracts. And much more.



