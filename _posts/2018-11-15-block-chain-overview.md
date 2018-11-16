---
category: Block Chain
title: 'Block Chain Overview'
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

Every transaction can create multiple outputs, such as when creating a transaction
to send elixir to multiple addresses. Each output of any given transaction can
only be used as an input to a transaction one time in the entire blockchain --
using the same output as an input in multiple transactions is invalid as this is
an attempt to spend the same elixir; this is classified as a [double spend]().

Outputs are directly tied to the transaction they are created in -- each output
has a TXOID which is the hash of the output followed by its index in the transaction's
outputs. An output that is at index 5 of the output list within a transaction
with the hash "9B96A1FE1D548CBBC960CC6A0286668" would have the TXOID of
"9B96A1FE1D548CBBC960CC6A0286668:5".

Since each output can only be spent once (used as an input once), each output
must be spent in full. An output with the value of 5 elixir can not be used as
an input once to use 3 elixir and then used as an input again to spend 2 elixir
in another transaction. This leads to a classification of two different types of
outputs: unspent transaction outputs (UTXOs) and spent transaction outputs. A
transaction is only valid if it solely consists of UTXOs as inputs.

![Transaction fee calculation](https://s3-us-west-2.amazonaws.com/elixium-assets/Transaction_fee.png)

Excluding [Coinbase transactions](), if the value of a transactions outputs
exceeds the value of its inputs, the transaction is invalid and will be rejected.
If the value of a transactions inputs exceeds the value of its outputs, the
difference will be claimed by as a [mining fee]() by the miner who includes the
transaction into a block.
