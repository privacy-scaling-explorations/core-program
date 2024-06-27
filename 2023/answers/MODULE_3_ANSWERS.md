### Intro to Elliptic Curves
1. **What is the general equation for an elliptic curve?**
   - Answer: The equation of an elliptic curve is `y^2 = x^3 + ax + b`.
   
2. **How do you find the sum of two points P and Q on an elliptic curve?**
   - Answer: To add two points P and Q on an elliptic curve, you draw a line between P and Q, find the third point where that line intersects the curve, and then reflect that point over the x-axis to get the result of P + Q.
   
3. **What is the special point on the elliptic curve that serves as the identity element for addition?**
   - Answer: The identity element in elliptic curve addition is the point at infinity, often denoted as O.

### Elliptic Curve Cryptography (ECC)
1. **What is the primary advantage of ECC over traditional methods like RSA?**
   - Answer: ECC offers much shorter key lengths for the same level of security compared to traditional methods like RSA. This results in faster computations, less power consumption, and reduced storage and bandwidth requirements.
   
2. **How is the public key in ECC derived from the private key?**
   - Answer: In ECC, the public key is derived by multiplying the private key (a scalar) with a generator point G on the elliptic curve. The result is a point on the curve, which serves as the public key.
   
3. **What is the Elliptic Curve Discrete Logarithm Problem (ECDLP)?**
   - Answer: ECDLP is the problem of determining the scalar (private key) used to multiply the generator point G to arrive at a given point on the curve (public key). It's computationally difficult to solve, providing the security foundation for ECC.

### Schnorr Signatures and EdDSA
1. **What are the primary advantages of Schnorr Signatures?**
   -  Answer: Schnorr Signatures are a type of digital signature scheme based on elliptic curves. They are important because of their simplicity, efficiency, and the ability to aggregate multiple signatures into a single one due to their linear structure.

2. **What differentiates EdDSA from traditional Schnorr signatures?**
   -  Answer: EdDSA (Edwards-curve Digital Signature Algorithm) is a digital signature scheme that uses a specific type of elliptic curve called twisted Edwards curves. Unlike traditional DSA, EdDSA is deterministic, meaning the same message and private key will always produce the same signature.

### Pairing-Based Cryptography
1. **What is a pairing in the context of elliptic curve cryptography?**
   - Answer: In the context of elliptic curve cryptography, a pairing is a bilinear map that takes two points from an elliptic curve and maps them to a point in a finite field. This operation allows for certain cryptographic constructions that are not possible with just the elliptic curve operations.

2. **What are the three main properties of a bilinear map?**
   - Answer: The three main properties of a bilinear map are bilinearity, non-degeneracy, and computability.

3. **Name one cryptographic application that is enabled by pairings.**
   - Answer: Cryptographic applications enabled by pairings include BLS Signatures and Identity-Based Encryption (IBE).

### KZG Polynomial Commitments
1. **What is the primary purpose of a polynomial commitment scheme?**
   - Answer: The primary purpose of a polynomial commitment scheme is to allow a prover to commit to a polynomial in a way that they can later reveal specific evaluations of the polynomial without revealing the entire polynomial, and these evaluations can be verified against the original commitment.

2. **How is the commitment in the KZG scheme computed for a given polynomial and secret value?**
   - Answer: In the KZG scheme, the commitment to a polynomial `f(x)` is computed by evaluating the polynomial at a secret value `s` and then multiplying the result by the generator point `G` of the elliptic curve.

3. **Why are KZG polynomial commitments considered efficient and succinct?**
   - Answer: KZG polynomial commitments are considered efficient and succinct because they offer commitments and proofs that have a constant size, regardless of the degree of the polynomial. This results in compact representations and reduced computational overhead.

### Trusted Setups
1. **Why is the trusted setup phase crucial for the security of certain cryptographic protocols?**
   - Answer: The trusted setup phase is crucial because it involves generating initial parameters that are vital for the security of the protocol. If the setup is compromised, or if certain intermediate values (often called "toxic waste") are not properly discarded, they could be used to undermine the security of the system.
   
2. **How is the trusted setup related to zk-SNARKs?**
   - Answer: zk-SNARKs require a trusted setup to generate a common reference string (CRS) that is used by both the prover and verifier in the protocol. The security of zk-SNARKs relies on the fact that certain intermediate values during the CRS generation are destroyed, ensuring the integrity of the proofs.
   
3. **What are some of the challenges associated with trusted setups?**
   - Answer: Some challenges associated with trusted setups include the need for participants to trust that the setup was performed correctly and securely, the potential centralization of the setup process, and the need for transparency to gain trust from users.