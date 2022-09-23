# MEV & PBS

PBS means "proposal-builder separation", that means that you allow a 3rd party
to construct an optimal block for your validator and use it for a slot.

In this setup, you validator is the block **proposal**, and this 3rd party is
a block **builder**.

That allows for more optimal block production (more txs per block), more fees,
MEV extraction.

The full proposal includes both PBS and crList for making sure potential
centralization of block building doesn't affect the platform neutrality. See
[crList proposal](https://notes.ethereum.org/@fradamt/H1ZqdtrBF) for more info.

## MEV-boost

MEV-Boost is the current live implementation by Flashbots, that uses APIs of
PBS to produce blocks for your validators. Just like with previous flashbots,
the advantage is that your blocks get more transaction fees. On the downside,
it means that your validator (since crList is not implemented now) doesn't have
any influence on what goes into your block.

You can read more about MEV-Boost and how to set it up there:

* [MEV Boost in a Nutshell / Flashbots](https://boost.flashbots.net)

* [What is MEV Boost?](https://www.alchemy.com/overviews/mev-boost)


