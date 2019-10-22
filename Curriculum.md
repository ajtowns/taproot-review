# Taproot Review - Curriculum

## Intro & Taproot

* Week: Nov 3rd-9th
* What questions to ask while reviewing BIPs?
  * Do the goals make sense?
  * Does the design actually work and achieve the goals?
  * What are the tradeoffs? Do they make sense?
  * How are end users affected?
  * Do all the details fit together and work right?
* Bip-taproot, excluding “script path spending", “Signature validation rules”, “Constructing and spending Taproot outputs”
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
* Bip-taproot:
  * script path spending
  * Constructing and spending Taproot outputs
* Bip-tapscript, excluding “Rules for signature opcodes”, “Transaction digest”, “Resource limits”, “Rationale” sections 2, 4-14.
  * Motivation, Design
  * Specification
  * Script execution
* Optech workshop: https://github.com/bitcoinops/taproot-workshop
* Some things to consider:
  * How to do multisig (different MAST leaves, or CHECKSIGADD, or…)
  * How to change miniscript to cover MAST/script-path alternatives
  * How to change miniscript policy to deal with different costs of different execution paths depending on tree shape
  * Comparisons to other MAST approaches (eg BIP 114, BIP 116/117, BIP 98)

## Schnorr

* Week: Nov 17th-23rd
* Bip-schnorr without the Applications section
  * Motivation, Design
  * Key generation, Signing, Verification
  * Batch verification
  * Optimizations
  * Test vectors
  * Non-production Python reference implementation
* libsecp256k1: https://github.com/bitcoin-core/secp256k1/pull/558

## Signature Details and Resource Limits

* Week: Nov 24th-30th
* Bip-taproot
  * Signature validation rules
* Bip-tapscript
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
* Bip-schnorr Applications section
  * MuSig
  * Adaptor Signatures
  * Threshold Signatures
  * Blind Signatures
* Libsecp256k1-zkp: https://github.com/ElementsProject/secp256k1-zkp/blob/secp256k1-zkp/src/modules/musig/musig.md
* Scriptless scripts: https://github.com/ElementsProject/scriptless-scripts
* Things to consider:
  * Are these approaches secure?
  * Are the proposed APIs for these applications likely to result in secure implementations?
  * What are the limitations of these approaches? (eg, trusted parties, interactivity, lack of accountability as to who was compromised)
  * Are these ideas useful in practice, or do their limitations (eg threshold signatures are not accountable, so if some signers are compromised and funds are stolen, you cannot tell which signers were compromised) make them impractical?

## Upgrades

* Week: Dec 8th-14th
* Bip-taproot:
  * Leaf versions
  * Annex
  * Unencumbered v1 spends (non-32B size, p2sh)
* Bip-tapscript:
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
* Results of dev projects / proof of concept attempts as at the end of the previous week
* Collect questions, suggestions, problems discovered during review
* Capture overall summary as ACK / HOLD (overall we expect to find some things to improve, so likely this will be HOLD)
* Where to go from here

