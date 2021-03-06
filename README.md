# Smart Contract Application Layer Execution
#### (Work in progress) 

## Problem
Ethereum smart contract source code and transactions require storage, recomputation and validation by every node on the network including those who will never use the contract. This makes a smart contract blockchain impossible to scale since it must be restricted by the resources of the slowest node in the network. Ideally, each node should only process and store smart contracts that it would interact with or attempt to read. This scenario would allow far higher smart contract scalability as well as smart contract privacy.

## Proposal

I propose cheap smart contracts that do not require recomputation, storage or validation to be replicated on every node in the network. It is only validated on the machines of those who use the smart contract. Since only dApp users will recompute the smart contract, this allows for far higher gas limits. This can work on any blockchain that supports extra data in transactions. For the sake of simplicity, the proof of concept implementation will be based on Ethereum. In the future, it could also allow scalable Solidity smart contracts on top of the Bitcoin protocol. 
I'm still working on the PoC and I will release it on this repository when finished.

## How it should work

* Smart contract bytecode and ABI are shipped with frontend dApp code in addition to gas limit (as high as you want, 1000s of times higher than the Ethereum block limit) and maximum transaction length (for transactions downloaded from Swarm/IPFS).
* Web3.js watches the Ethereum blockchain for events including the hash of the shipped solidity bytecode as a topic.
* Found transactions on Ethereum can either contain the entire content or optimally refer to a Swarm/IPFS hash in order to retrieve large transaction content.
* To provide privacy, transaction data can be encrypted whether on the Ethereum chain or on Swarm. A private key would be shipped with the dApp code in order to allow only those with access to it to decrypt the smart contract transactions.
* Ethereumjs-vm runs and validates transactions found then finalizes a new smart contract state.
* Users of the smart contract never communicate. New users get the smart contract code with the dApp code then reconstruct its latest state by retrieving all events relevant to the smart contract from Ethereum.

## Possible use cases
* Smart contracts with very high gas limit and without gas fees.
* Private smart contracts
* Solidity smart contracts on top of the Bitcoin protocol or any other blockchain.
* ERC20 tokens fees paid with itself rather than Ether. This would work by forming a blockchain layer on top of SCALE.

## Challenges

 * The main challenge is to make this interoperable with the rest of the Ethereum ecosystem including the use of Ether and other smart contracts hosted on the chain. This is possible but requires further work.

## Contribution
* Please contact me on my email address nour@lamarkaz.com for questions, suggestions or ideas.
* PRs are very welcome
