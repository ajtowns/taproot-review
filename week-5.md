
# Week Five Info

> "Our third objective of smart contract design is privity, the principle that knowledge and control over the contents and performance of a contract should be distributed among parties only as much as is necessary for the performance of that contract. This is a generalization of the common law principle of contract privity, which states that third parties, other than the designated adjudicators and intermediaries, should have no say in the enforcement of a contract." - Nick Szabo, ["Formalizing and Securing Relationships on Public Networks"](https://firstmonday.org/ojs/index.php/fm/article/view/548/469-publisher=First) 1997-09-01

This week's topic -- applications of Schnorr signatures -- is quite a rabbit hole: you can probably keep diving into different applications of Schnorr for months or years, without running out of novel and useful things to think about. So don't be afraid to "blue pill" yourself at some point and wake up in your own bed, rather than forever lost in Wonderland!

## Schnorr Applications

The leaping off point for this week is

 * bip-schnorr [Applications](https://github.com/sipa/bips/blob/bip-schnorr/bip-schnorr.mediawiki#Applications)

As a gentle introduction, the idea is that a little maths (and a lot of care that what we do remains secure) we can set things up so that some smart contracts can be enforced on the blockchain just by publishing a signature. This has obvious scaling benefits -- when it works, you don't need any more data on the blockchain than the signature, which you needed anyway! -- but it also tends to have privacy benefits: you no longer reveal the details of the smart contract or what information is being passed around to third parties monitoring the blockchain.

In particular there are schemes proposed to do this for n-of-n multisig (MuSig), or k-of-n multisig (threshold MuSig), or a preimage reveal as used in lightning or to control atomic swaps (adaptor signatures), or conditional contracts based on an oracle's determination (discreet log contracts).

MuSig essentially provides a way of summing public keys to produce an aggregate public key (eg AB = "A + B") so that the holders of the individual private keys can produce partial signatures that can be summed to produce a valid signature that verifies against the aggregate public key.

The MuSig scheme is more complex than simple addition though, because there are a variety of subtle ways to in which these schemes can be broken. A [January 2018 blog post by Pieter Wuille](https://blockstream.com/2018/01/23/en-musig-key-aggregation-schnorr-signatures/) gives an overview of the scheme, and describes a simple attack that shows simple addition is not enough, but note the update from a year later that references a paper demonstrating that the simplified two-round MuSig scheme was also discovered to be insecure. More recently, [Jonas Nick has a blog post describing attacks on other variations on MuSig protocols](https://medium.com/blockstream/insecure-shortcuts-in-musig-2ad0d38a97da). A similarly recent [blog post by Adam Gibson describes Wagner's generalised birthday problem](https://joinmarket.me/blog/blog/avoiding-wagnerian-tragedies/) which is the technique that undermines some of these schemes that otherwise seem like they should be secure.

An [implementation of MuSig is included in libsecp256k1-zkp](https://github.com/ElementsProject/secp256k1-zkp/blob/secp256k1-zkp/src/modules/musig/musig.md).

MuSig essentially provides a way of doing n-of-n multisig, where everyone has to sign, but it seems to be possible to convert that to a k-of-n threshold multisig via an additional interactive setup protocol, and additional math when combining the partial signatures. Andrew Poelstra has a branch implementing threshold MuSig, including a [description of the protocol](https://github.com/apoelstra/secp256k1-mw/blob/2019-01-threshold/src/modules/thresholdsig/threshold.md) and a [design doc](https://github.com/apoelstra/secp256k1-mw/blob/2019-01-threshold/src/modules/thresholdsig/design.md) that discusses why it's hard to turn this idea into a workable API; there is an open pull request, namely [libsecp256k1-zkip PR#46](https://github.com/ElementsProject/secp256k1-zkp/pull/46).

Adaptor signatures are well worth reading about -- they allow a signature to be conditionally valid upon revealing the discrete log of a point. This allows for "preimage" reveals (the basis for lightning's hash-timelock-contracts), or revealing a private key, or even revealing a secondary signature. Jonas Nick's ["scriptless scripts" repo](https://github.com/ElementsProject/scriptless-scripts/blob/master/md/) has some write ups of techniques likes this, and there's more resources, mostly focussed on lightning network use cases, at the end of the [multi-hop locks](https://github.com/ElementsProject/scriptless-scripts/blob/master/md/multi-hop-locks.md) document in particular. [Discreet log contracts](https://adiabat.github.io/dlc.pdf) are an interesting variation that you also might find worth looking into.


