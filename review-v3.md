## Review of [Version 3 of Benchoufi et al](https://doi.org/10.12688/f1000research.10531.3)

After the previous two rounds of revision, there are still major outstanding issues. The revisions only minimally react to my previous reviews and do not include the substantial changes that would be necessary for me to approve this study. For context, see the [changes from version 2 to 3 here](https://github.com/dhimmel/benchoufi/blob/084a514838d27291aa3c3c313a7a9fd64b9a0788/f1000/diff/f1000-benchoufi-v3-v2-diff.pdf).

Here are the main factors weighing on my decision:

1. The digital signature scheme that was implemented is worthless in terms of proving that a participant consented. Hence, I entirely ignore and discount this aspect of the proposal.

2. The "proof of concept" justification provided by the authors for the methodological shortcomings and incomplete nature of their study is frustrating. The authors make statements such as (manuscript typos bolded):

  > The current implementation is an application of the **frst** principle. Ideally, we would have to build a patient authentication system which **does not relies** on any trial **stackholder**

  > It would be possible to build a Smart Contract that will be executed with the only condition that patients will only be included when the **enrolment** is complete.

  The assertion that solutions to these problems will come later is insufficient. The authors have to implement the solutions or cease promoting their benefits. In my opinion, these are unsolved problems. Implementing such solutions is difficult: suggesting that a solution exists but not offering an implementation is therefore worthless.

3. The study continuous to overstate its reliance on blockchain technology. As our previous dialogue has confirmed, the study only uses the a blockchain for timestamping. Timestamping is an important addition, but does not justify titling the study "blockchain protocols in clinical trials" nor the abundant discussion of blockchains when their role is relatively minor in the actual proposal.

To help explain my decision, I'll elaborate on the theoretically sound aspects of the authors' proposal. The following workflow is theoretically sound, albeit poorly communicated in the manuscript:

1. A webapp is created to administer an electronic consenting process. The webapp can be designed to enforce a rigid workflow that ensures the right steps are performed in the right order.

2. The user interactions and inputs from the electronic consent process can be recorded via a Chainscript JSON file. Therefore, one can store the digital equivalent of paper forms from a traditional physical consent process.

3. The Chainscript JSON file can be timestamped using the Bitcoin blockchain. This prevents predating the existence of a consent record.

Now while a clear, compelling, and clean implementation of the previous steps would be of interest, the study fails to achieve this. Specifically, the webapp is not publicly hosted, so users can experiment with and observe the proposed electronic consent implementation.

Second, the authors do not provide any Chainscript JSON files for their study. In their previous response to [my review](https://doi.org/10.5256/f1000research.12384.r22303), they link to a [Chainscript file](http://chainscript.io/#/chainmap-explorer?application=docchain&mapId=59262a2eb446491fe9d48ecb) unrelated to their study. Even more troubling is that their Chainscript example from the manuscript appears to be manually edited from an example Chainscript document rather than computer-generated output from their consent application. As I mentioned in previous review, the JSON example contains flagrant formatting errors suggesting it was created by hand. Furthermore, the Chainscript includes a `mapID` of `56c11d0ea55773bc6e681fde`. The same `mapID` is also used in the [Stratumn documentation](https://github.com/dhimmel/benchoufi/blob/084a514838d27291aa3c3c313a7a9fd64b9a0788/reference/stratumn/docs-interacting-with-your-blockchain-application.pdf), suggesting copying and pasting from the docs.

The question remains **did the study actually produce any real Chainscript JSON files or timestamp even a single Chainscript file**. It's telling that the authors still haven't revealed a Chainscript file whose past existence has been timestamped. Hence, there is no evidence that the authors actually implemented their proposed "proof of concept".

Given the severity of the outstanding issues despite the number of previous rounds of review, I do not intend to review this study again. Hence, my decision to not approve this study should be considered final.
