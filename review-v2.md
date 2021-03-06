## Review of Version 2 of Benchoufi et al

In [version 2](https://doi.org/10.12688/f1000research.10531.2), the authors updated the manuscript and responded to [my review of version 1](https://doi.org/10.5256/f1000research.11349.r21311). I'd like to thank the authors for these additions, which provide a clearer picture of the trust model and proof of process. To assist in my review, I created a [GitHub repository](https://github.com/dhimmel/benchoufi) that includes a [diff between versions 1 and 2](https://github.com/dhimmel/benchoufi/blob/32425902d2a8500633f027dd5318df1e993b8d04/f1000/diff/f1000-benchoufi-v2-v1-diff.pdf).

## Trust model

In their response, the authors clarify who generates the private key for a given participant:

> A participant cannot simply generate any Bitcoin address and use it to sign, because the private key is created on the server by the agent (but not saved on the server), then is sent to the email address.

I believe "the agent" refers the `agent` folder of the [`benchoufi/DocChain`](https://github.com/benchoufi/DocChain/tree/ad0c71741257d8e9365230c6e57be69079ac966d) source code. In their proof of concept, the clinical trial investigators host the agent. Presumably, the agent could also be hosted by a trusted third party, such as Stratumn or a governing body like an Institutional Review Board.

It's crucial to note that the proof of process for participant consent requires complete trust in the agent. Assuming the agent is hosted by the investigators, then we must trust the investigators to have faithfully run an uncompromised agent. Hence, the proposed implementation provides an equivalent trust model to the current consent process. In both cases, one must trust the investigators to truthfully collect consent. Presently, we trust that investigators did not forge a participant's handwritten signature. In the proposed implementation, we trust that the investigators ran an agent that properly generated (and then deleted) a private key for each participant's email. For the time being, the later is perhaps even less verifiable than a handwritten signature. Regardless, the proposed digital identity solution requires a trusted party.

## Proof of process

The authors should more clearly document the proof of process underlying their approach. The Chainscript examples (the code block and Figure 4–6) are a good start. However, Figure 4–6 are poor resolution and difficult to read. More discussion of the Chainscript format along with instructions to verify a process and timestamp are needed. For example, there is no example Chainscript JSON file provided with step-by-step instructions on how to verify or evaluate it. The Chainscript code block is littered with broken JSON syntax, so it's certainly an insufficient example. With more details, additional questions may arise. For example, is the 12-byte `mapID` (with a best-case attack complexity of 2<sup>96</sup>) secure against preimage attacks? The manuscript doesn't appear to specify what hash algorithm is used.

## Smart contracts

The manuscript is misleading regarding "smart contracts" and implies that the study proposes a smart contract enrollment protocol. Specifically:

1. Figure 1 includes a smart contract step in the workflow.
2. The abstract states "a blockchain core functionality, named Smart Contract, can help prevent clinical trial events not to happen in the right chronological order".
3. The introduction states "This makes it possible to build a Smart Contract that will be executed with the only condition that patients will only be included when the enrolment is complete".

As the authors admit in their response to my review of version 1, they "did not implement" anything related to smart contracts. Implementing a smart contract to manage enrollment is not trivial. Unless the authors actually implement such a contract, they should remove claims about its utility and applicability. Discussing smart contracts in the discussion would be justified, but it's misleading to suggest that the current proposal involves smart contracts.

## Overstated blockchain usage

In their response to my review of version 1, the authors clarify that the primary achievement of the study is to create a web-based consent workflow that makes it most natural and easy to perform the proper consent process. However, the study only minimally leverages the guarantees provided by cryptography and secure blockchains. For example, the study does not achieve _trustless consent_, whereby participant consent can be provided and verified in a decentralized manner without having to trust any other parties. However, in the abstract, the authors imply the trustless & decentralized aspects of Bitcoin apply to their consent process:

> This is a distributed technology that brings a built-in layer of transparency and traceability. Additionally, it removes the need for third parties, and gives participative control to the peer-to-peer users.

In reality, the only area where a blockchain was applied is for the Chainscript timestamping. I agree this timestamping is valuable for its ability to prevent retroactive consent forgery. However, it's insufficient to verify an actual participant's identify or consent. Foremost, the use of blockchain timestamping is not sufficient to justify the grandiose claims of blockchain relevance to clinical trial consent.

In other words, the proposed consent protocol would suffer little were all blockchains to immediately disappear. The blockchain is not essential to implement more automated, web-based, and reliable consent processes. Yet the study titles itself "blockchain protocols in clinical trials" and implies that blockchains are what allows "transparency and traceability of consent". The manuscript does not adequately differentiate between speculation and the actual ways in which the study leverages blockchain technology.

For me to consider approving this study, the authors would need to drastically reduce their claims regarding the benefits of blockchain usage for clinical trial consent applications. In addition, greater clarity and focus on the specifics of their proof of concept implementation would be necessary.
