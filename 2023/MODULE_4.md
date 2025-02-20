# Module 4 - zkSNARKs

In this module, we will "look under the hood" of zkSNARKs and acquire an understanding of how zkSNARKs are constructed. To set the stage, we will introduce the concepts of homomorphic hiding and blind evaluation.

Then we will go through the process of converting a computation into a zkSNARK, starting from arithmetic circuits, to R1CS and QAP. Finally, we will explore some common proof systems like Groth16 and Plonk.

## 1. From Computation to QAP

Now that you have a general idea of the topics above, let's turn to the "pipeline" of a zkSNARK construction.

The goal of our construction is to be able to create a proof that a particular computation was properly executed. In order to do that, we must first transform it into a special form.

### 1.1 Arithmetic Circuits

First, we need to convert our problem into something called an [arithmetic circuit](https://en.wikipedia.org/wiki/Arithmetic_circuit_complexity). This allows us to take an equation and "flatten" it into a series of simpler equations. Read the following:

- The **Arithmetic Circuits** section of this [**Electric Coin article**](https://electriccoin.co/blog/snark-explain5/)
- The **Flattening** section of this [**0xParc article**](https://learn.0xparc.org/materials/circom/additional-learning-resources/R1CS%20Explainer#step-1-flattening)
- The following two posts in this series by Maurizio Binello:
    - [**From Theory to Practice**](https://www.zeroknowledgeblog.com/index.php/the-pinocchio-protocol/from-theory-to-practice)
    - [**One line, one operation**](https://www.zeroknowledgeblog.com/index.php/the-pinocchio-protocol/one-line-one-operation)

### 1.2 Rank-1 Constraint System (R1CS)

Once we have this arithmetic circuit in the form as explained above, we can proceed to convert it into a representation of matrices and vertices known as the Rank-1 Constraint System (R1CS).

To understand how it works, read the following resources:

- [**R1CS: A Day in the Life of a few Equations**](https://learn.0xparc.org/materials/circom/additional-learning-resources/r1cs%20explainer/) - This 0xParc article was mentioned above, ensure you read this in full as it is a very friendly introduction to R1CS.
- [**R1CS by Maurizio Binello**](https://www.zeroknowledgeblog.com/index.php/the-pinocchio-protocol/r1cs) - This is a continuation of Maurizio Binello's series of blog posts mentioned above. You might want to revisit the other pages in this series.

### 1.3 Quadratic Arithmetic Program (QAP)

R1CS helped to reduce our computation into a set of matrices and vertices. But now, we need to convert it into a format called QAP.

For understanding this, we turn to the following resources:

- [**Explaining SNARKs Part V: From Computations to Polynomials**](https://electriccoin.co/blog/snark-explain5/) - A continuation of the Electric Coin blog series.
- [**QAP by Maurizio Binello**](https://www.zeroknowledgeblog.com/index.php/the-pinocchio-protocol/qap) - A continuation of Maurizio Binello's blog series.
- [**Quadratic Arithmetic Programs: from Zero to Hero**](https://medium.com/@VitalikButerin/quadratic-arithmetic-programs-from-zero-to-hero-f6d558cea649) - Vitalik Buterin's article on getting to a QAP representation. Feel free to start from the "R1CS to QAP" section.

## 2. Proof Systems

Two common proof systems you should know about are Groth16 and PLONK. They are significant improvements over the Pinocchio proving system. Here is a very brief [overview](https://docs.gnark.consensys.net/Concepts/schemes_curves) of the two and their tradeoffs.

### 2.1 Groth16

The efficiency of Groth16 is very hard to beat, and as such it has become a de-facto standard in many blockchain technologies that require an efficient proof system. However, the requirement of a circuit-specific trusted setup is a significant downside for some use-cases.

We may skip the details of Groth16 but just keep in mind that the advantage is its small proof size. The disadvantage is that it requires a circuit specific trusted setup. These days, we have much more advanced proof systems that improve upon these trade-offs. Nevertheless, Groth16 continues to be used in a lot of existing projects.

#### Optional Reading

Here are a couple articles to understand how Groth16 works:

- [Groth16 by Remco Bloemen](https://xn--2-umb.com/22/groth16/) - A very light article that covers the full life cycle of the Groth16 proving system.
- [Groth16 by Maurizio Binello](http://www.zeroknowledgeblog.com/index.php/groth16) - A continuation of the blog series above that you should be well acquainted with.

### 2.2 PLONK

PLONK has fast become one of the favourite proof systems because of its "universal and updateable" trusted setup, eliminating the need to have a new trusted setup for every circuit.

Here are a couple resources to understand how PLONK works:

- [Understanding PLONK by Vitalik Buterin](https://vitalik.eth.limo/general/2019/09/22/plonk.html)
- [How does PLONK work? by David Wong](https://cryptologie.net/article/529/how-does-plonk-work-part-1-whats-plonk/)
- [How PLONK Works: Part 1 by CoinGeek](https://coingeek.com/how-plonk-works-part-1/)
- [How PLONK Works: Part 2 by CoinGeek](https://coingeek.com/how-plonk-works-part-2/)

## 3. Additional Study

In the above, we have drawn very heavily from blog posts written by Vitalik Buterin, Electric Coin, and Maurizio Binello. However, these are only some of the many pathways towards understanding zkSNARK construction.

Since it is always helpful to take a look at the same problem from different angles, we recommend you visit the following resources:

- [**Why and How zk-SNARK Works**](https://medium.com/@imolfar/why-and-how-zk-snark-works-1-introduction-the-medium-of-a-proof-d946e931160) (highly recommended) - Originally [**a paper**](https://arxiv.org/abs/1906.07221) by Maksym Petkus, it dives into the specifics of how a zkSNARK is constructed, it has been converted to a series of blog posts for easy consumption.
- [**ZK Whiteboard Sessions**](https://zkhack.dev/whiteboard/) - There are three videos by Dan Boneh (he's the B in BLS Signatures) providing a very compelling introduction to zkSNARKs. I highly recommend at least watching ***What is a SNARK?*** and ***Building a SNARK (Part I)***.
- [**The MoonMath Manual for zkSNARKs**](https://leastauthority.com/community-matters/moonmath-manual/) - This is a free online textbook PDF that explains many of the necessary concepts. It is an excellent reference guide whenever you need to dive into specific topics.

### 3.1 Homomorphic Hiding and Blind Evaluation

Let's start by looking into the concepts of homomorphic hiding and blind evaluation. Although not directly related to zkSNARKs, it is one of the main ingredients or concepts that make zkSNARKs possible.

This blog series from Electric Coin is a good start:

- [Explaining SNARKs Part I: Homomorphic Hidings by Electric Coin Co.](https://electriccoin.co/blog/snark-explain/)
- [Explaining SNARKs Part II: Blind Evaluation of Polynomials](https://electriccoin.co/blog/snark-explain2/)

ASecuritySite.com also has some helpful interactive examples that go along with these two blog posts:

- [zkSNARK (Homomorphic Hiding)](https://asecuritysite.com/zero/zksnark01)
- [zkSNARK (Blind Evaluation Problem)](https://asecuritysite.com/zero/zksnark02)

### 3.2 The Pinocchio Protocol

The Pinocchio Protocol was first described in a paper in 2013, [**Pinocchio: Nearly Practical Verifiable Computation**](https://eprint.iacr.org/2013/279). As the name suggests, it was a big step towards the practical construction of zkSNARKs that we know today. It builds upon the QAP representations we described above and it is also here where elliptic curve pairings become relevant again.

Admittedly, the details from here get even more technical than before. So it is important to start with a focused article before moving onwards.

Therefore, read Vitalik's article, [**zk-SNARKs: Under the Hood**](https://medium.com/@VitalikButerin/zk-snarks-under-the-hood-b33151a013f6). This article was designed to follow his two other blog posts (on [QAP](https://medium.com/@VitalikButerin/quadratic-arithmetic-programs-from-zero-to-hero-f6d558cea649) and [Pairings](https://medium.com/@VitalikButerin/exploring-elliptic-curve-pairings-c73c1864e627)), so feel free to revisit those articles if you need to.

Once you have done this, check out Maurizio Binello's page on the [**history of the Pinocchio paper**](https://www.zeroknowledgeblog.com/index.php/the-pinocchio-protocol). You can then jump back into the series by reading the page on [Hiding](https://www.zeroknowledgeblog.com/index.php/the-pinocchio-protocol/hiding) (which follows after the page on QAP) and continue by clicking "Next" at the bottom of each page.

Finally, Part VI of the Electric Coin series provides a brief sketch of the protocol. While Part VII ties it all up with elliptic curve pairing concepts. Both of these are worth a read:

- [**Explaining SNARKs Part VI: The Pinocchio Protocol**](https://electriccoin.co/blog/snark-explain6/)
- [**Explaining SNARKs Part VII: Pairings of Elliptic Curves**](https://electriccoin.co/blog/snark-explain7/)

# 💪 Exercises

Answer the following questions (in as much detail as you like).

## Homomorphic Hiding

1. Explain homomorphic hiding in your own words.

## Arithmetic Circuits

1. What is the primary purpose of converting a problem into an arithmetic circuit?
2. What are the main components of an arithmetic circuit?

## Rank-1 Constraint System (R1CS)

1. Describe the Rank-1 Constraint System (R1CS) in your own words.
2. Why is R1CS essential in the zkSNARK construction pipeline?

## Quadratic Arithmetic Program (QAP)

1. What is the primary goal of converting R1CS into a QAP?
2. How does QAP aid in the zkSNARK proof generation process?
3. Why are polynomials central to the QAP representation?

## The Pinocchio Protocol

1. Why is the Pinocchio Protocol considered a significant step towards practical zkSNARK construction?
2. How does the Pinocchio Protocol utilize QAP representations?
3. What role do elliptic curve pairings play in the Pinocchio Protocol?

## Groth16

1. What makes Groth16 a popular choice for zkSNARK constructions in blockchain technologies?
2. Describe the main advantage and disadvantage of the Groth16 proof system.
3. How does Groth16 differ from the original Pinocchio Protocol?

## PLONK

1. What are the advantages of PLONK over Groth16? What are the disadvantages?
2. How does PLONK eliminate the need for a new trusted setup for every circuit?
