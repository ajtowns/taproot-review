
# Week One Info

> "Some people worry about developers attempting to take control, but the defense against that is for other developers to review their code and sound an alarm if they see something inappropriate." -- David Harding, [2017-07-28](https://dtrt.org/posts/minimum-majority-measure/)

This first week's focus is on two things: getting setup to review the BIPs and taking a first pass at the taproot BIPs; see the [first section in the Curriculum cheat sheet](https://github.com/ajtowns/taproot-review/blob/master/Curriculum.md#intro--taproot).

## Intro

As a general reminder, BIPs are just proposals -- they're the first step on the path to making a change to Bitcoin, but taking that first step doesn't mean you won't immediately turn around and walk straight back to where you came from. If you look through the bip repository on github, you can see many BIPs that haven't progressed, some that have and have been walked back from, and others that have achieved consensus and implementation and are in active use today. If you're not familiar with the process, it can be instructive to have a look through how things have gone in the past:

 * [BIPs repo](https://github.com/bitcoin/bips/)
 * [BIP 2 -- BIP policy](https://github.com/bitcoin/bips/blob/master/bip-0002.mediawiki)
 * [BIP PRs](https://github.com/bitcoin/bips/pulls?utf8=%E2%9C%93&q=is%3Apr)

The bech32 segwit address format might serve as a helpful example if you haven't seen the process in action before. The initial proposal failed, and after a lot more development resulted in a new proposal that was eventually implemented and deployed:

 * [BIP 142](https://github.com/bitcoin/bips/blob/master/bip-0142.mediawiki); List disccusion: [(1)](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2015-December/012095.html) [(2)](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2015-December/012136.html); PRs: [PR #267](https://github.com/bitcoin/bips/pull/267), [PR #291](https://github.com/bitcoin/bips/pull/291), [PR #294](https://github.com/bitcoin/bips/pull/294)
 * [BIP 173](https://github.com/bitcoin/bips/blob/master/bip-0173.mediawiki); List discussion: [(1)](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2017-March/013749.html) [(2)](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2017-May/014274.html); bitcoin-talk discussion [(3)](https://bitcointalk.org/index.php?topic=2624630.msg26762627); PRs: [PR #533](https://github.com/bitcoin/bips/pull/533), [PR #534](https://github.com/bitcoin/bips/pull/534), [PR #565](https://github.com/bitcoin/bips/pull/565), [PR #582](https://github.com/bitcoin/bips/pull/582), [PR #587](https://github.com/bitcoin/bips/pull/587), [PR #607](https://github.com/bitcoin/bips/pull/607), [PR #627](https://github.com/bitcoin/bips/pull/627)

Note that discussion of the details of proposals usually takes place outside of the PRs -- eg on the bitcoin-dev mailing list.

It's probably a good idea to approach reviewing with a "constructive" mindset rather than a "judgemental" one -- that is coming up with ideas for how things might be changed to be better, or how things might not work as expected or hoped, rather than why particular approaches might be good or bad. In particular, Bitcoin might change in ways that even the smartest, most experienced Bitcoin developers think is a bad idea (or might not change in ways that they think is a good idea).

One example of this might be the success of BIP 148, despite opposition by well respected developers and lack of support by the Bitcoin Core software:

 * [BIP 148](https://github.com/bitcoin/bips/blob/master/bip-0148.mediawiki); List disccusion: [(1)](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2017-March/013714.html) [(2)](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2017-April/014152.html) [(3)](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2017-May/014377.html); [PR#501](https://github.com/bitcoin/bips/pull/501); [Segwit Support page](https://en.bitcoin.it/wiki/Segwit_support); [Bitcoin Core merge NACK](https://github.com/bitcoin/bitcoin/pull/10442#issuecomment-305004154)

So, personally, my recommendation is to focus almost all of your review effort on understanding the proposal and finding ways to make it work better, and not about whether you'll ultimately end up "for" or "against" it. That way your review effort will make things better whatever ends up happening. That doesn't mean you shouldn't form an opinion as to whether the change is a good one or not, of course, just try not to make that your primary focus!

## Taproot

The current draft of the taproot BIP can be found at:

 * https://github.com/sipa/bips/blob/bip-schnorr/bip-taproot.mediawiki

Remember that this is being actively worked on, so there may have been changes if you've read it previously!

We'll be spending more time later on how "script path" spends work and the details of how signatures work, so you may wish to skip or skim the "script path spending" bullet in the section titled "Script validation rules", as well as the sections titled "Signature validation rules" and "Constructing and spending Taproot outputs" for now.

Ideally reading the BIP (and its references) will already make it clear what the purpose of the proposal is and how it achieves that purpose. Some good general questions to think about might include:

 * Do the goals make sense?
 * Do the design decisions follow from the goals?
 * What are the tradeoffs, and do they make sense?
 * How will this affect people who use Bitcoin?
 * Are there better ways to achieve these goals?
 * Do all the details of the proposal fit together and work?

You may want to review the sample implementation, at

 * https://github.com/sipa/bitcoin/commits/taproot

or you may want to review past discussion, such as on the bitcoin-dev mailing list, in the OpTech newsletters, or looking through the git changelog of the BIP draft or the PRs or issues in the repository. If you do want to explore some of these paths, there are links in the curriculum doc mentioned above. If you find more resources, you may wish to open a PR to add them to the Resources doc:

 * https://github.com/ajtowns/taproot-review/blob/master/Resources.md

Alternatively, you may want to just focus on the BIP text directly to see if it makes sense on its own.

If there are parts you don't understand, discuss them with others, such as your study group, or asking at the Q&A sessions, or raising a question on bitcoin.stackexchange.org, or however else you like. If that resolves the confusion, great! If not, it might be worth creating an issue or pull request against the bip-schnorr draft on github. It can be hard to find a balance between getting the details right and caught up in bikeshedding, so talking to other people first is usually a good idea!

## Misc

If you want to chat on Slack, there's an [invite site](https://bitcoin-review-slack-invite-site-automationd766.azurewebsites.net/) available for this project.

Please see the [suggested study groups](study-groups.md) for some other people to talk to!

The first Q&A sessions are on ##taproot-bip-review on the Freenode IRC network at Tue 1900 UTC (America/Europe/Africa) and Thu 0200 UTC (America/Asia/Oceania). In different timezones these are:

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

