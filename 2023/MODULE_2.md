# Module 2 - Crypto Primitives: Encryption, Hash Functions, and Beyond

Welcome to Module 2! As we delve deeper into the world of cryptography and zero-knowledge proofs, this module will introduce you to encryption, hash functions, and various advanced cryptographic concepts. By mastering these core building blocks, we will better understand the practical implementation of these technologies in areas like blockchain and beyond. 

# Detailed Self Study

The following is a list of topics for you to research and learn about. At the bottom of each section is a set of questions for you to check your understanding. Try to make sure that you can confidently answer the questions before moving on. Feel free to reach out on Discord if you are struggling with a certain topic.

## Symmetric vs. Asymmetric Encryption

Encryption is a technique used to encode data, making it readable only to those who possess the correct decryption key. There are two main types of encryption - symmetric and asymmetric, each serving different purposes and with their own strengths and weaknesses.

**Symmetric Encryption** - Also known as single-key encryption, this method involves using the same key for both encryption and decryption. The most widely used symmetric encryption algorithm is Advanced Encryption Standard (AES).

**Asymmetric Encryption** - Also known as public-key encryption, this method uses a pair of keys: one for encryption and another for decryption. The RSA algorithm is one of the best-known public-key algorithms.

The key difference between the two is the number of keys used: symmetric encryption uses one key for both encrypting and decrypting, while asymmetric encryption uses a different key for each (one public, one private). For a deeper understanding of symmetric and asymmetric encryption, please explore these resources:
- [Symmetric vs. Asymmetric Encryption – What are differences?](https://www.ssl2buy.com/wiki/symmetric-vs-asymmetric-encryption-what-are-differences)
- [AES Explained (Advanced Encryption Standard) - Computerphile [14:13]](https://www.youtube.com/watch?v=O4xNJsjtN6E)
- [Prime Numbers & RSA Encryption Algorithm - Computerphile [15:06]](https://www.youtube.com/watch?v=JD72Ry60eP4)
- [What Is AES Encryption and How Does It Work?](https://www.simplilearn.com/tutorials/cryptography-tutorial/aes-encryption)
- [What is RSA encryption and how does it work?](https://www.comparitech.com/blog/information-security/rsa-encryption/)


:::info
**🤔 Consider the following:**
1. What is the primary difference between symmetric and asymmetric encryption?
2. Can you briefly explain how AES (Advanced Encryption Standard) works?
3. What makes RSA a popular choice for public-key encryption? 
:::

## DLP-based Public-Key Cryptography
While RSA encryption is based on the hardness of the factoring problem, there is another public key cryptography system based on hardness of Discrete Logarithm Problem (DLP).

1. **Discrete Log Problem (DLP):** This is a cornerstone problem in public-key cryptography and underlies many key exchange and encryption algorithms. Understanding DLP provides a foundation for the remaining topics.
    - [The Discrete Logarithm Problem - Khan Academy [1:55]](https://youtu.be/SL7J8hPKEWY)
    - [Public key cryptography using discrete logarithms](https://www.di-mgt.com.au/public-key-crypto-discrete-logs-0.html)

2. **Diffie-Hellman Key Exchange:** This is one of the earliest practical implementations of key exchange protocols based on the Discrete Log Problem. It's critical to understand how secure communication can be established over insecure channels.

    This protocol is significant as it enables secure communication over insecure channels by allowing two parties to generate a shared secret key, which can then be used for encryption and decryption of messages
    - [Secret Key Exchange (Diffie-Hellman) - Computerphile [8:39]](https://www.youtube.com/watch?v=NmM9HA2MQGI)
    - [Diffie Hellman -the Mathematics bit- Computerphile [7:04]](https://youtu.be/Yjrfm_oRO0w)
    - [Implementation of Diffie-Hellman Algorithm
](https://www.geeksforgeeks.org/implementation-diffie-hellman-algorithm/)

3. **ElGamal Encryption:** This is a public-key encryption method that utilizes the principles of DLP. This will allow you to see a practical application of these abstract concepts in a real-world encryption scheme.
    - [Intro to the ElGamal Cryptosystem [8:20]](https://www.youtube.com/watch?v=oQqr8d5s3Uk)
    - [The ElGamal Algorithm: a simple example [6:38]](https://www.youtube.com/watch?v=4xVCrTb_1II)
    - [ElGamal Encryption Algorithm](https://www.geeksforgeeks.org/elgamal-encryption-algorithm/)

:::info
**🤔 Consider the following:**
1. What is the Discrete Logarithm Problem (DLP)?
2. How does the Diffie-Hellman protocol work?
3. What is the main idea behind ElGamal encryption?
4. Can you name a drawback of using DLP-based systems?
:::

## Hash Functions

A hash function takes an input and returns a fixed-size string of bytes. **SHA-256** and **Poseidon** are popular cryptographic hash functions in our context, with Poseidon specifically designed for arithmetic-friendly operations, benefiting certain applications in blockchains.

The primary characteristics of a good hash function are [preimage resistance](https://en.wikipedia.org/wiki/Preimage_attack), second preimage resistance, and [collision resistance](https://en.wikipedia.org/wiki/Collision_resistance), ensuring data security and integrity. In blockchain technology, hash functions create an unalterable, unique representation of each block's content, contributing to the immutability and transparency of the system.

Explore these resources to further your understanding:
- [What Is SHA-256 Algorithm & How It Works](https://www.ssldragon.com/blog/sha-256-algorithm/)
- [How is SHA-256 used in blockchain, and why?](https://www.educative.io/answers/how-is-sha-256-used-in-blockchain-and-why)
- [Poseidon: A new hash function for zero-knowledge proof systems](https://eprint.iacr.org/2019/458.pdf)
- [USENIX Security '21 - Poseidon: A New Hash Function for Zero-Knowledge Proof Systems [10:45]](https://www.youtube.com/watch?v=hUx3WpDV_l0)
    - This video is quite technical, but the first few minutes provide a good explanation for the motivation behind the Poseidon hash function.

:::info
**🤔 Consider the following:**
1. What is a hash function and what are its primary uses in cryptography?
2. How does the SHA-256 hashing algorithm function, in simple terms?
3. What is the Poseidon hash function and why is it particularly useful in ZKPs?
:::

## Merkle Trees

A Merkle tree is a core component of blockchain and cryptography. It's a binary tree filled with cryptographic hashes. This structure enables efficient and secure verification of the contents of large data structures. To understand more about Merkle trees, read the following:
- [How Merkle Trees Enable the Decentralized Web! [10:05]](https://www.youtube.com/watch?v=3giNelTfeAk)
- [Merkle Trees and Merkle Roots Explained](https://academy.binance.com/en/articles/merkle-trees-and-merkle-roots-explained)
- [Visualizing Efficient Merkle Trees for Zero-Knowledge Proofs](https://kndrck.co/posts/efficient-merkletrees-zk-proofs/)
- [The Ultimate Merkle Tree Guide in Solidity](https://soliditydeveloper.com/merkle-tree)


:::info
**🤔 Consider the following:**
1. Can you describe the structure of a Merkle tree?
2. How are Merkle trees used within the blockchain context?
3. Why are Merkle trees useful for efficient and secure verification of large data structures?
:::

## Cryptographic Commitments

Cryptographic commitments are essential in cryptography and blockchain technology as they allow for selective hiding and revealing of information. This feature ensures data privacy while still enabling verification processes.

It helps achieve secure and efficient verification of transactions in blockchain protocols. In such contexts, sensitive information, such as transaction details or user identities, is hidden while revealing others for the verifier to authenticate the transactions.

You can break down the concept of commitment into two parts: commit and open (reveal).

![commitment scheme](./assets/commitment.png)
[Source](https://zecrey.medium.com/commmitment-schemes-in-zecrey-e6c446e2da97)

There is always a commit phase and a reveal phase, in other words you first encrypt a secret and then reveal it later.

### Pedersen Commitments (Optional)
Pedersen Commitments are a type of cryptographic primitive that allows you to commit to a certain value while keeping it hidden, with the ability to disclose the committed value later. They're often used to achieve privacy-preserving properties in cryptographic protocols. For more on Pedersen Commitments, review these materials:

- [Pedersen Commitments](https://asecuritysite.com/encryption/ped)
- [What is a Pedersen Commitment?](https://crypto.stackexchange.com/questions/64437/what-is-a-pedersen-commitment)

As a final touch on this section, [this video [10:32]](https://www.youtube.com/watch?v=IkNZWJFcfcU) provides a brief yet comprehensive summary of the fundamental concepts discussed in this section.

:::info
**🤔 Consider the following:**
1. What is the main purpose of Cryptographic Commitments?
2. What type of information does a Polynomial Commitment hide and reveal?
3. How do Pedersen Commitments contribute to privacy in cryptography?
4. Why are Cryptographic Commitments important in blockchain technology?
:::

## Digital Signatures

Digital signatures ensure the integrity and authenticity of digital messages or documents. By providing a means to verify the origin and confirm that the content has not been altered, digital signatures play a pivotal role in maintaining trust in digital communications.

In PKC, anyone can encrypt their message with the receiver's public key, and only the receiver can decrypt the message with their private key. In digital signatures, on the other hand, if a signer generates a signature for a message using their private key, anyone can validate it using the signer's public key. Therefore, the message of the signature is made public, which distinguishes it from cryptographic commitments.

Start your exploration of digital signatures with this intuitive video:
- [What are Digital Signatures? - Computerphile [10:16]](https://www.youtube.com/watch?v=s22eJ1eVLTU)

**Schnorr Signature**: Schnorr signatures are a digital signature scheme known for their simplicity and efficiency.
- [Schnorr Digital Signature (by GeeksForGeeks)](https://www.geeksforgeeks.org/schnorr-digital-signature/)
- [Schnorr Digital Signature [4:58]](https://www.youtube.com/watch?v=mV9hXEFUB6A)

**Exploring DSA**: Get a deep dive into the Digital Signature Algorithm (DSA) and its significance in bolstering internet security. Through the listed resources, understand the mechanics of DSA and its use cases.
- [Digital Signature Algorithm (DSA) in Cryptography](https://www.simplilearn.com/tutorials/cryptography-tutorial/digital-signature-algorithm)
- [Digital Signature Algorithm (DSA) - Cryptography [5:46]](https://www.youtube.com/watch?v=iS1nK4G6EtA)
- [Digital Signature Algorithm (DSA) explained with example [24:32]](https://www.youtube.com/watch?v=MtT3NBfpV5Q)

:::info
**🤔 Consider the following:**
1. Can you describe what digital signatures are and why they are essential in digital communications?
2. Explain the workings of the Digital Signature Algorithm (DSA).
:::

# 💪 Exercises

## Written Questions

1. **Symmetric vs. Asymmetric Encryption**: What are the key differences between symmetric and asymmetric encryption? Provide a practical use case for each.
2. **Public-Key Cryptography and Key Exchange Protocols**: How can the Diffie-Hellman protocol enhance security in a messaging application?
3. **Hash Functions**: What features make SHA-256 and Poseidon good hash functions for ensuring data integrity? Mention one unique advantage of Poseidon.
4. **Merkle Trees**: Explain how Merkle trees can help verify data in a large database efficiently.
5. **Cryptographic Commitments**: How can Pedersen Commitments be used in a blockchain protocol to maintain transaction privacy?
6. **Digital Signatures**: How can you verify the authenticity of a digitally signed document?

## Programming Challenges

In these challenges, you'll implement cryptographic methods in a Node.js environment. You will need the following packages, which you can install using NPM:

```bash
npm install merkletreejs poseidon-encryption ffjavascript
```

### Challenge 1: Asymmetric Encryption and Digital Signature

In this challenge, you will use the `crypto` built-in library in Node.js to implement asymmetric encryption. Your task is to encrypt and decrypt some sample text, generate a digital signature for the encrypted message, and then verify it. This simulates a secure message exchange where you want to ensure the confidentiality and authenticity of the messages.

```javascript
const crypto = require('crypto');

// Asymmetric encryption
const { publicKey, privateKey } = crypto.generateKeyPairSync('rsa', { modulusLength: 2048 });

// Encrypt
const plaintext = 'This is a secret message.';
// TODO: Use the publicKey to encrypt the plaintext message. Remember that RSA encryption is public key encryption.

// Decrypt
// TODO: Use the privateKey to decrypt the encrypted message. The result should be the original plaintext.

// Create a digital signature
const sign = crypto.createSign('SHA256');
sign.update(plaintext);
sign.end();
// TODO: Use the privateKey to sign the plaintext message. This will generate a digital signature.

// Verify a digital signature
const verify = crypto.createVerify('SHA256');
verify.update(plaintext);
verify.end();
// TODO: Use the publicKey to verify the signature. It should return true if the signature is valid.
```

Tip: The `crypto` library has specific functions for encryption, decryption, signing, and verifying. Look up the library documentation for examples and usage [here](https://nodejs.org/api/crypto.html).

### Challenge 2: Hashing with SHA-256 and Poseidon

For this challenge, your task is to compute the SHA-256 and Poseidon hashes of some input data. You will then observe how the hash value changes drastically even with a small change in the input data. This is an important property of cryptographic hash functions called ["avalanche effect"](https://en.wikipedia.org/wiki/Avalanche_effect).

```javascript
const crypto = require("crypto");
const poseidon = require("poseidon-encryption");

// SHA-256
const data = "This is some data X.";
// TODO: Compute the SHA-256 hash of the data and print it. Try changing the data slightly and observe the changes in the hash.

// Poseidon
const inputs = [1, 2, 3, 4];
// TODO: Compute the Poseidon hash of the inputs and print it. Remember that Poseidon accepts an array of integers as input.
```

Tip: Use the `.digest('hex')` method of the `hash` object to print the hash in a human-readable format. As for the `poseidon-encryption` package, there lacks good documentation but have a look at the source code [here](https://github.com/weijiekoh/circomlib/tree/feat/poseidon-encryption) for some hints (pay special attention to the tests for example usage).

### Challenge 3: Using a Simple Merkle Tree

In this challenge, you will use the 'merkletreejs' library to construct a simple Merkle Tree from some input data. You will then generate a proof for a leaf node and verify it. This task is analogous to verifying a transaction in a block in a blockchain.

```javascript
const MerkleTree = require('merkletreejs');
const crypto = require('crypto');

function hashFunction(data) {
  const hash = crypto.createHash('sha256');
  hash.update(data);
  return hash.digest();
}

// Create tree
const leaves = ['a', 'b', 'c', 'd'].map(x => hashFunction(x));
// TODO: Build the Merkle tree using the leaves and hashFunction. Compute the root of the tree and print it.

// Generate and verify proof
const leaf = hashFunction('b');
// TODO: Generate a proof for the leaf 'b' and verify it against the root of the tree. It should return true if the leaf is part of the tree.
```

Tip: Refer to the `merkletreejs` library [documentation](https://github.com/merkletreejs/merkletreejs) for the functions needed to build the tree, generate the proof, and verify it.

### Challenge 4: Implementing Pedersen Commitments

This challenge is a little more involved, but should be more rewarding. Here, you will be creating a Javascript object capable of Pedersen Commitments. This template should get you started:

```javascript
class PedersenCommitment {
  constructor() {
    // Set prime number (p) and generator (g)
    this.p = BigInt(23); // use a large prime in a real-world scenario
    this.g = BigInt(4); // use a large number in a real-world scenario
    this.h = null;
    this.r = null;
    this.s = null;
  }

  // Generate 'h' with a random number 'r' (h = g^r mod p)
  generateH() {
    // TODO: Generate a random number r (and save it to this.r)
    // TODO: Calculate h using g, r and p (and save it to this.h)
  }

  // Generate the commitment (g^s * h^r mod p)
  generateCommitment(s) {
    // TODO: Convert s to BigInt (and save it to this.s)
    // TODO: Calculate and return the commitment using g, s, h, r and p
  }

  // Reveal the secret number and random number (s, r)
  reveal() {
    // TODO: Return the secret and random number
  }

  // Verify the commitment (g^s * h^r mod p)
  verify(s, r, C) {
    // TODO: Verify the commitment by recalculating it and comparing with C
  }
}

// Test the PedersenCommitment
const pc = new PedersenCommitment();
pc.generateH();

// Party A: Generate a commitment
let secretNumber = 7;
let commitment = pc.generateCommitment(secretNumber);
console.log("Commitment: ", commitment);

// Party A: Reveal the secret and random number
let reveal = pc.reveal();
console.log("Revealed: ", reveal);

// Party B: Verify the commitment
let verification = pc.verify(reveal.s, reveal.r, commitment);
console.log("Verification: ", verification);
```

If everything worked properly, the final output should read:

```
Verification:  true
```

Congrats on reaching the end of this module!

## Conclusion

In summary, we've ventured through some very important cryptographic primitives, gaining insights into encryption, hash functions, Merkle trees, and more. These components underpin blockchain technologies and zero-knowledge proofs. Moving forward, our next module will navigate the fascinating field of elliptic curve cryptography.
