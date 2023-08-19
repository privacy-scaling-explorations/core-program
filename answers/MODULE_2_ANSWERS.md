### Written Questions

1. **Symmetric vs. Asymmetric Encryption**:
   - **Symmetric Encryption**: Uses the same key for both encryption and decryption. It is faster and less complex, but the key must be shared securely between parties. 
     * *Use case*: Securely transmitting data over a trusted channel, such as an encrypted WiFi connection.
   - **Asymmetric Encryption**: Utilizes a pair of keys: a public key for encryption and a private key for decryption. It ensures that the private key does not need to be shared but is more computationally intensive.
     * *Use case*: Secure email systems like PGP, where the recipient's public key encrypts the message, and only the recipient's private key can decrypt it.

2. **Public-Key Cryptography and Key Exchange Protocols**:
   - *Answer*: Diffie-Hellman protocol allows two parties to generate a shared secret key securely over an untrusted network. It enhances security in a messaging application by enabling encrypted communication without sharing the actual keys.
     * *Use case*: Securely exchanging messages in apps like WhatsApp, allowing for end-to-end encryption.

3. **Hash Functions**:
   - *Answer*: SHA-256 is well-regarded for its resistance to collisions, preimage attacks, and speed. Poseidon, on the other hand, is tailored for cryptographic purposes with a more efficient arithmetic design.
     * *Unique advantage of Poseidon*: Its design is particularly suited for zero-knowledge proofs, providing more efficient computations in that context.

4. **Merkle Trees**:
   - *Answer*: Merkle trees help verify data in a large database efficiently by structuring the data into a binary tree where each leaf is a hash of a data block, and each non-leaf node is a hash of its child nodes. Verifying the inclusion of a specific block only requires the hashes along the path to the root, not the entire dataset.
     * *Use case*: Verifying transactions in a blockchain, where the Merkle root represents all transactions in a block.

5. **Cryptographic Commitments**:
   - *Answer*: Pedersen Commitments allow committing to a value without revealing it, maintaining transaction privacy in a blockchain protocol. By combining randomness with the actual value, it ensures the commitment is both hiding and binding.
     * *Use case*: Confidential transaction systems within blockchains like Monero to keep amounts private.

6. **Digital Signatures**:
   - *Answer*: To verify the authenticity of a digitally signed document, one must use the public key corresponding to the signer's private key to apply the signature verification algorithm. If verification succeeds, it proves the document was signed by the corresponding private key and has not been altered.

### Programming Challenges

#### Challenge 1: Asymmetric Encryption and Digital Signature

```javascript
const crypto = require('crypto');

// Asymmetric encryption
const { publicKey, privateKey } = crypto.generateKeyPairSync('rsa', { modulusLength: 2048 });

// Encrypt
const plaintext = 'This is a secret message.';
const encrypted = crypto.publicEncrypt(publicKey, Buffer.from(plaintext));

// Decrypt
const decrypted = crypto.privateDecrypt(privateKey, encrypted);
console.log('Decrypted message:', decrypted.toString());

// Create a digital signature
const sign = crypto.createSign('SHA256');
sign.update(plaintext);
sign.end();
const signature = sign.sign(privateKey);

// Verify a digital signature
const verify = crypto.createVerify('SHA256');
verify.update(plaintext);
verify.end();
console.log('Signature valid:', verify.verify(publicKey, signature));
```

#### Challenge 2: Hashing with SHA-256 and Poseidon

```javascript
const crypto = require("crypto");
const poseidon = require("poseidon-encryption");

// SHA-256
const data = "This is some data X.";
const hash = crypto.createHash("sha256");
hash.update(data);
const sha256Hash = hash.digest("hex");
console.log("SHA-256 Hash:", sha256Hash);

// Poseidon
const inputs = [1, 2, 3, 4, 5];
const poseidonHash = poseidon.poseidon(inputs);
console.log("Poseidon Hash:", poseidonHash.toString());
```

#### Challenge 3: Using a Simple Merkle Tree

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
const tree = new MerkleTree.MerkleTree(leaves, hashFunction);
const root = tree.getRoot().toString('hex');
console.log('Merkle Root:', root);

// Generate and verify proof
const leaf = hashFunction('b');
const proof = tree.getProof(leaf);
console.log('Proof valid:', tree.verify(proof, leaf, tree.getRoot()));
```

#### Challenge 4: Implementing Pedersen Commitments

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
    this.r = BigInt(Math.floor(Math.random() * 10 + 1));
    this.h = this.g ** this.r % this.p;
  }

  // Generate the commitment (g^s * h^r mod p)
  generateCommitment(s) {
    this.s = BigInt(s);
    return (this.g ** BigInt(s) * this.h ** this.r) % this.p;
  }

  // Reveal the secret number and random number (s, r)
  reveal() {
    return { s: this.s, r: this.r };
  }

  // Verify the commitment (g^s * h^r mod p)
  verify(s, r, C) {
    return C === (this.g ** BigInt(s) * this.h ** BigInt(r)) % this.p;
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