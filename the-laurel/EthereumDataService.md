---
tags: EDS
---

# The Ethereum Data Service (EDS)

https://youtu.be/EI74YA1nbVo

The Ethereum Data Service is a gas-efficient solution for storing data on an EVM-compatible blockchain.

Built with EVM assembly, the database contract has minimal behavior gas costs. Items are packed efficiently for minimal storage costs.

You can get, set, delete records one by one or in bulk, which can decrease transaction costs considerably.

The Ethereum Data Service, or EDS, offers you an upgradable, browseable, selectable, indexed storage solution on the blockchain. Access control is decentralized. And most importantly, the data is typed. Decentralized applications and projects can share data together. And they can take the type data directly from the chain, for automatic type checking and data display. 

Users have a decentralized way to verify both validity of data and semantic meaning.

Now, the demo.
This is the master table, which contains all the table entries, including itself.

This is Table1. All the records are retrieved from the blockchain and, based on what type of fields the table has, they are decoded into what we see here. A greeting string, a name string, a vote number, and a color in hex format.

The fields themselves are stored in the database, as records. With name, type, and length.

Going back to table1, you can get, set, and delete records.
Let's modify one of the records. We select it and write Solidity instead of Taylor.
Now, the set transaction.

We see the record change in the table. 
Let's delete it. We execute the delete transaction. Notice we have 50 records. And the record is gone. Now, we have 49 records.


The Ethereum Data Service is available today, for provable volunteers.

