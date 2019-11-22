# Week Four Info

TODO: QUOTE

Welcome to Week 4. We are now past the halfway point and have entered the phase where we'll be zooming in on some of the more of the details and their implications.

## Results from Week Three
TODO: SURVEY RESULTS

We dropped to a single Q&A slot this week and it seems like questions and discussion are being spread out in the IRC channel with experts jumping in to answer questions as they pop up. We encourage you to continue to ask questions at any time and experts will give you an answer when they can. (If you can't stay connected, you can use the logs to catch answers to your question, but it might be wise to mention that you'll be doing so to avoid people thinking there's no point responding because you've left the channel.)

There have been a few more suggested improvements for the BIPs, including [PR#154](https://github.com/sipa/bips/pull/154), [#152](https://github.com/sipa/bips/issues/152), and [PR#148](https://github.com/sipa/bips/pull/148). Keep them coming...

## Signature details

Following our review of the schnorr BIP, we will focus on reviewing the signature validation rules(https://github.com/sipa/bips/blob/bip-schnorr/bip-taproot.mediawiki#Signature_validation_rules) including the validation rules and the valid `hash_types` and the similar semantics of the [BIP143](https://github.com/bitcoin/bips/blob/master/bip-0143.mediawiki) sighash types save for a few exceptions described at the end of the [transaction digest](https://github.com/sipa/bips/blob/bip-schnorr/bip-taproot.mediawiki#transaction-digest) section. We will also cover the rules for [signature opcodes](https://github.com/sipa/bips/blob/bip-schnorr/bip-tapscript.mediawiki#Rules_for_signature_opcodes), [transaction Digest](https://github.com/sipa/bips/blob/bip-schnorr/bip-tapscript.mediawiki#Transaction_digest).

Some questions to keep in mind as you review:
  * Any chance of having different messages in different contexts result in the same digest? Extension attacks? Other ambiguities? Does the epoch make sense?
  * Are there any O(n^2) paths where n signatures might require different sets of n data having to be rehashed?
  * Can cached data be shared with segwit v0 signatures where possible?
  * Is this efficient for hardware wallets that want to have as little data and computation as possible?
  * Is there any way to exploit users using hardware wallets with this scheme?

## Resource Limits

We'll also covering the Bip-tapscript Resource Limits.

From the [optech newsletter](https://bitcoinops.org/en/newsletters/2019/09/25/):
> The bip-tapscript proposal limits transactions to one signature-checking operation (sigop) for
> every 12.5 vbytes the witness data adds to the size of the transaction (plus one free sigop per
> input). Because signatures are expected to be 16.0 vbytes, this limit prevents abuse without
> affecting normal users. Compared to earlier abuse-prevention solutions, it means any valid
> taproot transaction can be included in a block regardless of how many sigops it contains—keeping
> miner transaction code simple and fast.

It might be also helpful to read over [this mailing list post](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2019-September/017306.html) by Sipa where he dives into more depth about bip-tapscript resource limits.

Some questions that you might ask yourself as you review:
  * What is the worst-case resource usage and is that worse than today?
  * What is the expected/average case resource usage and is this worse than today?

The two relevant BIPs are at:

https://github.com/sipa/bips/blob/bip-schnorr/bip-schnorr.mediawiki and https://github.com/sipa/bips/blob/bip-schnorr/bip-tapscript.mediawiki


## Misc

As before, the IRC channel for the Q&A sessions is ##taproot-bip-review on the Freenode IRC network. If you've got questions through the week, feel free to ask there -- if someone is around and available they might be able to answer. As well as the meeting logs there are ongoing channel logs as well, in case you want to see what's been going on there while you've been absent. As mentioned above, there's only one scheduled Q&A session this week: Tue 1900 UTC (America/Europe/Africa).


* Tue 19 Nov 11:00 -0800 Los Angeles
* Tue 19 Nov 14:00 -0500 New York
* Tue 19 Nov 19:00 +0000 UTC / London
* Tue 19 Nov 20:00 +0100 Paris
* Wed 20 Nov 00:30 +0530 Calcutta
* Wed 20 Nov 04:00 +0900 Tokyo
* Wed 20 Nov 06:00 +1100 Sydney

There's also the dedicated slack instance if you prefer that method of communicating.
