## Homomorphic Hiding

1. **Explain homomorphic hiding in your own words.**

   - Answer: Homomorphic hiding refers to a cryptographic commitment scheme that allows for specific operations to be performed on the committed data without revealing the data itself. In other words, you can perform computations on hidden values, and the results, when revealed, will be the same as if the computations were done on the original, non-hidden values.

---

## Arithmetic Circuits

1. **What is the primary purpose of converting a problem into an arithmetic circuit?**

   - Answer: Converting a problem into an arithmetic circuit allows for the representation of complex computations in a structured and standardized format. This "flattening" into simpler equations makes it easier to transform the computation into other representations, like R1CS, which are more amenable to zkSNARK constructions.

2. **What are the main components of an arithmetic circuit?**

   - Answer: The main components of an arithmetic circuit are gates (which perform operations like addition or multiplication), wires (which carry values between gates), and input/output ports (which define the inputs to and outputs from the circuit).

---

## Rank-1 Constraint System (R1CS)

1. **Describe the Rank-1 Constraint System (R1CS) in your own words.**

   - Answer: R1CS is a system of representing computations using a set of matrices. It takes the structure provided by arithmetic circuits and further simplifies it into a format where each constraint (or equation) ensures that specific operations are correctly performed. Each constraint is designed to be rank-1, meaning it can be represented with a single row or column in a matrix.

2. **Why is R1CS essential in the zkSNARK construction pipeline?**

   - Answer: R1CS is essential because it provides a bridge between arithmetic circuits and QAPs. It simplifies the computation into a format that can be efficiently transformed into a QAP, which is a polynomial representation suitable for zkSNARK proof generation.

---

## Quadratic Arithmetic Program (QAP)

1. **What is the primary goal of converting R1CS into a QAP?**

   - Answer: The primary goal is to represent the computation in a polynomial format. QAPs allow for the efficient generation and verification of zkSNARK proofs by leveraging the properties of polynomials.

2. **How does QAP aid in the zkSNARK proof generation process?**

   - Answer: QAPs provide a structured way to represent the computation such that proving knowledge of a solution (or satisfying assignment) to the computation becomes equivalent to proving knowledge of certain polynomial evaluations. This polynomial representation is amenable to the cryptographic techniques used in zkSNARKs.

3. **Why are polynomials central to the QAP representation?**

   - Answer: Polynomials are central because they offer properties that make the zkSNARK construction efficient. Operations on polynomials, like evaluation and interpolation, are used to generate and verify proofs. The structure of polynomials also allows for the creation of succinct and zero-knowledge proofs, which are the hallmarks of zkSNARKs.

---

## The Pinocchio Protocol

1. **Why is the Pinocchio Protocol considered a significant step towards practical zkSNARK construction?**

   - Answer: The Pinocchio Protocol was one of the first to demonstrate a practical construction of zkSNARKs. It provided a clear methodology for taking a computation, represented as a QAP, and generating a succinct, non-interactive proof of its correctness.

2. **How does the Pinocchio Protocol utilize QAP representations?**

   - Answer: The Pinocchio Protocol builds upon the QAP representation to generate zkSNARK proofs. The protocol uses the polynomial structure of QAPs, combined with cryptographic techniques like pairings on elliptic curves, to produce proofs that are both short in size and verifiable in a few milliseconds.

3. **What role do elliptic curve pairings play in the Pinocchio Protocol?**

   - Answer: Elliptic curve pairings provide the cryptographic foundation for the Pinocchio Protocol. They are used in the proof generation and verification processes, enabling the creation of proofs that are both zero-knowledge and succinct. Pairings allow for certain mathematical checks that make the verification of zkSNARK proofs efficient.

---

## Groth16

1. **What makes Groth16 a popular choice for zkSNARK constructions in blockchain technologies?**

   - Answer: Groth16 is popular because of its efficiency. It produces shorter proofs and requires less computational power for proof generation and verification compared to earlier zkSNARK constructions. This efficiency makes it well-suited for blockchain technologies where resource constraints are a concern.

2. **Describe the main advantage and disadvantage of the Groth16 proof system.**

   - **Advantage**: Groth16 is highly efficient, producing succinct proofs and allowing for fast verification. This makes it ideal for systems where performance is critical.
   - **Disadvantage**: Groth16 requires a circuit-specific trusted setup, which can be a significant downside for some use-cases due to the potential security risks associated with the setup phase.

3. **How does Groth16 differ from the original Pinocchio Protocol?**

   - Answer: Groth16 improves upon the Pinocchio Protocol by producing shorter proofs and allowing for faster verification. Additionally, while both require a trusted setup, Groth16's setup is circuit-specific, whereas the Pinocchio Protocol's setup is more general.

---

## PLONK

1. **What are the advantages of PLONK over Groth16?**

   - Answer: PLONK offers a "universal and updateable" trusted setup, eliminating the need for a new trusted setup for every circuit. This makes it more versatile and reduces the security concerns associated with multiple setup phases. Additionally, PLONK is designed to be more modular and flexible, allowing for easier integration with various cryptographic primitives.

2. **How does PLONK eliminate the need for a new trusted setup for every circuit?**

   - Answer: PLONK utilizes a universal trusted setup, which means that the setup phase is done once and can be used for any circuit of a given size or smaller. This contrasts with circuit-specific setups where a new setup is required for each new circuit. The universality of PLONK's setup reduces the overhead and potential security risks associated with multiple setups.