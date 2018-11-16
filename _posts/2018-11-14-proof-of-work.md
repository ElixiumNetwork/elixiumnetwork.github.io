---
category: Block Chain
title: 'Proof of Work'
---

The block chain is a distributed public ledger maintained by anonymous peers on
the network. In order to protect against malicious peers from adding to or
modifying the blockchain at will, Elixium requires that each block is crafted
by expending a significant amount of computing power, and by extension electricity.
This means that blocks can not be created instantaneously, and forces malicious
actors to have to expend more computing power to modify past blocks than honest
nodes which are just adding new blocks to the chain. This disincentivizes
malicious behavior by making it expensive to run attacks against the network, and
helps prevent against [sybil attacks]().

Chaining blocks together makes it impossible to modify any part of a transaction
or block without modifying all subsequent blocks, meaning that it becomes more
computationally expensive to modify a given block as more blocks are added to the
chain after it.

Nodes on the network will always build on the chain with the most computation
expended on it. This is not the chain with the most blocks, but rather the
chain with the highest cumulative difficulty -- a long chain can easily be created
when mined at a low difficulty, but when a chain is both long and has been mined
at a high difficulty, it can be inferred that the majority of the network's
hashing power has been expended mining on this chain, and this chain is the most
secure.

Difficulty is calculated using the [WWHM (Weighted-Weighted Harmonic Mean)]()
difficulty algorithm. The target solve time in Elixium is set to be 120 seconds,
so every 2 minutes, on average, a new block will be mined. Before each block is
mined, it's difficulty is calculated by finding the cumulative difficulties and
weighted cumulative solve times of the previous 60 blocks, and then solving for
difficulty (D') where T is target solve time, W is weighted solve times, and D is
cumulative difficulties in the following equation:

`D' = D / (61 / 2 * T) * W`

Difficulty is used to maintain the creation of new blocks to the target solve
time regardless of network hashrate fluctuations -- blocks should take 2 minutes
to mine whether there are 10 nodes on the network or 10,000. If the hashrate of
the network increases, the difficulty will scale accordingly. The same is true
in the case of a network hashrate decrease.

Nodes will only accept blocks if their hash was at least as challenging as the
blocks difficulty (which every node will calculate when receiving the block).
Because each block header must hash to a target threshold, and because each header
must contain the hash of the header of the block that preceded it, it requires
(on average) as much hashing power to propagate a modified block as the entire
Elixium network expended between the creation of the original block and the
current time. An attacker who holds 51% or more of the hashing power of the
network can execute such an attack where they can modify an existing block and
outpace the rest of the network to become the most computationally secure chain.

Since cryptographic hash functions are deterministic, meaning that given the
same input they will always produce the same output, the same block header will
always produce the same hash. In the process of mining, the miner is looking
to calculate a hash that is below a certain target threshold that is defined
by the block's difficulty, but if the block header does not change, the miner
will always get the same hash and will likely not get a satisfactory hash.
Because of this, the block header consists of a nonce value that can be freely
modified in order to generate different hashes. The block header is also fixed
in size. Since hash functions take longer to complete when given a larger input,
and since the transactions of a block must all be represented in the header,
miners would be disincentivized from including large amounts of transactions
in their blocks as each hash cycle would take longer than if they had included
minimal transactions in their block. In order to set an equal time per cycle,
transactions are represented within the header as a fixed size [merkle root]()
which need only be calculated once.
