---
category: Block Chain
title: 'Block Chain Overview'

layout: nil
---

![Basic Blockchain Overview](https://s3-us-west-2.amazonaws.com/elixium-assets/Basic_blockchain.png)

The diagram above shows a simple representation of a block chain. Transactions
are grouped together into a block, hashed, then paired together and hashed
continuously until a [merkle root]() representing the transactions is calculated.

This merkle root is part of the block header, along with the index of the block,
the timestamp of the block, a nonce, the block's version, and the hash of the
previous block's header.

Because each block contains the hash of the block before it in its header, blocks
are interlinked with all previous blocks. Consequently, since the merkle root of
a blocks transactions are stored in the block header, if any transaction within
the block is changed, the merkle root will change, which will change the hash
of the block's header. Changing the block's header will also change the headers
of all the blocks following.

Transactions are also chained within blocks. Elixium wallet software may give
the illusion that elixir is sent from one wallet to another, or that an address
may have a balance associated with it, but really elixir is transferred through
transactions. Each transaction spends elixir that was previously received in one
or more previous transactions, i.e the output of one transaction will be used
as an input in a future transaction.

![Transaction Chaining Diagram](https://s3-us-west-2.amazonaws.com/elixium-assets/Transaction_chaining.png)
