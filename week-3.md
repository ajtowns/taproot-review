# Week Three Info

> "Don't roll your own crypto, bro." -- Joseph Cox, VICE.com [2015-12-11](https://www.vice.com/en_us/article/wnx8nq/why-you-dont-roll-your-own-crypto)

With luck, everyone's into the swing of things now, because we're moving on to the first look at the final BIP, both the alpha and omega, if you will: [bip-schnorr](https://github.com/sipa/bips/blob/bip-schnorr/bip-schnorr.mediawiki). This marks the halfway point -- by the end of this week we'll have gone through all the BIPs (if you're following the [curriculum](Curriculum.md) anyway!) and for the following three weeks we'll be focussing on some of the details (that you might have skipped over if you followed the suggestions here) and their implications.

We've set up a "[knowledge check](https://forms.gle/rsezDoj2fChBj7u76)" survey this week so you can record where you think you're up to in understanding the BIPs, as well as some free fields for comments about the process or the BIPs. This survey is associated with your email, both on the off-chance that we might be able to find some interesting correlations, and so that we might be able to followup on any comments that get left. The idea is to do another one of these around the last week of the review.

The quote this week emphasises the widely known wisdom that you shouldn't roll your own crypto -- even though that's essentially what we're doing here with both a new standard for schnorr signatures, and introducing the taproot construction for real world use. Both of these are security constructions that rely on mathematical assumptions working out as expected; so before adopting it, it's wise to make sure that these new constructions really can survive expert cryptanalysis. (We'll see in the "schnorr applications" week how the first version of the musig construction didn't survive expert review, eg)

One thing that's been working out really well (in my opinion, anyway!) is how engaged reviewers have been with the regular processes of communicating online (irc, bitcoin-dev, etc), and filing issues and pull-requests on github to make improvements to the drafts. Since that's the usual way of improving most open source Bitcoin related things, we've been encouraging people to focus on that, rather than collecting review results via google forms or similar. But to help avoid things getting missed, we've added some free form fields to the [knowledge check](https://forms.gle/rsezDoj2fChBj7u76) survey for capturing things that might need changes that haven't been filed in github.

## Week 1 Feedback

We got 36 responses (about 20%) to the "week 1 feedback" survey -- summary stats were:

 * Solo review: 2 hours (15 responses), 3+ hours (11 responses), 1 hour (6), 30 min (4)
 * Study group: 1 hour (13), 2 hours (8), None! (8), 30 minutes (6), 3+ hours (1)
 * Q&A session: 1 hour (19), 30 minutes (7), None! (5), 2 hours (4), 3+ hours (1)
 * PoC work: None! (33), 3+ hours (1), 1 hour (1), 30 minutes (1)

Most people rated their first week progress as 2 or 3, so about as expected, and resources as 3-5 which is great. Study group rating was bit more spread out, with nine responses give a low rating of 1 or 2, twenty giving mid-good rating of 3 or 4, and six giving top marks of 5. So if your group is doing particularly well, it might be worth writing a blog post or making a youtube video or similar about what's going right so others can learn from you; alternatively if your group is not doing so great, it might be interesting to lurk through some of the other groups' slack channels to see what works for them and perhaps try it in your group.

This poll was just for the first week, so it's already out of date, but since this is all an experiment, might be of interest anyway.

## Results from Week Two

We've had the second two Q&A sessions, with meetbot logs: [week 2 Q&A 1](http://www.erisian.com.au/meetbot/taproot-bip-review/2019/taproot-bip-review.2019-11-12-19.00.log.html), [week 2 Q&A 2](http://www.erisian.com.au/meetbot/taproot-bip-review/2019/taproot-bip-review.2019-11-14-02.00.log.html) -- but as it turns out the second Q&A didn't actually have any questions. Since Q&A 2 in week one seemed a bit sparser too, we'll just advertise the single slot this week, but if that's not convenient for you, do feel free to ask questions anytime -- experts are lurking in that channel most of the time, and even if they're not available to answer immediately, if you can stay connected you will often get an answer sometime later. (If you can't stay connected, you can use the [logs](http://www.erisian.com.au/taproot-bip-review/) to catch answers to your question, but it might be wise to mention that you'll be doing so to avoid people thinking there's no point responding because you've left the channel)

There's been a few more suggested improvements for the BIPs, including [#138](https://github.com/sipa/bips/issues/138), [PR#145](https://github.com/sipa/bips/pull/145), [PR#144](https://github.com/sipa/bips/pull/144), [PR#137](https://github.com/sipa/bips/pull/137), and [PR#136](https://github.com/sipa/bips/pull/136). Max Hillebrand has filed an [issue for high-level discussion of adding taproot to Wasabi Wallet](https://github.com/zkSNACKs/WalletWasabi/issues/2531) that might be interesting to see.

## Schnorr

The schnorr BIP was the first of the three BIPs with a [public draft](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-July/016203.html), and is the one most easily analysed on its own, separate from the other BIPs. However, this is also, in some sense, the BIP that is least connected to Bitcoin -- it just describes a signature system, and leaves how it might be used in practice undocumented.

Fortunately, having hopefully read the taproot and tapscript BIPs already, you have some ideas on how it might be used in Bitcoin! But you might like to also consider how the schnorr BIP might be useful elsewhere as well -- for example in the Bitcoin p2p protocol, for authenticating lightning gossip, for a new variant of Bitcoin signed messages (eg, [BIP 322](https://github.com/bitcoin/bips/blob/master/bip-0322.mediawiki)), or some other application.

Anyway, the BIP is at:

 * https://github.com/sipa/bips/blob/bip-schnorr/bip-schnorr.mediawiki

You may wish to skim the "Applications" section since we've got week 5 reserved for looking into that in more detail. However most of the complexity there is actually in reading the detailed explanations of how those work in other papers and documents, so just reading the whole BIP this week might be a good approach too.

Jonas Nick wrote a [blog post](https://medium.com/blockstream/reducing-bitcoin-transaction-sizes-with-x-only-pubkeys-f86476af05d7) for the Blockstream blog about x-only pubkey construction that might be interesting. t-bast from group 17 pointed out a [paper on bad nonces with ECDSA](https://eprint.iacr.org/2019/023.pdf) that may be useful background for why deterministic nonce generation is useful when possible; and Leonid Beder from the same group pointed to a [talk by Andrew Poelstra at the Monero Conference on Schnorr signatures](https://www.youtube.com/watch?v=L6KqkrP_nU4) that mentions an interesting construction to ensure proper nonce generation by hardware wallets. The videos from the [optech taproot workshop](https://bitcoinops.org/en/schorr-taproot-workshop/) might be helpful as a slightly gentler introduction to the topic.

If you're interested in looking at implementations, then you may wish to look at any or all of:

 * the [python reference code](https://github.com/sipa/bips/tree/bip-schnorr/bip-schnorr/) (not for production use)
 * the [jupyter notebooks from the optech taproot workshop](https://github.com/bitcoinops/taproot-workshop/) (also not for production use)
 * [libsecp256k1 PR#558](https://github.com/bitcoin-core/secp256k1/pull/558) adds basic schnorr signature support
 
## Misc

The IRC channel for the Q&A sessions is ##taproot-bip-review on the Freenode IRC network. If you've got questions through the week, feel free to ask there -- if someone is around and available they might be able to answer. As well as the [meeting logs](http://www.erisian.com.au/meetbot/taproot-bip-review/2019/) there are ongoing [channel logs](http://www.erisian.com.au/taproot-bip-review/) as well, in case you want to see what's been going on there while you've been absent. As mentioned above, there's only one scheduled Q&A session this week: Tue 1900 UTC (America/Europe/Africa).

 * Tue 19 Nov 11:00 -0800 Los Angeles
 * Tue 19 Nov 14:00 -0500 New York
 * Tue 19 Nov 19:00 +0000 UTC / London
 * Tue 19 Nov 20:00 +0100 Paris
 * Wed 20 Nov 00:30 +0530 Calcutta
 * Wed 20 Nov 04:00 +0900 Tokyo
 * Wed 20 Nov 06:00 +1100 Sydney

There's also the dedicated [slack instance](https://bitcoin-review.slack.com/) if you prefer that method of communicating.

