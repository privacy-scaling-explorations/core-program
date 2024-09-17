# PSE Core Program 2024: Contributions

![Core Program](https://img.shields.io/badge/Core-Program-blue)
![PSE Projects](https://img.shields.io/badge/PSE-Projects-orange)

## Contributions During the PSE Core Program

Throughout the PSE Core Program, several talented hackers and teams came together to push the boundaries of cryptographic solutions and blockchain innovation. Their contributions spanned various areas and technologies. These projects not only showcased the technical expertise of the participants but also demonstrate the collaborative spirit essential to solving real-world challenges in decentralized ecosystems.

## **PSE Core Program 2024 Projects**

This is a complete list of contributions made by the program participants.

| Project Name                                                                              | Project Description                                                                                                                                                                                                                                      |
| :---------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [AnonAr](#anonar)                                                                         | AnonAr is a zero-knowledge protocol that allows DNI's holders to prove their identity in a privacy preserving way.                                                                                                                                       |
| [ZK-Kit](#zk-kit-contributions)                                                           | In the context of the Lean-IMT package of the library - Implemented a method in the Lean-IMT Merkle tree package that reduces the worst-case time complexity from O(n.logn) to O(n) for bulk leaf updates by ensuring each node is updated at most once. |
| [IMT Benchmarks](#imt-benchmarks)                                                         | Comparison of different implementation of Incremental Merkle Tree in a server and a browser.                                                                                                                                                             |
| [TLSN - Duolingo](#tlsn-duolingo)                                                         | Project to generate a proof using TLSN that you have a given streak on duolingo, hiding your user_id and email address.                                                                                                                                  |
| [Anon x MACI](#anon-x-maci)                                                               | Proof of Reserve for Exchanges (Summa)                                                                                                                                                                                                                   |
| [Semaphore (issue 332)](#semaphore-issue)                                                 | Build a Semaphore step-by-step tutorial showing how to develop a DApp using the extensions contracts package.                                                                                                                                            |
| [ZK-Kit (issue 230)](#zk-kit-issue)                                                       | Restrict types of message in eddsa-poseidon's signMessage                                                                                                                                                                                                |
| [Summa Solvency](#summa-solvency)                                                         | Contributed with a PR to the Summa Solvency project.                                                                                                                                                                                                     |
| [MPC Adventures](#mpc-adventures)                                                         | Tutorials and explanations of vanilla implementations of MPC primitives                                                                                                                                                                                  |
| [Jubmoji Quest - Proof of Location Extension](#jubmoji-quest-proof-of-location-extension) | Extended proof of location to Jubmoji via QR                                                                                                                                                                                                             |
| [Zk Multiverse](#zk-multiverse)                                                           | ZK Multiverse guides users through interactive challenges to learn zero-knowledge proofs, focusing on zk circuit development with Circom or Noir, while covering essential cryptography and math concepts.                                               |
| [KZG implementation](#kzg-implementation)                                                 | Implementation of KZG for non-membership and counting.                                                                                                                                                                                                   |
| [Sempahore UI contribution](#semaphore-ui-contribution)                                   | Update cli monorepo ethers and subgraph web app UI                                                                                                                                                                                                       |
| [ZKP2P landing bug fix](#zkp2p-landing-bug-fix)                                           | Fix docs URL in ZKP2P landing page                                                                                                                                                                                                                       |
| [Zk-mercadopago](#zk-mercadopago)                                                         | Zk Mercadopago                                                                                                                                                                                                                                           |

---

### AnonAr

**Contributors:**

- Lorenzo Hardoy - https://x.com/lorenzz29

**Project Description:**
AnonAr is a zero-knowledge protocol that allows DNI's holders to prove their identity in a privacy preserving way.

**Technical Stack:**

- Circom

**Project Goals:**
To build a MVP allowing users to generate a valid proof.

**GitHub Link:**
[https://github.com/Lorenz29/anon-ar/](https://github.com/Lorenz29/anon-ar/)

---

### ZK-Kit contributions

**Contributors:**

- Chino Cribioli - @chino_cribioli

**Project Description:**

- Contribution 1:
  In the context of the Lean-IMT package of the library, which is an implementation of a merkle tree in which you can add, erase and modify leaves dinamically, I implemented a method that lets the user modify several leaves at the same time. This improved the worst-case time complexity from O(n.logn) to O(n) in the case where the number of leaves to update is similar to the size of the tree. This is done by updating every node of the tree at most once during the whole execution of the method.  
  A full analysis of the complexity is included in the contribution.

- Contribution 2:
  I detected a vulnerability in the implementation of the Baby JubJub curve in the EdDSA package of the library. This is a type of 'timing attack', which consists of extracting information from the time it takes for the processor to perform a certain process.  
  In this case, based on the time it takes to complete a 'mulPointScalar' call, an attacker could infer the number of 1's in the binary expression of the secret number passed as input since the method is implemented with the classic 'square-and-multiply' algorithm.  
   A deeper description of the problem can be found in the issue I created [https://github.com/privacy-scaling-explorations/zk-kit/issues/324](https://github.com/privacy-scaling-explorations/zk-kit/issues/324)

**Technical Stack:**

- Typescript.
- Algorithmic analysis

**Project Goals:**

- Contribution 1:
  Optimize the performance of the package when the number of updates is high.

- Contribution 2:
  Fix the issue to the best of our knowledge. I proposed an implementation of the 'Montgomery Ladder' algorithm, which I learned is a technique used to mitigate this kind of timing attacks.

**GitHub Link:**

- Contribution 1:
  [https://github.com/privacy-scaling-explorations/zk-kit/pull/314](https://github.com/privacy-scaling-explorations/zk-kit/pull/314)

- Contribution 2:
  [https://github.com/privacy-scaling-explorations/zk-kit/pull/325](https://github.com/privacy-scaling-explorations/zk-kit/pull/325)

---

### IMT Benchmarks

TLSN - Duolingo
**Contributors:**

- Sebastián Giraudo - @sebagiraudo

**Project Description:**
Comparison of different implementation of Incremental Merkle Tree in a server and a browser. The Rust implementation was translated to wasm and the js implementation was used directly.

**Technical Stack:**

- Rust, TS, wasm converter.

**Project Goals:**
Obtain benchmarks to compare the different implementations.

**GitHub Link:**
[https://github.com/sebagiraudo/imt-benchmarks](https://github.com/sebagiraudo/imt-benchmarks)

---

### TLSN-Duolingo

**Contributors:**

- Sebastián Giraudo - @sebagiraudo

**Project Description:**
Project to generate a proof using TLSN that you have a given streak on duolingo, hiding your user_id and email address.

**Technical Stack:**

- TLSN, Rust

**Project Goals:**
Proof of concept to learn how to use TLSN, hide data in request and reply.

**GitHub Link:**
[https://github.com/sebagiraudo/tlsn-duolingo](https://github.com/sebagiraudo/tlsn-duolingo)

---

### Anon X MACI

**Contributors:**

- @protocolwhisper
- @protocolllo

**Project Description:**
Proof of Reserve for Exchanges (Summa)

**Technical Stack:**

- Rust

**Project Goals:**
Be able to create a proof of liquidity without showing all the balance

**GitHub Link:**
[https://github.com/summa-dev/summa-solvency/pull/301](https://github.com/summa-dev/summa-solvency/pull/301)

---

### Semaphore issue

**Contributors:**

- Fernando Ledesma - https://t.me/f3rledesma

**Project Description:**
Build a Semaphore step-by-step tutorial showing how to develop a DApp using the extensions contracts package. In my case, I have to use `SemaphoreWhistleblowing.sol` contract

**Technical Stack:**

- Semaphore, Typescript, Nextjs, Wagmi, rainbowkit

**Project Goals:**
Deploy the DApp and publish an article showing the steps

**GitHub Link:**
[https://github.com/f3r10/semaphore-whistleblowing-example-app](https://github.com/f3r10/semaphore-whistleblowing-example-app)

---

### ZK-Kit issue

**Contributors:**

- Fernando Ledesma - https://t.me/f3rledesma

**Project Description:**
Restrict types of message in eddsa-poseidon's signMessage

**Technical Stack:**

- Typescript.

**Project Goals:**
Update the type of the parameter so it will more clear for developers which type should be used. If the parameter is longer that 32 bytes should not be accepted.

**GitHub Link:**
[https://github.com/privacy-scaling-explorations/zk-kit/pull/318](https://github.com/privacy-scaling-explorations/zk-kit/pull/318)

---

### Summa Solvency

**Contributors:**

- Francisco Bezzecchi - @bezze

**Project Description:**
I just contributed with a PR to the Summa Solvency project. The project itself is a system for exchanges to proof solvency to their users without revealing balances.

**Technical Stack:**

- Rust, Solidity, Halo2

**Project Goals:**
Contribute towards enhancing transparency in the whole Summa flow. In particular provide a way for the users to easily check the verification key used in the upstream ethereum smart contracts that verify proofs.

**GitHub Link:**
[https://github.com/summa-dev/halo2-solidity-verifier/pull/2](https://github.com/summa-dev/halo2-solidity-verifier/pull/2)

---

### MPC Adventures

**Contributors:**

- Caro Lang - @carolang

**Project Description:**
Tutorials and explanations of vanilla implementations of MPC primitives: Yao's Garbled Circuits, Oblivious transfer in particular, and Shamir Secret Sharing.

**Technical Stack:**

- Jupyter Notebook with usage of pycryptodome and sagemath.

**Project Goals:**
To offer a source of learning for the implemented primitives based in working code in Python. This offers a bridge between the more mathematical sources (like the corresponding papers) and the community, but at the same time offering concrete code to play with online and gain more understanding. The exercises are offered along with solved versions of the notebooks.

For the future, I want to add automated tests for the code snippets, and to modularize the code a bit (for example the implementation for OT is copied and pasted inside the Garbled Tables one and this takes away the attention from the important part). Also I want to add progressively more versions with some optimizations.

**GitHub Link:**
[https://github.com/carolang/mpc-adventures](https://github.com/carolang/mpc-adventures)

---

### Jubmoji Quest Proof of Location Extension

**Contributors:**

- Joaquin Barrientos - @jbmkahdeksan
- Steven Cordero - @stevencartavia
- Erick Vásquez - @evgongora
- Humberto Trejos - @HumbertoTM10
- Ricardo Bonilla - @richbm10
- Roberto Solano - @robertosolano

**Project Description:**
Extended proof of location to Jubmoji via QR

**Technical Stack:**

- Circom, SnarkJS, NextJS

**Project Goals:**
Implemented Proof of Location verification via QR codes to Jubmoji

**GitHub Link:**
[https://github.com/richbm10/jubmoji.quest](https://github.com/richbm10/jubmoji.quest)

---

### ZK Multiverse

**Contributors:**

- Alfredo - https://x.com/brolag
- Mai https://x.com/MaiCVCR

**Project Description:**
ZK Multiverse helps users choose the right path in learning zero-knowledge proofs (ZK). Through interactive challenges, it teaches how to build zk circuits with Circom or Noir, while covering cryptography and math fundamentals. The guided structure ensures learners stay on track, focusing on practical skills needed for ZK development.

**Technical Stack:**

- Circom, Noir, Scaffold Eth (Next.js, TailwindCSS, TypeScript)

**Project Goals:**
The Problem We Are Solving:  
Too Much Theory, Not Enough Practice: Cryptography is often surrounded by complex theories with few practical examples. ZK Multiverse bridges this gap by offering practical, real-world scenarios where you can apply what you’ve learned.

Information Overload: With so many cryptographic concepts and resources available, it’s easy for developers to get sidetracked or overwhelmed. ZK Multiverse guides you through a curated learning path, ensuring you stay focused and gain the essential skills needed to excel in zero-knowledge proof development.

**GitHub Link:**
[https://github.com/brolag/zk-multiverse](https://github.com/brolag/zk-multiverse)

---

### KZG implementation

**Contributors:**

- Lucas Dario Cardacci

**Project Description:**
Motivation  
Actually, a type of vector commitment scheme uses hash functions to prove the belonging of an element to a vector, counting the number of occurrences and confirming the non-membership with Merkle trees. On my final project for my bachelor's degree in mathematics I present a vector commitment scheme based on KZG, that allows do the same.

Project description  
Implement these schemes non-membership and counting bases on KZG using rust as a principal language of programming.

**Technical Stack:**

- Rust

**Project Goals:**
The end goal of the project is to have a functional Rust library that can be used to prove the membership or non-membership of elements in a vector, as well as count occurrences of elements, using the new schemes based on KZG. The project will be considered successful when the library is thoroughly tested, well-documented, and can be easily integrated into other cryptographic systems.

**GitHub Link:**
[https://github.com/lcarda/Curucucha](https://github.com/lcarda/Curucucha)

---

### Semaphore UI contribution

**Contributors:**

- yagopajarino - @0xyago

**Project Description:**
Update cli monorepo ethers and subgraph web app UI

**Technical Stack:**

- React, HTML, CSS

**Project Goals:**
Update semaphore demo frontend

**GitHub Link:**
[https://github.com/semaphore-protocol/semaphore/pull/841](https://github.com/semaphore-protocol/semaphore/pull/841)

---

### ZKP2P landing bug fix

**Contributors:**

- yagopajarino - @0xyago

**Project Description:**
Fix docs URL in ZKP2P landing page

**Technical Stack:**

- Frontend

**Project Goals:**
Fix docs URL in ZKP2P landing page

**GitHub Link:**
[https://github.com/zkp2p/zk-p2p/pull/398](https://github.com/zkp2p/zk-p2p/pull/398)

---

### Zk-mercadopago

**Contributors:**

- yagopajarino - @0xyago

**Project Description:**
Zk-mercadopago

**Technical Stack:**

- Circom

**Project Goals:**
Create a circom circuit that proves a transaction over mercadopago payment system

**GitHub Link:**
[https://github.com/yagopajarino/zk-email-minimal](https://github.com/yagopajarino/zk-email-minimal)
