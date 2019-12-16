# Taproot BIP Review

## Pitch

The schnorr/taproot/tapscript BIPs are ready for review at this point, and we want to get as much in-depth review from as broad a range of people as we can before we go further on implementation/deployment.
Reviewing the BIPs is hard in two ways: not many people are familiar with reviewing BIPs in the first place, and there are a lot of concepts involved in the three BIPs for people to get their heads around.

This is a proposal for a structured review period.
The idea is that participants will be given some guidance/structure for going through the BIPs, and at the end should be able to either describe issues with the BIP drafts that warrant changes, or be confident that they’ve examined the proposals thoroughly enough to give an “ACK” that the drafts should be formalised and move forwards into implementation/deployment phases.

Benefits of participating:

 * Deeply understand schnorr and taproot
 * Be a stakeholder in Bitcoin consensus development
 * Support/safeguard decentralisation of Bitcoin protocol development
 * Have fun!

An overview of the topics covered is outlined on the [curriculum](Curriculum.md)
page.

A list of background [resources](Resources.md) are available for review.

## Timeline

 * Oct 23rd to 30th - Sign up
 * Nov 3rd to Dec 14th - Structured review
   * [Week 1 - Taproot](week-1.md)
   * [Week 2 - Tapscript](week-2.md)
   * [Week 3 - Schnorr](week-3.md)
   * [Week 4 - Signature details / Resource limits](week-4.md)
   * [Week 5 - Schnorr applications](week-5.md)
   * [Week 6 - Upgrade Methods](week-6.md)
 * Dec 15th to 21st - Wrap up
   * [Week 7 - Wrap up](week-7.md)

## Sign up

 * Consider whether you have time to try doing any [proof-of-concept development work](PoC-Projects.md) and if so, what project to work on.
 * Before Oct 30, sign up via [RSVP form](https://forms.gle/iiPaphTcYC5AZZKC8).
   **NOTE:** The information you share in the form will be shared with others completing the form, including your provided email address
 * If you sign up prior to Oct 30th (23:59 UTC-10) we’ll help you find other people to review with. Please join freenode IRC channel ##taproot-bip-review to join discussion with other reviewers and form study groups.
 * Beginning November 3, you should expect to commit to 4 hours per week over 7 weeks; possibly more if you’re developing a proof-of-concept, or maybe less if you’re already familiar with some of the details, or only aiming to do a rough review.

## What if I want to do things differently?

* This just aims to provide a helpful structure to reviewing the taproot bips -- if something else works for you, feel free to do things your way! Different perspectives are more likely to find more problems so this is a good thing!
* If you aren’t confident in some area, you may want to skip it -- that’s okay, but being unfamiliar with something may just mean you’ve got fresh eyes and are able to find problems other people will overlook because they’re relying on assumptions that aren’t valid. So do at least consider trying to review everything.
* If you want to do things out of order, you can find the curriculum info that we’ll be sending out for future sessions [here](Curriculum.md).

## What happens each week

* On Sunday each week, we’ll email you this week’s topic, some links to related work, and some focus questions to consider, as well as a link to a **google form** to log your feedback/conclusions about the topic.
* On Monday or Tuesday, you should do an initial review of the topic.
* You should then join one of the Q&A sessions, to raise any concerns, and hear other people’s take.
* Finally, on Thursday or Friday, you should complete your review and fill in the google form.

## How the Q&A sessions work

* They’ll go for 1 hour, starting at Tue 1900 UTC (America/Europe/Africa) and Thu 0200 UTC (America/Asia/Oceania)
* They’ll happen on IRC (##taproot-bip-review on freenode) and be logged
* Depending on number of participants, they may be moderated, with questions submitted on one channel, and answers on another
* We’ll have some experts available for answering questions at both sessions (including Jonas Nick, Andrew Poelstra, Tim Ruffing, Anthony Towns, and Pieter Wuille)

## What happens in the wrap-up week

* For people working on a proof-of-concept development project, we’ll send out a google form prior to the last week so you can summarise how you went, any problems you found, and include a link to your github so other people can check your work out.
* On the Sunday before the final week, we’ll send out info about the proof-of-concept results to everyone, and a google form for your overall conclusions
* On Monday or Tuesday you should do any final review of the BIPs and look into any of the proof of concept work that interests you
* The final Q&A sessions can be used to raise any concerns that haven’t already been covered, or discuss some of the proof of concept work
* And finally, on Thursday or Friday, you should complete your review and fill in the google form, and, if you have any concerns that haven’t already been addressed, work on ensuring that’s raised as an issue or pull request against the relevant BIPs.

## What happens after this is all over?

* We’ll establish a wiki page with the final ACK / HOLD conclusion from each participant
* We’ll pass on all the results and suggestions we’ve collected in the google forms to the BIP drafters
* The BIP drafters will review any issues raised or pull requests and include changes they think make sense, and may also add additional rationale for why some changes weren’t made

