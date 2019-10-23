# Proof of Concept Projects

These are some ideas for proof of concept projects to explore Schnorr and/or taproot in more depth.

 * LN payment points and scalars
 * LN 2-of-2 Schnorr MuSig construction for channel open/close
 * Off-chain 2-of-3 key rotation
 * Liquid-style 11-of-15 multisig
 * Taproot/Schnorr support for python-bitcoinlib (etc?)
 * Taproot/Schnorr support for bitcoinjs-lib?
 * ...

Note: Optech has developed a [Schnorr & Taproot library](https://github.com/bitcoinops/taproot-workshop), which can be used to prototype many of the proof-of-concept projects suggested above. The library features a Schnorr and MuSig implementation as well as methods to construct Taproot outputs from various types of Tapscripts. The documentation is written in the form of interactive Jupyter notebooks, which provide thorough examples on how to use the library.