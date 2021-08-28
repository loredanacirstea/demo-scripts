# Hi, Jack! browser wallets on IPFS


You can hijack any dApp deployed on a decentralized storage gateway.

IPFS, or the Interplanetary File System and other decentralized storage solutions bring web3 content to web2. The gateways serve any IPFS content under the same domain, so this opens up both interesting interoperability and hijacking possibilities.

I am using the Marks Factory project, which is published on IPFS. I programmed an application that wraps any dapp deployed on IPFS in an iframe and hijacks the web3 provider. I named this wrapper "Jack".
Here, we have loaded the Uniswap app, using its IPFS hash, inside Jack. So, both Uniswap and Jack live on IPFS and are loaded through the same IPFS gateway.
In a previous video, I showed you how this technique can be used to attach an EVM debugger, and I debugged the Uniswap dApp interactions right from the UI.

But, you can use it to hijack the transactions sent to your browser wallet. Now, hijacking is stopped and we are preparing an Uniswap exchange of ETH to Wrapped ETH.

We switch on hijack once transaction, so only our swap transaction is caught. And when we make the transaction, a fake Metamask appears. This time, it is just a screenshot and my dApp provider has obvious UI elements. This demo is not for giving a complete hijacking recipe: only to increase awareness and demo a multi-use product.

Next videos we will see other surprising uses of Jack.



