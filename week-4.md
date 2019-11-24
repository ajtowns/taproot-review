# Week Four Info

> "I hate reinventing the wheel [...].  The serialization format we have is as dead simple and flat as possible.  There is no extra freedom in the way the input stream is formed.  At each point, the next field in the data structure is expected.  The only choices given are those that the receiver is expecting.  There is versioning so upgrades are possible." -- satoshi, [2010-08-02](https://bitcointalk.org/index.php?topic=632.msg7090#msg7090)

In theory, this might be a lighter week than others: there aren't major new concepts on the agenda this time, just bunches of details. Which, as I write it, doesn't sound lighter all... But if it is, there might be some opportunity to take a breath this week or do some extra review of things from the past three weeks, if there was anything you weren't satisfied with. As always, if you've got better ideas as to what to look at next, don't feel in any way obliged to follow the suggestions here!

As mentioned last week, we've got a "[knowledge check](https://forms.gle/rsezDoj2fChBj7u76)" poll up to try to track where everyone is at this point -- so if you haven't already filled it out, doing it early this week would be great!

## Results from Week Three

The [week 3 Q&A logs](http://www.erisian.com.au/meetbot/taproot-bip-review/2019/taproot-bip-review.2019-11-19-19.00.log.html) are available as usual -- it included a walk through of how batch validation can be more efficient, and there was [more discussion](http://www.erisian.com.au/taproot-bip-review/log-2019-11-19.html#l-293) on that after the meeting ended. While there wasn't an official second Q&A, some folks showed up at the time it would have been anyway, and there was some [discussion](http://www.erisian.com.au/taproot-bip-review/log-2019-11-21.html#l-10) anyway. There's other discussions in those logs that might be of interest, so do have a look if you have time. There's also been [more PRs](https://github.com/sipa/bips/pulls?utf8=%E2%9C%93&q=is%3Apr). There's also some further discussion of the "e" vs "R" choice for Schnorr signature encoding on the slack instance.

## Signature Details

The first topic for this week is thinking about the details of how the "message" is encoded when passed through to the bip-schnorr signing protocol. The particular sections of the BIPs to focus on (that you may have skimmed over previously) are:

 * bip-taproot: [Signature validation rules](https://github.com/sipa/bips/blob/bip-schnorr/bip-taproot.mediawiki#Signature_validation_rules) 
 * bip-tapscript: [Rules for signature opcodes](https://github.com/sipa/bips/blob/bip-schnorr/bip-tapscript.mediawiki#Rules_for_signature_opcodes), and [Transaction digest](https://github.com/sipa/bips/blob/bip-schnorr/bip-tapscript.mediawiki#Transaction_digest) and corresponding sections from the rationale.

For context, you might consider some of the complexities bitcoin has had with signatures in the past, eg:

 * CHECKMULTISIG pops an extra item from the stack which it then ignores, resulting in a malleability vector, which is fixed by [BIP 147](https://github.com/bitcoin/bips/blob/master/bip-0147.mediawiki)

 * When signing with an input that doesn't have a corresponding output, [SIGHASH_SINGLE signs the value "1"](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2012-August/001805.html) rather than a digest of the transaction. (Though there are examples where this is actually [useful](https://bitcointalk.org/index.php?topic=1118704.msg11864913#msg11864913))

 * FindAndDelete() can behave in [rather confusing ways](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2014-November/006878.html), and perform [far worse](https://bitslog.com/2017/01/08/a-bitcoin-transaction-that-takes-5-hours-to-verify/) than might be expected

 * Simply hashing data for signature verification can take [excessively long](https://rusty.ozlabs.org/?p=522) if it needs to be done differently for each signature, and each time uses a lot of data.

As far as signature hashing goes, the approach bip-taproot and bip-tapscript take is perhaps reflected in satoshi's quote above -- it aims to make it easy to cache components so that quadratic blowups don't happen, it tries to be simple so that there isn't any confusing behaviour to uncover bugs in years later, and it tries to constrain things so that accidental collisions, length extension attacks and similar problems just can't arise.

Also, bip-tapscript replaces CHECKMULTISIG and it's extra stack element bug with CHECKSIGADD -- and hopefully doesn't introduce any new bugs to go with it.

Some of the sorts of questions you might want to consider include:

 * Is there any chance of having different messages in different contexts result in the same digest? How about extension attacks? Other ambiguities? Does the epoch make sense?
 * Are there any O(n^2) paths where n signatures might require different sets of n data having to be rehashed?
 * Can cached data be shared with segwit v0 signatures where possible?
 * Is this efficient for hardware wallets that want to have as little data and computation as possible?
 * Is there any way to exploit users using hardware wallets with this scheme?

## Resource Limits

As suggested by some of the problems mentioned above, an important thing to keep in mind is limits on resource usage. Both the changes to the way transaction digests for signatures are calculated, and the resource limit changes in bip-tapscript could have unanticipated effects here, so in addition to the sections above, we're covering:

 * bip-tapscript [Resource Limits](https://github.com/sipa/bips/blob/bip-schnorr/bip-tapscript.mediawiki#Resource_limits) and corresponding rationale.

The most obvious way we constrain resources is via the block weight limit -- the more vbytes you have in your transaction, the more fees you pay; standard transactions are limited to at most 400k weight units; and blocks are limited to 4M weight units. Because it's easier to optimise for one dimension rather than two, many other limits are tied back to the weight limit -- so the idea is that if your transaction is twice the size, then it can use up to twice the CPU for calculating signatures or hashes or doing logic in script, but it shouldn't do more than that.

This can be more subtle than it seems -- eg, there is currently an O(n^2) path with nested OP_IF statements, so that removing the 201-opcode limit and allowing larger transactions to execute more opcodes would not be safe. See [PR#16902](https://github.com/bitcoin/bitcoin/pull/16902) for more details on that.

It's probably worth reading some of the PRs on this that have already been addressed in the draft bips, in particular [PR#60](https://github.com/sipa/bips/pull/60), [PR#73](https://github.com/sipa/bips/pull/73), and [PR#76](https://github.com/sipa/bips/pull/76).

It might be worth considering how you might construct a worst case block that attempts to maximise signature operations by using both the current block-wide sigop limit and the different taproot sigop budget -- does this allow significantly more sigops per block than can currently be achieved, or could be achieved with taproot/tapscript transactions alone? If so, is this significant enough to warrant some other resource limit to be coded (cf [PR#84](https://github.com/sipa/bips/pull/84)), and if so, what form should that extra limit take?

Other references: [optech newsletter commentary](https://bitcoinops.org/en/newsletters/2019/09/25/), [mailing list post](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2019-September/017306.html)

## Miscellaneous

The IRC channel for the Q&A sessions is ##taproot-bip-review on the Freenode IRC network. If you've got questions through the week, feel free to ask there -- if someone is around and available they might be able to answer. As well as the [meeting logs](http://www.erisian.com.au/meetbot/taproot-bip-review/2019/) there are ongoing [channel logs](http://www.erisian.com.au/taproot-bip-review/) as well, in case you want to see what's been going on there while you've been absent. There's only one scheduled Q&A session this week: Tue 1900 UTC (America/Europe/Africa), but feel free to ask questions at any time during the week.

 * Tue 26 Nov 11:00 -0800 Los Angeles
 * Tue 26 Nov 14:00 -0500 New York
 * Tue 26 Nov 19:00 +0000 UTC / London
 * Tue 26 Nov 20:00 +0100 Paris
 * Wed 27 Nov 00:30 +0530 Calcutta
 * Wed 27 Nov 04:00 +0900 Tokyo
 * Wed 27 Nov 06:00 +1100 Sydney

There's also the dedicated [slack instance](https://bitcoin-review.slack.com/) if you prefer that method of communicating.

