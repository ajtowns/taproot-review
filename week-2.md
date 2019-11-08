# Week Two Info

> "The solution was script, which generalizes the problem so transacting parties can describe their transaction as a predicate that the node network evaluates.  The nodes only need to understand the transaction to the extent of evaluating whether the sender's conditions are met." -- Satoshi, [2010-06-17](https://bitcointalk.org/index.php?topic=195.msg1611#msg1611)

Hopefully you've made it through the first week, successfully contacted
your study group, caught up on any background about the process, and
made some initial progress with review! If you haven't, that's fine --
catch up as best you can, and feel free to ask questions about earlier
topics even if we've supposedly moved on to later topics.

We've got a short poll for [week 1 feedback](https://docs.google.com/forms/d/e/1FAIpQLSfX6OZ3rK0_EW_A2S8-TCVkeK7t_3Slagg9apVZ5dq-1eLk1w/viewform) to help track how the review is going so far, if you can spend a couple of minutes filling it in that would be great! If you have questions/problems that need a more immediate response, feel free to send an email, ask on IRC or create a PR or issue in the github repo as seems appropriate.

Per the [curriculum](Curriculum.md) this week moves on from the overall
taproot construction to looking at key path spends and the merkle
construction that allows a multitude of scripts as alternatives
to direct key path spends.

## Results from Week One

We had the first two Q&A sessions, and have logs of the conversations captured: [week 1 Q&A 1](http://www.erisian.com.au/meetbot/taproot-bip-review/2019/taproot-bip-review.2019-11-05-19.00.log.html),
[week 1 Q&A 2](http://www.erisian.com.au/meetbot/taproot-bip-review/2019/taproot-bip-review.2019-11-07-02.00.log.html). There's some interesting discussion in both of them, so worth a look if you've got time!

There's already been a few suggested changes to the BIPs, including [PR#122](https://github.com/sipa/bips/pull/122), [PR#126](https://github.com/sipa/bips/pull/126/files), and [PR#128](https://github.com/sipa/bips/pull/128/files) -- they're all pretty short, so if you haven't contributed to a BIP or Bitcoin core before, they make for pretty easy examples of how to contribute!

One thing mentioned in a Q&A session which hasn't been resolved yet was the possible impact of a bech32 malleability misfeature on taproot upgradeability -- see [Pieter Wuille's post to bitcoin-dev](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2019-November/017443.html) and the following discussion for more information.

There have also been some interesting questions and answers on [bitcoin stackexchange](https://bitcoin.stackexchange.com/), eg:
 * [MuSig Signature Interactivity](https://bitcoin.stackexchange.com/questions/91534/musig-signature-interactivity)
 * [Taproot/Schnorr Pubkey lengths](https://bitcoin.stackexchange.com/questions/91531/would-a-schnorr-pubkey-be-a-different-length-than-a-taproot-pubkey-like-p2wpkh-a)

## Tapscript

To understand how tapscript works, you need to see both the taproot and tapscript BIPs:

 * https://github.com/sipa/bips/blob/bip-schnorr/bip-taproot.mediawiki
 * https://github.com/sipa/bips/blob/bip-schnorr/bip-tapscript.mediawiki

You've hopefully already read much of the taproot BIP, but you'll need to add in the "Constructing and spending Taproot outputs" section and the bullet points under "If there are at least two witness elements left, script path spending is used" in "Script validation rules" if you missed them before.

As far as the tapscript BIP goes, you may wish to skip or skim the sections "Rules for signature opcodes", "Transaction digest", "Resource limits" and the related items from the "Rationale" section, but should read the rest of it in depth.

The generic suggestions about what sort of questions to consider from [last week](week-1.md) still apply -- so do consider rereading that.

There are probably two sorts of examples that are helpful to think about for tapscript as proposed. One is just plain multisig, and what different ways there are to implement it with taproot and tapscript, and what tradeoffs there are between them. The other is to think about entirely different signing policies -- eg, you might want to have some addresses that can be spent as a hot wallet, but are also spendable via a cold wallet in the event that your hot wallet breaks somehow -- the taproot construction allows you to have one of those as the cheap key path, and hide the other as the script path spend, and the merkle path that the taproot BIP specifies allows you to potentially have many such paths for each address.

Gregory Sanders (aka instagibbs) has made some progress on the proof of concept for doing Liquid-style k-of-n multisig in the taproot environment: he's got a [jupyter notebook](https://github.com/instagibbs/taproot-workshop/blob/liquid_tap/3.2-liquid-tapscript-case-study.ipynb) based on the workbooks from the [Optech taproot workshop](https://bitcoinops.org/en/schorr-taproot-workshop), which might be interesting to look through.

## Misc

The IRC channel for the Q&A sessions is ##taproot-bip-review on the Freenode IRC network. If you've got questions through the week, feel free to ask there -- if someone is around and available they might be able to answer. As well as the [meeting logs](http://www.erisian.com.au/meetbot/taproot-bip-review/2019/) there are ongoing [channel logs](http://www.erisian.com.au/meetbot/taproot-bip-review/2019/) as well, in case you want to see what's been going on there while you've been absent. The Q&A sessions this week are at the same times as last week: Tue 1900 UTC (America/Europe/Africa) and Thu 0200 UTC (America/Asia/Oceania). In different time zones these are:

 * Tue 05 Nov 11:00 -0800 Los Angeles
 * Tue 05 Nov 14:00 -0500 New York
 * Tue 05 Nov 19:00 +0000 UTC / London
 * Tue 05 Nov 20:00 +0100 Paris
 * Wed 06 Nov 00:30 +0530 Calcutta
 * Wed 06 Nov 04:00 +0900 Tokyo
 * Wed 06 Nov 06:00 +1100 Sydney

and

 * Wed 06 Nov 18:00 -0800 Los Angeles
 * Wed 06 Nov 21:00 -0500 New York
 * Thu 07 Nov 02:00 +0000 UTC / London
 * Thu 07 Nov 03:00 +0100 Paris
 * Thu 07 Nov 07:30 +0530 Calcutta
 * Thu 07 Nov 11:00 +0900 Tokyo
 * Thu 07 Nov 13:00 +1100 Sydney

There's also the dedicated [slack instance](https://bitcoin-review.slack.com/) if you prefer that method of communicating.

