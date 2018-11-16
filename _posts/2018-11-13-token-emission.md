---
category: Block Chain
title: 'Token Emission'
---

Block rewards in Elixium are determined by a smooth token emission algorithm.
Rather than distributing elixir in a logarithmic fashion (such as in Bitcoin),
Elixium block rewards scale down smoothly over time. Elixium will have a total
of 1 billion tokens in existence after the token emission period.

With a target emission period of 2,628,000 blocks (~ 10 years), we determine the
block reward for any given block with the following equation, where X is total
token supply, T is emission period (in blocks), I is block index, and S is the
sigma of the total token supply:

`BLOCK_REWARD = (X * max(0, T - I)) / S`
