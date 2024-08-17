# Week 5 - Frontier Technologies

In this final week of the curriculum, we are going to take a more self-exploratory approach to some exciting topics and tools at the forefront of programmable cryptography. This will give you the flexibility to continue exploring PLONK if you need the extra time, but also new areas of exploration which may interest you.

First, we will dive into some basics about MPC/FHE. Then we will look at some interesting tools and primitives like TLSNotary and ZKEmail. Keep in mind that the topics in this module continue to evolve at a rapid pace. We will only be able to touch on some basic concepts and the rest will be for you to explore.

## MPC/FHE

Zero-knowledge proofs (ZKPs), Multi-Party Computation (MPC), and Fully Homomorphic Encryption (FHE) are all areas of research that have significant overlap with each other. So far, you have mostly focused on ZKPs, but learning about MPC/FHE will allow you to see things from a new perspective.

### Multi-Party Computation (MPC)

[Secure Multi-Party Computation](https://en.wikipedia.org/wiki/Secure_multi-party_computation) or MPC for short, is a protocol that allows multiple entities to jointly compute a function without revealing their individual inputs.

The classic example of MPC is the [Yao's Millionaire Problem](https://en.wikipedia.org/wiki/Yao%27s_Millionaires%27_problem). This is a thought experiment in which two millionaires are interested in knowing which of them is richer without revealing their actual wealth.

MPC is also used to generate the secret value and the Common Reference String (CRS) for a trusted setup in a distributed manner, where multiple parties collaborate to generate the parameters without any single party having access to the entire secret value.

Start here with a blog post from PSE: [Secure Multi-Party Computation](https://mirror.xyz/privacy-scaling-explorations.eth/v_KNOV_NwQwKV0tb81uBS4m-rbs-qJGvCx7WvwP4sDg)

When you are done, feel free to browse these (optional) additional resources at your own pace:

- [Introduction to Multi-Party Computation (MPC or SMPC) [5:43]](https://www.youtube.com/watch?v=90jcXCHsBF0)
- [Sharing Knowledge without Sharing Data by Azer Bestavros [32:08]](https://www.youtube.com/watch?v=P2MmO458xu4)
- [Accessible and Scalable: Secure Multi-Party Computation](https://multiparty.org/)
- [Intro to MPC (Javascript tutorial and examples)](https://github.com/multiparty/jiff/blob/master/tutorials/0-intro-to-mpc.md)

### Fully Homomorphic Encryption (FHE)

Another fascinating and growing area of research is the concept of [Fully Homomorphic Encryption (FHE)](https://en.wikipedia.org/wiki/Homomorphic_encryption#Fully_homomorphic_encryption). Technically, FHE as a concept is a subset of homomorphic hidings (the Wikipedia article linked above reflects this).

The properties of FHE are quite interesting, even though much work still needs to be done to make it viable for production. To get started learning about FHE, read the two-part blog post below to get a general lay of the land:

- [Zero to Start: Applied Fully Homomorphic Encryption (FHE) Part 1](https://mirror.xyz/privacy-scaling-explorations.eth/D8UHFW1t48x2liWb5wuP6LDdCRbgUH_8vOFvA0tNDJA)
- [Zero to Start: Applied Fully Homomorphic Encryption (FHE) Part 2](https://mirror.xyz/privacy-scaling-explorations.eth/wQZqa9acMdGS7LTXmKX-fR05VHfkgFf9Wrjso7XxDzs)

After you are done reading that, please go through the following:

#### Tutorials and Examples
- **[Zama FHE Tutorials](https://github.com/zama-ai/awesome-zama?tab=readme-ov-file#tutorials)**: A list of Fully Homomorphic Encryption (FHE) resources created by Zama.
- **[Homomorphic Encryption Example](https://github.com/homenc/HElib/tree/master/examples)**: Example codes using the HElib library. HElib is an open-source software library that implements homomorphic encryption.
- **[Microsoft SEAL Examples](https://github.com/Microsoft/SEAL/tree/main/native/examples)**: Example codes and tutorials for Microsoft SEAL. Microsoft SEAL is an easy-to-use and powerful homomorphic encryption library.

#### Key Papers and Articles
- **[Gentry's Original Paper on FHE](https://eprint.iacr.org/2009/616.pdf)**: The foundational paper by Craig Gentry that introduced the first practical FHE scheme.
- **[Homomorphic Encryption Standardization](https://homomorphicencryption.org/standard)**: Ongoing efforts and papers aimed at standardizing homomorphic encryption schemes.
- **[Jeremy Kun's Overview on FHE](https://www.jeremykun.com/2024/05/04/fhe-overview/)**: A detailed blog post that provides an excellent overview of FHE concepts and advancements.

#### Current Research
- **[FHE.org Community](https://fhe.org)**: A hub for researchers and developers working on advancing FHE and other secure computation techniques.
- **[TII Survey on FHE](https://eprint.iacr.org/2022/1602.pdf)**: A comprehensive survey paper that provides an in-depth overview of the current state of FHE research.

## TLSNotary

[TLSNotary](https://tlsnotary.org/) is a protocol that allows you to prove to a third party that you have received certain data from a web server, without allowing the third party to see the data itself. This is particularly useful for verifying the authenticity of the data you’ve received, such as bank statements or signed documents, without exposing sensitive information.
It enables a client to prove data provenance—that data was honestly obtained from a specific server—while preserving privacy through Multi-Party Computation (MPC), without revealing the actual content to third parties or relying on a single trusted intermediary.

For a brief overview, watch this video: [Verify Private Data with TLSNotary Plugins](https://www.youtube.com/watch?v=SDjmjiqmUFw)

We also encourage you to take a look at the following:

- [Explanatory Blog Post](https://pluto.xyz/blog/how-tlsnotary-works)
- [GitHub Organization](https://github.com/tlsnotary)
- [Main Website](https://tlsnotary.org/)

## ZKEmail

The [ZKEmail](https://github.com/zkemail) project is a fascinating application of Zero-Knowledge Proofs with traditional protocols (like emails and DKIM). A simple intersection of new and old technologies allow for fascinating new use-cases like treating emails as a wallet or even a peer-to-peer network of transfer.

For a brief introduction, have a look at this short video: [Zuconnect 2023 ZK Day: ZK Email
 (11:40)](https://www.youtube.com/watch?v=3jCKdxQ9Pfw)

Have a look at the following:

- [Technical explanatory blog post](https://blog.aayushg.com/zkemail/)
- [Github Organization](https://github.com/zkemail)
- [Main Website](https://prove.email/)