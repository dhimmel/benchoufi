Benchoufi et al propose and implement a method for notarizing participant consent for clinical trials using the Bitcoin blockchain. At a minimum, such an approach must accomplish two cryptographic objectives:

1. provide participants with a fraud-resistant method to irrefutably consent to the terms of a clinical trial. 
2. provide clinical trial investigators with a method to retrospectively verify participant consent at a given point in time. 

I agree with the authors that cryptographically notarizing consent would be a major advance. If possible, there would be strong incentives, both ethical and practical, for investigators to implement and regulatory agencies to mandate such an approach.

By encoding a hash into the Bitcoin blockchain that derives from a "consent document", it is possible for investigators to timestamp a consent document and thereby retrospectively prove the existence of that consent document at a given point in time. However, I am not convinced that the study provides patients with a fraud-resistant, irrefutable method of consent. Specifically, I don't think the study provides a method for ensuring that a specific participant provided consent. In other words, can clinical trial investigators prove that a specific participant consented rather than just proving that some entity consented under the supposed digital identify corresponding to a specific participant?

The study uses digital signatures to attest that a participant approved a specific consent form. The implementation relies on bitcoin private keys to provide digital signatures. The problem is that bitcoin addresses (which uniquely derive from a private key) are pseudonymous. For example, anyone with access to a consent form could create an unlimited number of bitcoin private keys and use these private keys to digitally sign the consent form. How does one prove that a bitcoin address solely belonged to a single participant?

The generation of bitcoin private keys in this study occurs at https://git.io/vSPTE. I don't see anything in the code or manuscript that irrefutably links a participant to ownership of a given bitcoin address. Therefore, it appears to me that clinical trial investigators (or many other actors) could forge consent. In fact, the manuscript appears to concede this point with the statement:

> Each of the to-be-enrolled users were assigned a private key in order to sign data and documents, and in practice this would be used to publish their signed consent.

Linking digital identities to physical identities is difficult. However, this is a precondition to blockchain notarization of clinical trial consent. OpenPGP (the most established method for digital identity and signatures) relies on a web of trust model to link digital identities to physical identities. HTTPS relies on Certificate Authorities to link digital identities to organization identities.

Since the manuscript does not sufficiently address how it links digital and physical identities, I dug a bit deeper into Stratumn, the underlying service provider. [Stratumn](https://stratumn.com/) is a French company, which aims to "secure processes between partners through blockchain technology." Stratumn focuses on "proof of process" using a JSON data structure called [chainscript](http://chainscript.io/). I had difficulty uncovering the implementation details of Stratumn's proof of process, as much of the available online material focuses on the implications of the technology rather than the technology itself. The most helpful resource I found was the [Epicenter Podcast #159](https://soundcloud.com/epicenterbitcoin/eb-159) titled "Richard Caetano & Anuj Das Gupta: How Stratumn Secures Processes." This investigation did not answer how digital identities are linked to physical identities in Stratumn's services. The Stratumn proof-of-process [white paper](https://stratumn.com/proof-of-process.html)does mention identity verification under "Non-Repudiation of Source and Destination", stating:

> Non-repudiation implies that the stakeholders of the information content of each and every step should not be able to deny their involvement with the steps representing their data through the digests. The tool we will use for this is Digital Signatures.

> Both Alice and Bob need to be responsible to their respective steps in such a way they they can not repudiate their involvement if challenged. The record of their identities would be maintained by having the stakeholders digitally sign the digest of their move and then storing the signatures and public keys along with the digest in the step. The private keys will not be stored in the steps; each player hold hers separately and securely. Anyone who has access to the proof can use the public key verification to ascertain whether or not Alice or Bob can be held responsible for a step.

> In this way we enable identity management and ownership in each and every step for the proof of a process to demonstrate the Who behind each and every step.

Unfortunately, this description does not explain how digital identities are linked to physical identities. How does one know whether a digital signature is actually Alice or Bob's? Stratumn even [provides a document](https://stratumn.com/pdf/use-cases/Clinical-Trials.pdf) detailing the clinical trial consent use case. However, this document does not provide an identity solution.

## Conclusion

I am marking my review as Not Approved. If the authors can show that it is not trivial to forge a specific participant's consent, I would be happy to revisit my decision. However, absent a reliable method to link a digital identity to a participant's physical identity, there is little benefit to cryptographic notarization of clinical trial consent. Such an approach is only as useful as its most vulnerable step. At a minimum, the authors need to identify the trusted parties related to participant identity.

## Minor points

The study could do a better job citing the relevant cryptographic literature. For example, the study cites neither the [Bitcoin white paper](https://bitcoin.org/bitcoin.pdf) nor the [proof-of-process white paper](https://stratumn.com/pdf/proof-of-process.pdf). In addition, the study should consider referencing [OriginStamp](https://arxiv.org/abs/1502.04015), [OpenTimestamps](https://opentimestamps.org/), and [Carlisle's 2014 blog post](http://www.bgcarlisle.com/blog/2014/08/25/proof-of-prespecified-endpoints-in-medical-research-with-the-bitcoin-blockchain/).

Figures 2 & 3 are in French. I understand that it's important to show the consent form and interface as given to the participants. However, perhaps these should be supplements with English versions in the main text.
  
The study states: "Smart contract: this is a contract that is algorithmically implemented and binds any change in the protocol to the patients’ consent seeking renewal." However, from my understanding the study does not propose any blockchain smart contracts. Instead, the Bitcoin blockchain is only used as a timestamping service.

## Positives

The study aims to replace trust with cryptography in medical research.

The study makes its source code available under a permissive open source license on [GitHub](https://github.com/benchoufi/DocChain) ([Zenodo archive](https://doi.org/10.5281/zenodo.237040)).

The study understands that directly writing every document hash to a secure & immutable blockchain will be cost prohibitive, and therefore it is necessary to "group transactions", i.e. write one transactions that attests to the existence of many chainscript hashes.

```
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA512

I have read https://doi.org/10.12688/f1000research.10531.1.
I believe I have an appropriate level of expertise to state that
I do not consider it to be of an acceptable scientific standard,
for reasons outlined above.
-----BEGIN PGP SIGNATURE-----
Version: Keybase OpenPGP v2.0.68
Comment: https://keybase.io/crypto

wsBbBAABCgAGBQJY7DVvAAoJEAOot/hH7qRdQocH9A8lOfVPDDO4SDV2NE9j8M5B
Rjtrx/mfN4qNjWWwwt2KbGKn8N8AKVMB+YoH1LCGd0LGpesmepKZKacReH2/xVwT
ARg9AddjeVh/o+LWZ4li1J30HMAt6APo6slhMEJq+Na6BdghPVD20vGnEba9e31S
cLErKqvwj9oWlKySD1CBLatIoE/dBF6EQNqOyhwBcD6cPNyElTEU/U77pQJKlr5a
YUcHgB3EicnjAhDHO0nhbjwwSdUeG31Eldn3Sx/hxGTSVX8JaZf+eVZ1dJLtnEXV
1Wk+t8i4YLm/ata3fPTT46mfHVvwi8xiK3FfdNvWeZyir2ENA7XNZ/g4DOk35g==
=Ozi4
-----END PGP SIGNATURE-----
```