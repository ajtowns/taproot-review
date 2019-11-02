# More resources : Schnorr, Taproot, MAST

A quick [review](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-May/015951.html) of different consensus changes on the mailing list, with
advantages, drawbacks, among others Schnorr, Taproot, MAST, Graftroot, new sighashes.

# Schnorr : a dlog-based Efficient Signature Scheme

## Introduction

To get started, a high-level list of [Schnorr advantages](https://bitcoin.stackexchange.com/questions/34288/what-are-the-implications-of-schnorr-signatures/35351#35351) like :
- reduce onchain footprint
- n-of-n key aggregation
- k-of-n key aggregation
- batch validation
- better security proof than ECDSA

A gentle [introduction to Schnorr](https://diyhpl.us/wiki/transcripts/scalingbitcoin/milan/schnorr-signatures/) by Pieter Wuille at Scaling Bitcoin 2016 or this [one](https://github.com/WebOfTrustInfo/rwot1-sf/blob/master/topics-and-advance-readings/Schnorr-Signatures--An-Overview.md) by Christopher Allen with more cryptographic litterarure references. Another good [explanation](https://medium.com/cryptoadvance/how-schnorr-signatures-may-improve-bitcoin-91655bcb4744) by CryptoAdvance with more ECC context.

You can find a discussion of Schnorr security proofs on Adam Gibson [blog](https://joinmarket.me/blog/blog/liars-cheats-scammers-and-the-schnorr-signature/).

Hurdles and challenges of getting Schnorr right have been laid out in this sipa [conference](http://diyhpl.us/wiki/transcripts/blockchain-protocol-analysis-security-engineering/2018/schnorr-signatures-for-bitcoin-challenges-opportunities/).

Schnorr has been further reviewed on bip-schnorr announcement [ml thread](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-July/016203.html)

## Applications

Beyond simple signatures, multiple applications are explored like [efficient pubkey aggregation for multi-sig](https://eprint.iacr.org/2018/068.pdf), [scriptless scripts protocols](http://diyhpl.us/wiki/transcripts/realworldcrypto/2018/mimblewimble-and-scriptless-scripts/), [atomic signatures exchange](https://suredbits.com/payment-points-part-4-selling-signatures/), anonymous credentials exchange via [blind signatures](https://jonasnick.github.io/blog/2018/07/31/blind-signatures-in-scriptless-scripts/) and maybe [secure threshold sigs schemes](https://slides.com/real-or-random/schnorr-threshold-sigs-ces-summit-2019#/).

## Concurrent signatures schemes

Other new signature schemes have been discussed inside the community, most notably the [Boneh-Lynn-Shacham one](https://medium.com/cryptoadvance/bls-signatures-better-than-schnorr-5a7fe30ea716).
You can find a summary of pros and cons in this core-dev meetup [here](http://diyhpl.us/wiki/transcripts/2016-july-bitcoin-developers-miners-meeting/dan-boneh/) and [here](https://bitcoincore.org/logs/2016-05-zurich-meeting-notes.html), 
BLS signatures are more space-efficient but more computation-intensive and security assumption is looser.
If you want to go deeper an [implementation of BLS signature algorithms](https://github.com/Chia-Network/bls-signatures) has been made by the Chia team.

2-party aggregated pubkeys are also workable on [ECDSA](https://eprint.iacr.org/2017/552.pdf) but far harder to implement.
Further discussion on the LN mailing list about [2p ECDSA](https://lists.linuxfoundation.org/pipermail/lightning-dev/2018-April/001221.html)

## Implementations

Schnorr is [under implementation](https://github.com/bitcoin-core/secp256k1/pull/558) in bitcoin-core ECC library, libsecp256k1.
You can find a [bip-schnorr rust implementation](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-November/016506.html) of some applications
like aggregated sigs, accountable sigs and threshold sigs.

## Further improvement

If Schnorr is deployed, we may build on top of further applications like [cross-input signature aggregation](https://bitcointalk.org/index.php?topic=1377298.0), [non-interactive signature aggregation per-block](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2017-May/014272.html), [generalised taproot](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-July/016249.html) (more efficient taproot in non-cooperative case).

## Lightning

Lightning will reap a huge bonus from Schnorr adoption on the base layer. To go through a simple [introduction](https://jonasnick.github.io/blog/2018/09/04/schnorr-and-taproot-in-lightning/).

More in-depth:
* how to eliminate payment hash correlation ? Switch to [payment-points/scalar locks](https://lists.launchpad.net/mimblewimble/msg00086.html) and [theoretical discussion](https://eprint.iacr.org/2018/472.pdf)
* how to enable [Atomic Multi-Payment path while keeping the Proof-of-Payment](https://lists.linuxfoundation.org/pipermail/lightning-dev/2018-March/001100.html) ?
* what interactions between [LN-invoices and scriptless scripts](https://lists.linuxfoundation.org/pipermail/lightning-dev/2018-November/001489.html) ?
* how to enable [stuckless payments](https://suredbits.com/payment-points-part-2-stuckless-payments/) without resorting to script-update on the whole network or use sha256 midstate ?
* what about more expressive e2e contracts like [escrow](https://lists.linuxfoundation.org/pipermail/lightning-dev/2019-June/002028.html) or even [combination of payment-points type of contract](https://lists.linuxfoundation.org/pipermail/lightning-dev/2019-October/002213.html)

A quick skim about how LN transactions [could look like](https://lists.linuxfoundation.org/pipermail/lightning-dev/2019-May/001996.html) and even further ideas to redesign LN transactions in a [post-schnorr world](https://lists.linuxfoundation.org/pipermail/lightning-dev/2018-February/001031.html)

# MAST : Merklized Abstract Syntax Tree

Although the MAST idea has been merged into Taproot, it's important to understand MAST context to well understand Taproot design.

MAST is a combination of a compiler construction (an AST) and a cryptographic one (a Merkle Tree) to gain both privacy and expressivity for Script. While it has been historically known as Merklized Abstract Syntax Tree, the backcronym Merklized Alternative Script Trees has been [proposed](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-November/016500.html) to reflect idea refinements.
A gentle [introduction](https://bitcointechtalk.com/what-is-a-bitcoin-merklized-abstract-syntax-tree-mast-33fdf2da5e2f) by David Harding or a [more-in-depth introduction](http://diyhpl.us/wiki/transcripts/bitcoin-core-dev-tech/2017-09-07-merkleized-abstract-syntax-trees/) at a core-dev meetup.                                                                                                                                                                                                                                                                                    
[Merkle Trees](https://rubin.io/public/pdfs/858report.pdf) in themselves have been hard to get right as [some vulnerabilities](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/attachments/20190225/a27d8837/attachment-0001.pdf) affecting the one used in Bitcoin consensus have shown.         
                                                                                                                                                                                                                                                                                                          
The MAST debate has been focused on the [template-vs-generic approach](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-January/015623.html) for script upgrades.                                                                                                                             
                                                                                                                                                                                                                                                                                                          
## Generic-design : Merkle branch verification & tail-call semantics for generalized MASTs by maaku

Mark Friedenbach proposed a [script-based approach](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2017-September/014932.html) relying on the combination of modular mechanism to enable powerful MAST:
* [BIP 98 : Fast Merkle Tree](https://github.com/bitcoin/bips/blob/master/bip-0098.mediawiki) (maybe relevant in the discussion about Taproot merkle tree) and [ml thread](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2017-September/014935.html)
* [BIP 116 : MERKLEBRANCHVERIFY](https://github.com/bitcoin/bips/blob/master/bip-0116.mediawiki)
* [BIP 117 Tail Call Execution Semantics](https://github.com/bitcoin/bips/blob/master/bip-0117.mediawiki) and [ml thread](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-January/015530.html)

## Templated-design : Merkelized Abstract Syntax Tree

Johnson Lau on a templated-design a la P2SH via a Segwit bump version.
* [BIP 114 Merkelized Abstract Syntax Tree](https://github.com/bitcoin/bips/blob/master/bip-0114.mediawiki) and [ml announcement](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2017-September/014963.html) (with examples of further upgrades like re-enabling OP_CAT or OPMUL)

Further debtate on both alternatives and taproot interaction during this [core-dev meetup](https://diyhpl.us/wiki/transcripts/bitcoin-core-dev-tech/2018-03-06-merkleized-abstract-syntax-trees-mast/).

## Lightning

MAST-specific advantages for Lightning:
- in cooperative closing, make output and spending indistinguishable from other users
- feature-gating of advanced feature (like SIGHASH_NOINPUT) inside MAST scripts

# Taproot : Privacy preserving switchable scripting

[Announcement](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-January/015614.html) on the ml and following design discussion.

A [security proof](https://github.com/apoelstra/taproot) of taproot has been written by Andrew Poelstra, spec has been drafted and [announced on the ml](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2019-May/016914.html) around May 2019.

Some engineering sheenigans of taproot/schnoor have been raised in this [talk](https://jonasnick.github.io/blog/2019/06/25/secure-protocols-on-bip-taproot/) by Jonas Nick.

## Lightning

Already covered in MAST and Schnorr sections.

# Deployment & Engineering

## Sum-up threads by aj on Schnorr and Taproot design & deployment

* [March 2018](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-March/015838.html), with issues in coordinating both OP_RETURNVALID (aka OP_SUCCESS)and signatures aggregation
* [December 2018](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-December/016556.html), more on OP_SUCCESS design


## Schnorr and Taproot tooling 

Optech workshop material is a [great source](https://github.com/bitcoinops/taproot-workshop), it plays with [Miniscript](http://bitcoin.sipa.be/miniscript/), a language to write subset of Bitcoin Script in a structured way, enabling analysis, composition, generic signing...
Some work has been done by James Chiang to extend [Miniscript for Taproot](https://residency.chaincode.com/presentations/Taproot_Policy.pdf).

Finally, some [slides](https://people.xiph.org/~greg/gmaxwell_sfbitcoin_2015_04_20.pdf) on how to review cryptosystems, among other advices, aiming for 5 properties: accountability, usability, privacy, efficiency and composability.
