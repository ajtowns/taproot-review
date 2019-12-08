# Week Six Info

> "Being open source means anyone can independently review the code.  If it was closed source, nobody could verify the security.  I think it's essential for a program of this nature to be open source." - satoshi, [2009-12-10](https://bitcointalk.org/index.php?topic=13.msg46#msg46)

Ten year anniversary of that quote this week!

Note: [Week Five's notes](week-5.md) never got mailed out, so if you didn't find the URL yourself, you probably missed out!

This is the last week of content for these sessions -- the final week (2019-12-16 to 2019-12-20) is intended for wrapping up. If you've been working on a proof-of-concept or other implementation of schnorr or taproot stuff these past weeks and would like to share your progress, please send an email or open a PR on the [taproot-review repo](https://github.com/ajtowns/taproot-review/pulls) to add it to [Resources.md](https://github.com/ajtowns/taproot-review/blob/master/Resources.md).

As we near the end it's a good time to start thinking about what the next step is. The obvious path would be to propose the BIPs formally, get them assigned numbers, and then move onto reviewing the code in depth. But if there's bugs in the design, or missing features we should add, or if the entire strategy isn't quite right, now is a better time than later to talk about that. Small changes to the design as we do code review are fine, of course (though catching them earlier is always better).

But assuming we do go ahead with taproot, that probably isn't the end of the line -- there are plenty of other ideas about how to improve Bitcoin, and if it turns out there's consensus to adopt one or more of them, we'd like to make that as easy as possible at least at a technical level.

## Upgrade Paths

This week's topic is therefore upgrade paths -- ways in which future changes can be made to Bitcoin after taproot is deployed. Things to (re)read:

 * bip-taproot -- Unencumbered v1 spends [(rationale 1)](https://github.com/sipa/bips/blob/bip-schnorr/bip-taproot.mediawiki#cite_note-1), Leaf versions [(7)](https://github.com/sipa/bips/blob/bip-schnorr/bip-taproot.mediawiki#cite_note-7) [(10)](https://github.com/sipa/bips/blob/bip-schnorr/bip-taproot.mediawiki#cite_note-10), Annex [(4)](https://github.com/sipa/bips/blob/bip-schnorr/bip-taproot.mediawiki#cite_note-4)
 * bip-tapscript -- OP_SUCCESS [(rationale 2)](https://github.com/sipa/bips/blob/bip-schnorr/bip-tapscript.mediawiki#cite_note-2), and Unknown Public Key types [(7)](https://github.com/sipa/bips/blob/bip-schnorr/bip-tapscript.mediawiki#cite_note-7)

Those are probably in order from worst to best to use -- so if you want to change the way signatures work, using an unknown public key type can solve your problem with minimal impact; if you need a new opcode, then upgrading an OP_SUCCESS opcode should work, again with minimal impact, while if you want to commit to some extra data then the annex is available. And if none of those work you can introduce a new scripting language via a new leaf version, or redo how everything works via using an unencumbered script pubkey, either segwit version 2-16 or an unencumbered v1 spend.

Some things to think about:

 * What are the pitfalls to each of these methods?
   * Do they work in parallel, or do you have to serialise upgrades?
   * Is there a limit to how many upgrades of this type can be done?
   * Can you extend the limit by doing something clever with the last upgrade of that type?
   * How complex is each method to use?
 * What upgrades are likely? Some proposals include:
   * NOINPUT/ANYPREVOUT
   * CHECKTEMPLATEVERIFY
   * Re-enable disabled opcodes like OP_CAT
   * Extend existing math opcodes (ADD, MUL on 64-bit or
     256-bit numbers)
   * Commit to block hash at a given height (for replay protection
     against chain splits or reorgs)
   * Changing the scripting language entirely (eg Simplicity)
   * Graftroot or generalised taproot
   * Cross-input signature aggregation
   * Are there other interesting proposals worth taking into account?
 * Which upgrade methods make sense for likely upgrades? How well do they work?

## Wrap-up Preparation

As this is the last week of content, you might also want to consider your overall assessment of the drafts:

 * Were there any parts that I'm not familiar enough with?
 * Were there any problems that haven't been filed as an issue,
   don't have a patch prepared, or have gotten stuck in discussion?
 * Are there any easy/big improvements that should get added in?
 * Am I comfortable with the set of changes being proposed -- conceivably there could be too many changes and some of them should be split out; or perhaps there are too few changes and others should be merged in?
 * Do I think this is ready to be assigned a BIP number and move onto code review and eventual deployment?

## Miscellaneous

The IRC channel for the Q&A sessions is ##taproot-bip-review on the Freenode IRC network. If you've got questions through the week, feel free to ask there -- if someone is around and available they might be able to answer. As well as the [meeting logs](http://www.erisian.com.au/meetbot/taproot-bip-review/2019/) there are ongoing [channel logs](http://www.erisian.com.au/taproot-bip-review/) as well, in case you want to see what's been going on there while you've been absent. There's only one scheduled Q&A session this week: Tue 1900 UTC (America/Europe/Africa), but feel free to ask questions at any time during the week.

 * Tue 10 Dec 11:00 -0800 Los Angeles
 * Tue 10 Dec 14:00 -0500 New York
 * Tue 10 Dec 19:00 +0000 UTC / London
 * Tue 10 Dec 20:00 +0100 Paris
 * Wed 11 Dec 00:30 +0530 Calcutta
 * Wed 11 Dec 04:00 +0900 Tokyo
 * Wed 11 Dec 06:00 +1100 Sydney

There's also the dedicated [slack instance](https://bitcoin-review.slack.com/) if you prefer that method of communicating.

