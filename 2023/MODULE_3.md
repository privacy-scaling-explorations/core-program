# Module 3 - Crypto Essentials: Elliptic Curves and More

Welcome to Module 3. First, we will explore the key concepts behind elliptic curves and their importance in modern cryptography. Then we will take you deeper into more advanced topics like bilinear maps, pairing-based cryptography, and KZG polynomial commitments, multi-party computation.

## Intro to Elliptic Curve Cryptography

Elliptic curve cryptography builds upon traditional cryptographic principles by applying them to the mathematical structure of elliptic curves.

For example, there exists an **Elliptic Curve Discrete Log Problem (ECDLP)**. By using elliptic curves, it has certain benefits over the regular Discrete Log Problem (DLP). These links are a good place to start:

- [Elliptic Curves - Computerphile [8:41]](https://www.youtube.com/watch?v=NF1pwjL9-DE)
- [A (relatively easy to understand) primer on elliptic curve cryptography](https://blog.cloudflare.com/a-relatively-easy-to-understand-primer-on-elliptic-curve-cryptography/)

**Elliptic Curve Digital Signature Algorithm (ECDSA)** extends the traditional Digital Signature Algorithm (DSA) by incorporating elliptic curves as well, enabling stronger security with shorter key lengths. This makes the algorithm more efficient and suitable for constrained environments. ECDSA is widely used in various secure communication protocols, including SSL/TLS.

The following StackExchange answer goes over the differences between some of the most popular digital signature protocols. It also leads into our next topic, which is another type of digital signature called the Edwards-curve Digital Signature Algorithm (EdDSA).

- [What is the difference between the RSA, DSA, and ECDSA keys that ssh uses?](https://askubuntu.com/a/1000928/733503)

## Schnorr Signatures and EdDSA (Optional)

EdDSA modifies and extends the Schnorr signature scheme to provide additional benefits. So it is crucial to first get an understanding of Schnorr signatures.

### EC-Schnorr Signatures

Schnorr signatures can also be extended to elliptic curves. A key benefit is their linear structure, which allows for multi-signature aggregation.

- [Introduction to Schnorr Signatures with Elichai Turkel](https://www.youtube.com/watch?v=XKatSGCZ-gE)
- [What Is a Schnorr Signature? (by Chainlink)](https://blog.chain.link/schnorr-signature/)
- [What The Heck Is Schnorr (by Rajarshi Maitra)](https://medium.com/bitbees/what-the-heck-is-schnorr-52ef5dba289f)
- [Introduction to Schnorr Signatures (more technical)](https://tlu.tarilabs.com/cryptography/introduction-schnorr-signatures)

Let's dive into EdDSA and see how it builds on concepts found in Schnorr Signatures.

### Edwards-curve Digital Signature Algorithm (EdDSA)

Unlike Schnorr signatures, which may use a random value for generating the signature, EdDSA takes a deterministic approach. It hashes the private key and the message together to produce the randomness, ensuring repeatability.


Suppose we have a private key `k` and a message `m`. In EdDSA, we would compute:
- `r = HASH(k || m)`
- `R = r * G`
where `G` is the base point on the curve and `R` is another point on the curve.

Just like Schnorr, the signature in EdDSA is a pair `(R, s)`, where:
- `s = (r + HASH(R || A || m) * k) mod q`

The verification checks:
- `s * G = R + HASH(R || A || m) * A`

With the values `A` (public key), `m` (message), and the signature values `R` and `s`, verification would involve checking that the left-hand and right-hand sides of the above equation match.

For more on EdDSA, check out the following links:

- [EdDSA and Ed25519](https://cryptobook.nakov.com/digital-signatures/eddsa-and-ed25519)
- [What's an EdDSA?](https://duo.com/labs/tech-notes/whats-an-eddsa)
- [Digital Signatures - ECDSA, EdDSA and Schnorr [19:50]](https://www.youtube.com/watch?v=S77ES52AGVg)

## Pairing-Based Cryptography (PBC)

Many of the following topics will depend upon what is called pairing-based cryptography. 
You can imagine pairing as the multiplication of elliptic curves. The original elliptic curve operation is homomorphically additive but not homomorphically multiplicative. Pairing is a way to mimic this "multiplication".

This is largely used in zk, especially during the verification stage. 

![Pairing](./assets/elliptic-curve-pairings.jpeg)
[Source](https://www.inevitableeth.com/home/concepts/elliptic-curve-pairings)

If you would like to know more about it, you can check out the following resources:

- **[Exploring Elliptic Curve Pairings by Vitalik Buterin (optional)](https://medium.com/@VitalikButerin/exploring-elliptic-curve-pairings-c73c1864e627)** - This resource builds upon the knowledge you learned above regarding elliptic curves and sets the stage for the topics discussed below. It is an excellent introduction to the topic.
- **[Pairings or Bilinear Maps by Alin Tomescu](https://alinush.github.io/2022/12/31/pairings-or-bilinear-maps.html)** - This resource begins with an introduction to the three fundamental properties of bilinear maps. Building on this foundation, it further explores applications such as the Tripartite Diffie-Hellman protocol, BLS signatures, and Identity-Based Encryption (IBE).

Make sure you read these two articles in full before proceeding.

### Bilinear Maps Deep Dive [Optional]

For those who desire a deeper dive into bilinear maps and pairings, check out these resources:

- [Intro to Bilinear Maps by John Bethencourt (28 slides)](https://people.csail.mit.edu/alinush/6.857-spring-2015/papers/bilinear-maps.pdf)
- [ZK and NIZK from Bilinear Maps (part1) - Jens Groth [36:04]](https://www.youtube.com/watch?v=_mAKh7LFPOU)
- [Pairings in Cryptography by Dan Boneh [1:29:48]](https://www.youtube.com/watch?v=8WDOpzxpnTE)
    - **Note:** This video is very long and technical, but can be a helpful reference.

## BLS Signatures

BLS (Boneh-Lynn-Shacham) signatures are a type of cryptographic signature scheme that allows for efficient aggregation of individual signatures into a single signature. It also makes use of pairing-based cryptography.

The intuition of BLS is that it is an aggregation signature. The image below shows how the public key and signature are aggregated. The advantage is that all signatures can be verified at once. That's why it is commonly used in consensus protocols.
![BLS](./assets/bls-signatures.jpeg)

### Optional Reading

The following articles offer a great introduction to BLS signatures and why they are important for the scaling of Ethereum (more specifically, the Beacon Chain):

- [Upgrading Ethereum (chapter on BLS Signatures) by Ben Edgington](https://eth2book.info/capella/part2/building_blocks/signatures/)
- [What is the BLS signature scheme? by David Wong](https://www.cryptologie.net/article/472/what-is-the-bls-signature-scheme/)
- [BLS Signatures by Alon Muroch - Overview (Part 1)](https://alonmuroch-65570.medium.com/bls-signatures-part-1-overview-47d9eebf1c75)
- [BLS Signatures by Alon Muroch - Key Concepts of Pairings (Part 2)](https://alonmuroch-65570.medium.com/bls-signatures-part-2-key-concepts-of-pairings-27a8a9533d0c)
- [BLS Signatures by Remco Bloemen](https://xn--2-umb.com/22/bls-signatures/)
- [BLS Signature Aggregation: Under the Hood by Stu](https://mirror.xyz/0x6afeB3d9E380787e7D0a17Fc3CA764Bb885014FA/D3g-4UPRLkAnug-p6AZYfjgXWo-psaTulyu3SaL35vg)

## KZG Polynomial Commitments

Polynomial Commitments are cryptographic tools that allow the hiding of some coefficients while revealing others. They're used in various cryptographic proofs and blockchain protocols. For a better understanding of Polynomial Commitments
The intuition of KZG is that it is a commitment scheme. It is used to commit to a polynomial and later reveal a certain point on that polynomial. All your input data "lock" a specific polynomial.

![KZG](./assets/polynomial-commitments-1.jpeg)

Read this article:
- [KZG commitment by Inevitable Ethereum](https://www.inevitableeth.com/home/concepts/kzg-commitment)

### Optional Reading

- [Polynomials](https://vitalik.eth.limo/general/2021/01/26/snarks.html#polynomials) section of Vitalik's article on zk-SNARKs.
- [KZG in Practice: Polynomial Commitment Schemes and Their Usage in Scaling Ethereum](https://scroll.io/blog/kzg)

KZG Polynomial Commitments is another technology that relies on pairing-based cryptography. The protocol is built upon pairing-friendly elliptic curves and bilinear properties. With this protocol, both the proof and commitment size is constant, no matter the degree of the polynomial being used.

Scroll's zk-rollup implementation makes use of this commitment scheme to commit to computations executed on an L2. While Ethereum’s Proto-Danksharding proposal ([EIP-4844](https://www.eip4844.com)) uses it to commit to data blobs.

- [KZG in Practice by Scroll](https://scroll.io/blog/kzg)
- [KZG Polynomial Commitments by Dankrad Feist](https://dankradfeist.de/ethereum/2020/06/16/kate-polynomial-commitments.html)
- [KZG Polynomial Commitments by Alin Tomescu](https://alinush.github.io/kzg)

## Trusted Setup

The concept of a trusted setup is an important part of the KZG Polynomial commitment scheme, and indeed part of the wider culture of Ethereum. Here are a few resources to learn more about trusted setups.

The intuition of a trusted setup is that it is a process to generate a bunch of points on the elliptic curve, and the prover will input these points to the polynomial commitment. Therefore the output is a point on the curve as well. Specifically, the generation of these points require many people join and discard the secret value (which they used to create the point). It should not be possible to generate the points without this. That's why it is called a trusted setup.

### Optional Reading

- [How do trusted setups work? by Vitalik Buterin](https://vitalik.eth.limo/general/2022/03/14/trustedsetup.html)
- [On-Chain Trusted Setup Ceremony by a16zcrypto](https://a16zcrypto.com/posts/article/on-chain-trusted-setup-ceremony/)
- [The KZG Ceremony - or How I Learnt to Stop Worrying and Love Trusted Setups by Carl Beekhuizen [27:27]](https://www.youtube.com/watch?v=dTBy661ubgg)
- [Trusted Setup by 0xParc [48:42]](https://learn.0xparc.org/materials/circom/learning-group-1/trusted-setup/)

### Multi-Party Computation (MPC) [Optional]

[Secure Multi-Party Computation](https://en.wikipedia.org/wiki/Secure_multi-party_computation) or MPC for short, is a protocol that allows multiple entities to jointly compute a function without revealing their individual inputs.

The classic example of MPC is the [Yao's Millionaire Problem](https://en.wikipedia.org/wiki/Yao%27s_Millionaires%27_problem). This is a thought experiment in which two millionaires are interested in knowing which of them is richer without revealing their actual wealth.

MPC can be used to generate the secret value and the SRS for a trusted setup in a distributed manner, where multiple parties collaborate to generate the parameters without any single party having access to the entire secret value.

- [Introduction to Multi-Party Computation (MPC or SMPC) [5:43]](https://www.youtube.com/watch?v=90jcXCHsBF0)
- [Sharing Knowledge without Sharing Data by Azer Bestavros [32:08]](https://www.youtube.com/watch?v=P2MmO458xu4)
- [Accessible and Scalable: Secure Multi-Party Computation](https://multiparty.org/)
- [Intro to MPC (Javascript tutorial and examples)](https://github.com/multiparty/jiff/blob/master/tutorials/0-intro-to-mpc.md)

# 💪 Exercises

Answer the following questions (in as much detail as you desire):

## Intro to Elliptic Curves

1. What is the general equation for an elliptic curve?
2. How do you find the sum of two points P and Q on an elliptic curve?
3. What is the special point on the elliptic curve that serves as the identity element for addition?

## Elliptic Curve Cryptography

1. What is the primary advantage of ECC over traditional methods like RSA?
2. How is the public key in ECC derived from the private key?
3. What is the Elliptic Curve Discrete Logarithm Problem (ECDLP)?

## Schnorr Signatures and EdDSA

1. What are the primary advantages of Schnorr Signatures?
2. What differentiates EdDSA from traditional Schnorr signatures?

## Pairing-Based Cryptography

1. What is a pairing in the context of elliptic curve cryptography?
2. What are the three main properties of a bilinear map?
3. Name one cryptographic application that is enabled by pairings.

## KZG Polynomial Commitments

1. What is the primary purpose of a polynomial commitment scheme?
2. How is the commitment in the KZG scheme computed for a given polynomial and secret value?
3. Why are KZG polynomial commitments considered efficient and succinct?

## Trusted Setup

1. Why is the trusted setup phase crucial for the security of certain cryptographic protocols?
2. How is the trusted setup related to zk-SNARKs?
3. What are some of the challenges associated with trusted setups?
