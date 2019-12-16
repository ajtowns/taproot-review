# Taproot BIP Review - Curriculum

_Note: a list of helpful [related resources](Resources.md) has been compiled
which can assist in reviewing._

## Intro & Taproot

* Week: Nov 3rd-9th
  * [Week 1 Notes](week-1.md)
* What questions to ask while reviewing BIPs?
  * Do the goals make sense?
  * Does the design actually work and achieve the goals?
  * What are the tradeoffs? Do they make sense?
  * How are end users affected?
  * Do all the details fit together and work right?
* Previous [issues](https://github.com/sipa/bips/issues?q=is%3Aissue) and [pull requests](https://github.com/sipa/bips/pulls?q=is%3Apr) may provide useful examples
* [bip-taproot][TR], excluding “script path spending", “Signature validation rules”, “Constructing and spending Taproot outputs”
  * Motivation, Design
  * Specification [partial]
  * Security
  * Backwards compatibility
* Bitcoin patches: https://github.com/sipa/bitcoin/commits/taproot
* Taproot security argument: https://github.com/apoelstra/taproot
* Optech Executive Briefing: https://bitcoinops.org/en/2019-exec-briefing/#the-next-softfork
* Some things to consider:
  * Background (gmax: https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-January/015614.html)
  * Break of ECC DL (eg via quantum computing breakthrough)
  * Cost of taproot outputs/spends versus p2pkh, p2wpkh, p2sh-p2wpkh
  * Requirement to use bech32 addresses

## Tapscript

* Week: Nov 10th-16th
  * [Week 2 Notes](week-2.md)
* [bip-taproot][TR]:
  * script path spending
  * Constructing and spending Taproot outputs
* [bip-tapscript][TS], excluding “Rules for signature opcodes”, “Transaction digest”, “Resource limits”, “Rationale” sections 2, 4-14.
  * Motivation, Design
  * Specification
  * Script execution
* Optech workshop: https://bitcoinops.org/en/schorr-taproot-workshop
* Some things to consider:
  * How to do multisig (different MAST leaves, or CHECKSIGADD, or…)
  * How to change miniscript to cover MAST/script-path alternatives
  * How to change miniscript policy to deal with different costs of different execution paths depending on tree shape
  * Comparisons to other MAST approaches (eg BIP 114, BIP 116/117, BIP 98)

## Schnorr

* Week: Nov 17th-23rd
  * [Week 3 Notes](week-3.md)
* [bip-schnorr][SCH] without the Applications section
  * Motivation, Design
  * Key generation, Signing, Verification
  * Batch verification
  * Optimizations
  * Test vectors
  * Non-production Python reference implementation
* libsecp256k1: https://github.com/bitcoin-core/secp256k1/pull/558
* Jonas Nick's x-only pubkeys article: https://medium.com/blockstream/reducing-bitcoin-transaction-sizes-with-x-only-pubkeys-f86476af05d7
* Paper on bad nonces (in ecdsa) https://eprint.iacr.org/2019/023.pdf

## Signature Details and Resource Limits

* Week: Nov 24th-30th
  * [Week 4 Notes](week-4.md)
* [bip-taproot][TR]:
  * Signature validation rules
* [bip-tapscript][TS]:
  * Rules for signature opcodes
  * Transaction Digest
  * Rationale, sections 4, 5, 7, 8 and 9.
* Things to consider:
  * Any chance of having different messages in different contexts result in the same digest? Extension attacks? Other ambiguities? Does the epoch make sense?
  * Are there any O(n^2) paths where n signatures might require different sets of n data having to be rehashed?
  * Can cached data be shared with segwit v0 signatures where possible?
  * Is this efficient for hardware wallets that want to have as little data and computation as possible?
  * Is there any way to exploit users using hardware wallets with this scheme?
* Bip-tapscript:
  * Resource Limits
  * Rationale, sections 10-14
* Things to consider:
  * What is the worst case resource usage? Is this worse than today?
  * What is the expected/average case resource usage? Is this worse than today?

## Schnorr Applications

* Week: Dec 1st-7th
  * [Week 5 Notes](week-5.md)
* [bip-schnorr][SCH] Applications section
  * [MuSig](https://blockstream.com/2019/02/18/en-musig-a-new-multisignature-standard/)
  * Adaptor Signatures
  * Threshold Signatures
  * Blind Signatures
* Libsecp256k1-zkp: https://github.com/ElementsProject/secp256k1-zkp/blob/secp256k1-zkp/src/modules/musig/musig.md
* Scriptless scripts: https://github.com/ElementsProject/scriptless-scripts
* [On the Security of Two-Round Multi-Signatures](https://eprint.iacr.org/2018/417.pdf) -- paper breaking original MuSig protocol/security proof, see also related [twitter thread](https://twitter.com/pwuille/status/1015317105116188672)
* [Insecure shortcuts in MuSig](https://medium.com/blockstream/insecure-shortcuts-in-musig-2ad0d38a97da)
* Things to consider:
  * Are these approaches secure?
  * Are the proposed APIs for these applications likely to result in secure implementations?
  * What are the limitations of these approaches? (eg, trusted parties, interactivity, lack of accountability as to who was compromised)
  * Are these ideas useful in practice, or do their limitations (eg threshold signatures are not accountable, so if some signers are compromised and funds are stolen, you cannot tell which signers were compromised) make them impractical?

## Upgrades

* Week: Dec 8th-14th
  * [Week 6 Notes](week-6.md)
* [bip-taproot][TR]:
  * Leaf versions
  * Annex
  * Unencumbered v1 spends (non-32B size, p2sh)
* [bip-tapscript][TS]:
  * `OP_SUCCESS`
  * unknown public key version
  * Rationale, sections 2 and 6
* Other proposals/ideas:
  * `SIGHASH_ANYPREVOUT` https://github.com/ajtowns/bips/blob/bip-anyprevout/bip-anyprevout.mediawiki
  * Re-enable opcodes, eg `OP_CAT`
  * Extended size math opcodes, eg 8-byte `OP_ADD`, `OP_MUL`
  * Commit to block at height via annex https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2019-May/016919.html
  * Change scripting language entirely, eg Simplicity https://github.com/ElementsProject/simplicity
* Things to consider:
  * Are there pitfalls to these upgrade methods?
  * Do these upgrade methods make the code too complex for the flexibility they provide?
  * Can the ideas mentioned above be implemented cleanly via the upgrade mechanisms we have?
  * Are there other interesting proposals, and can they be implemented cleanly too?

## Wrap-Up

* Week: Dec 15th-21st
  * [Week 7 Notes](week-7.md)
* Results of dev projects / proof of concept attempts as at the end of the previous week
* Collect questions, suggestions, problems discovered during review
* Capture overall summary as ACK / HOLD (overall we expect to find some things to improve, so likely this will be HOLD)
* Where to go from here


[TR]: https://github.com/sipa/bips/blob/bip-schnorr/bip-taproot.mediawiki
[TS]: https://github.com/sipa/bips/blob/bip-schnorr/bip-tapscript.mediawiki
[SCH]: https://github.com/sipa/bips/blob/bip-schnorr/bip-schnorr.mediawiki

