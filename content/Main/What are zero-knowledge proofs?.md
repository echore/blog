---
share: true
---
2025-08-24  20:23
Tags:[[Web3|Web3]]

https://youtu.be/fOGdb1CTu5c?si=We1qG9Yx9XTfjEh0

A **Zero-Knowledge Proof** is a way for someone to prove they know something (like a secret) without actually sharing the secret itself.

## Use-cases for zero-knowledge proofs
### Anonymous payments

Credit card payments are often visible to multiple parties, including the payments provider, banks, and other interested parties (e.g., government authorities). While financial surveillance has benefits for identifying illegal activity, it also undermines the privacy of ordinary citizens.

Cryptocurrencies were intended to provide a means for users to conduct private, peer-to-peer transactions. But most cryptocurrency transactions are openly visible on public blockchains. User identities are often pseudonymous and either wilfully linked to real-world identities (e.g. by including ETH addresses on Twitter or GitHub profiles) or can be associated with real-world identities using basic on and offchain data analysis.

### Identity protection

Current identity management systems put personal information at risk. Zero-knowledge proofs can help individuals validate identity whilst protecting sensitive details.

### Proof of Humanity

One of the most widely used examples of zero-knowledge proofs in action today is the [World ID protocolopens in a new tab](https://world.org/blog/world/world-id-faqs), which can be thought of as “a global digital passport for the age of AI.” It allows people to prove they are unique individuals without revealing personal information. This is achieved through a device called the Orb, which scans a person's iris and generates an iris code.

### Authentication

Using online services requires proving your identity and right to access those platforms. This often requires providing personal information, like names, email addresses, birth dates, and so on. You may also need to memorize long passwords or risk losing access.

Zero-knowledge proofs, however, can simplify authentication for both platforms and users. Once a ZK-proof has been generated using public inputs (e.g., data attesting to the user's membership of the platform) and private inputs (e.g., the user's details), the user can simply present it to authenticate their identity when they need to access the service. This improves the experience for users and frees organizations from the need to store huge amounts of user information. 
I feel like this kind of has business potential.

### Verifiable computation

Verifiable computation is a method that allows you to **outsource computation** (like doing math or processing transactions) to another entity or computer. But here’s the key part: even though you outsource the work, you can **verify** that the work was done correctly. This is done using **Zero-Knowledge Proofs**.

- **Why it's useful**: It allows systems like Ethereum to run faster without compromising security, because it doesn't need to do all the calculations itself—other computers do the heavy lifting, and Ethereum can check the results easily.

## How do zero-knowledge proofs work?

A zero-knowledge protocol must satisfy the following criteria:

1. **Completeness**: If the input is valid, the zero-knowledge protocol always returns ‘true’. Hence, if the underlying statement is true, and the prover and verifier act honestly, the proof can be accepted.
    
2. **Soundness**: If the input is invalid, it is theoretically impossible to fool the zero-knowledge protocol to return ‘true’. Hence, a lying prover cannot trick an honest verifier into believing an invalid statement is valid (except with a tiny margin of probability).
    
3. **Zero-knowledge**: The verifier learns nothing about a statement beyond its validity or falsity (they have “zero knowledge” of the statement). This requirement also prevents the verifier from deriving the original input (the statement’s contents) from the proof.

### Non-interactive zero-knowledge proofs

While revolutionary, interactive proving had limited usefulness since it required the two parties to be available and interact repeatedly. Even if a verifier was convinced of a prover’s honesty, the proof would be unavailable for independent verification (computing a new proof required a new set of messages between the prover and verifier).

Unlike interactive proofs, noninteractive proofs required only one round of communication between participants (prover and verifier). The prover passes the secret information to a special algorithm to compute a zero-knowledge proof. This proof is sent to the verifier, who checks that the prover knows the secret information using another algorithm.

Non-interactive proving reduces communication between prover and verifier, making ZK-proofs more efficient. Moreover, once a proof is generated, it is available for anyone else (with access to the shared key and verification algorithm) to verify.