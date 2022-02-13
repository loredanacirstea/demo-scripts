https://youtu.be/Mw8a9BVDhOw

Web3 is the decentralized and verifiable internet. Web3 is about data. It is about the most important data, that has enough value for someone to store it on-chain.

What do we want, as users from a Web3 browser?
To browse only what is important: state. 
Interoperability means that data is linked from one contract to another and the browser should be able to show link data and navigate from one contract to another. 
To insert, update and delete such data. And these operations should be as gas-efficient as possible, so we need compact data.

The browser should be able to create and render custom types - see our dType decentralized typing system project.

What do we want, as developers from the on-chain SDK of such a Web3 browser? 
ability to store behavior: upgradeable sub-contracts 
define data behaviors - and this is ensured by our Taylor interpreter 
higher-order functions for datasets such as map, reduce/fold, filter 
data is typed and new types can be defined 
Contract collaboration: multiple contracts can read and write to the same dataset

The SDK is available today with GPL3 and The Moral License

And now, a demo.

This is a contract of sets, which has a master set that registers all other sets. It also includes a set of types used in all the other sets.
Let's see this Profile set. It contains 5 records with values for 4 fields: a greeting, a person, votes, and color. The person value is actually a linked data value. It contains a reference to an entire other record, from another set and even, from another contract of sets.
We can click on record number 2 and the browser navigates to the referenced record. To Alice's data. 
This is in another contract and we can navigate to the main, master set and see what it contains - the master and type sets and a Persons set.

So, what will Web3 content be? 
It will be the essence of the old web. It will consist of linked data. Information is compacted to save gas. But, most importantly, it is decentralized.

We are releasing the SDK for browsing and composing the web3 as semantically-linked data.

Apply today for early access.
