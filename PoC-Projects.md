# Proof of Concept Projects

These are some ideas for proof of concept projects to explore schnorr and/or taproot in more depth.

 * LN payment points and scalars
 * LN 2-of-2 schnorr MuSig construction for channel open/close
 * Off-chain 2-of-3 key rotation
 * Liquid-style 11-of-15 multisig
 * Taproot/schnorr support for python-bitcoinlib (etc?)
 * Taproot/schnorr support for bitcoinjs-lib?
 * ...see below for ideas from the RSVP survey...

Note: Optech has developed a [schnorr & taproot library](https://github.com/bitcoinops/taproot-workshop), which can be used to prototype many of the proof-of-concept projects suggested above. The library features a Schnorr and MuSig implementation as well as methods to construct taproot outputs from various types of Tapscripts. The documentation is written in the form of interactive Jupyter notebooks, which provide thorough examples on how to use the library.

* Maybe Submarine Swaps (only the on-chain part)
* Perhaps a multisig app
* An OpenBaaar style 2-of-3 multisig where the 3rd party (moderator) would not ever know they are involved until a dispute is open, and the tapscript & tweak is sent to them to participate.
* Already on the sheet, but putting together a Liquid taptree+spend would be interesting
* I've been looking into Miniscript too so would be cool to use it in the context of Taproot
* Miniscript extension for Taproot/Tapscript. I have considered how Policy to Taproot compiler could work, policy can be extended with privacy constraints, so certain expressions do not share the same branch. See: https://youtu.be/EdRm_mnoCWc?t=1139
* Time preference when measured solely in terms of bitcoin is extremely interesting to me, and specifically how such a signal, may be aggregated and propagated in a trustless decentralized way. Tamas' work on https://github.com/defiads/defiads (an implementation of a more generic concept called a "side memory" for bitcoin as opposed to side chain) is something I'm quite interested in which is in the direction of time preference. I would like to better understand how something like defiads might perhaps be better implemented using schnorr/taproot . As far as proof of concept goes I am basically interested in seeing if something like a trustless/distributed version of https://lightningbutton.network could be implemented.
* Statechains
* We're developing on-chain financial products, currently using  Ethereum, but would love to move to Bitcoin-only on-chain derivatives. Interested in exploring how this might work.
* Replacing LN per-hop hashlock with payment points
* Taproot/Tapscript prototype in https://github.com/acinq/bitcoin-lib
* MuSig for Lightning channel messages
* Payment points / Anonymous Multi-Hop Locks for Lightning (maybe a bit ambitious)
* Explore how miniscript like policy languages get mapped to taproot specific features, especially from the point of view of improving privacy, i'm mostly interested better understanding the high level composability of taproot
* Probably a tx creation and signature spend on regtest
* Musig hardware wallet . Maybe 1 hardware wallet where secure element and mcu each have a key. Insurance against malicious closed source secure element.
* We would try our multisig wallets, spend to a taproot protected address and check we can spend onwards, on regtest
* Build a scriptless script atomic swap PoC between Grin and Bitcoin
* Off-chain 2-of-3 key rotation
* Signet network, btcdeb support
* Chaumian CoinJoinXT https://zmnscpxj.github.io/bitcoin/coinjoinxt.html
* Could be interesting to do DLC with Schnorr and Taproot
* Taproot/schnorr support for python-bitcoin library
* some DLC stuff for P2P derivatives
* code to work with for Schnorr signatures in python-bitcointx
* Yes, something combining MuSig with Discreet log contracts.
* a multisig escrow wallet
* Lightning commitment transactions
* Integration of Taproot into a wallet
* We are already building layer 3 solutions like RGB (github.com/rgb-org/rgb-spec) and generic LNP/BP standards (github.com/lnp-bp/lnpbps), so I will be making sure that they are matching Schnorrs/Taproot and be updating them wherever is required
* bitcoinjs-lib
* 
