# Validators & Validator Clients

The validator client is the software that runs on top of a beacon node and
attests to the existing chain as well as produces blocks. It is similar to
a mining software for the old POW version of ETH.

Validator client != validator. Validator is a pair of (pubk, pk) that is used
to sign attestations and blocks. 

Each validator client could handle multiple validators. 
How many? There is no universal answer, but for eth mainnet,
most organizations put 100 or 200 validators per a single validator
client.


