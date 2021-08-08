# Ethereum Assembly Debugger - Debug Loop Iterations


As I was working on different flavors of EVM interpreters built in the EVM, I quickly realized that debugging an EVM interpreter with current tools is more cumbersome than it needs to be. Debugging anything that has a recursive process, or is based on loops is like a Sisyphean task because you cannot just jump to the first opcode from a loop, at the 10th iteration.

For a long time, I used the Remix IDE debugger, which falls short at this task.
So, I improved the entire EVM debugging pipeline to accommodate this need.

What you see here are several independent components that can communicate with one another.
Everything is built with Marks Factory and Taylor. This left part is the Cometh EVM debugger and the right part is the Ethereum IDE, which allows us to compile, deploy and interact with Ethereum contracts and work with everything from Solidity and Yul code, to assembly, macroAssembly and raw bytecode. Both were presented in previous videos.

Now, you will see them working together. Any mark created with Marks Factory can now communicate with one another to create a powerful ecosystem.

Here I have a simple version of an EVM interpreter, written in our macroAssembly language. This is transpiled to EVM assembly, which is then transformed into bytecode. We deploy this bytecode to a test network.

Now, we want to interpret the bytecode and calldata for a contract, which I am going to fill in this raw calldata input. 
To use the debugger for this transaction, we select debug all or debug once. And click run.

And we get all the opcode steps. These are the opcodes in the execution order, so ordered by step index. We can also see the pc, the point in code index. If we select an execution step in the debugger, now we can see the exact assembly line that produced this opcode.

For example, this PUSH 0xa0, corresponds with this assembly line. Let's go to the main loop of our interpreter, where we read each opcode from the bytecode that we fed to our interpreter. So, this loop can be passed through thousands of times - each time an instruction is executed.

It starts from this tag_2 jump destination. Let's click on the line gutter. And the debugger will jump to the same position in code: it is the 55th byte in the contract bytecode and the 30th execution step.

Let's select the first loop instruction - this push 0x160 - the 31st execution step. 

We can now select at what loop count we want to go. We can see the state at opcode 56, at the 10th iteration. Which is at the .... execution step. And we can start debugging from here. At the 20th iteration. And we can start debugging from here, instead of blindly going through the opcodes by pure gut estimation.

You will not see this in other similar products, at this time.  

The Cometh Debugger, Ethereum IDE and Marks Factory are built by volunteers, for volunteers. Details in the description.



