# Module 5 - PSE Protocols

Congratulations on completing the first four modules. From this point onwards, we will focus more on practical application and actual coding rather than theory. Therefore, in this module, we will be covering a few of the protocols developed within the Privacy and Scaling Explorations (PSE) team.

Rather than delving into the intricate details of how each project works, we will present a brief overview of each one, followed by links to the relevant documentation and resources. This approach will equip you with the context to independently study and navigate through the documentation.

## Introductory Video

A previous PSE grantee (Jack Gilcrest) created a video for the recent EthGlobal Paris hackathon to explain some of the projects mentioned below. This is a great start and it is recommended that you view this video first.

👉 [**Semaphore, Unirep, RLN Explained [22:33]**](https://drive.google.com/file/d/1JQKDRhGsgNDfRrzy86n6wSCc1Xo1-F1F/view)

Please be aware that a wealth of videos on each of the protocols, such as Semaphore or UniRep, can be found online. A quick search on YouTube using these terms is likely to yield several results, offering additional content for those interested in delving deeper into these subjects.

## Semaphore

**Github**: https://github.com/semaphore-protocol
**Website**: https://semaphore.appliedzkp.org/

Semaphore allows users to prove their membership in a group and transmit anonymous data, such as votes or feedback, without revealing their identities.

This is a very general concept that can be applied to many use-cases. In fact, many of the projects discussed below are built on top of the Semaphore protocol.

This video is a good overview of the Semaphore protocol:

👉 [**Anonymous Signalling on Ethereum by Cedoor | Devcon Bogotá [15:30]**](https://www.youtube.com/watch?v=dxAfL91Sbw4&ab_channel=EthereumFoundation)

## UniRep

**Github**: https://github.com/Unirep
**Website**: https://developer.unirep.io/

Building on top of Semaphore, UniRep extends the concept of anonymous groups by allowing small amounts of data to be associated with anonymous users. Where Semaphore allows one to prove they are part of a group, UniRep allows one to prove *something* about the anonymous user.

One simple example of this is a system where Twitter can attest to a user's number of followers. The user can then prove to others that they have at least a certain number of followers while remaining anonymous.

This video is a good overview of the UniRep protocol:

👉 [**Chance Hudson - Robust Anonymous UX with the UniRep Protocol [17:01]**](https://www.youtube.com/watch?v=hGQlgS9s6P8)


## Rate-Limiting Nullifier (RLN)

**Github**: https://github.com/Rate-Limiting-Nullifier
**Website**: https://rate-limiting-nullifier.github.io/rln-docs/

An anonymous environment can bring new challenges to group coordination. One such problem is spam-protection. RLN takes a novel cryptographic approach in which those who exceed the rate limit, can be penalized either by withdrawing the offender's stake or revealing their secrets.

This video is a good overview of the RLN protocol: 

👉 **[Rate Limiting Nullifier by AtHeartEngineer | Devcon Bogotá [7:03]](https://www.youtube.com/watch?v=vrNiPBfbLw0)**

## Newer Projects

The following projects are a bit newer, and their documentation and APIs might not be stable or very complete yet. However, these are some of the projects that the PSE team is excited about bringing more attention to in the near future. As such, we have included them in this module for your benefit.

**NOTE**: The exercise section below does not necessarily apply to the following projects. However, you are free to include them if you have extra time to do so.

## Bandada

**Github**: https://github.com/privacy-scaling-explorations/bandada
**Website**: https://bandada.pse.dev/

Bandada is a backend and frontend stack to assist in managing anonymous Semaphore groups. It is aimed at developers who want to build privacy-based applications and integrate anonymity sets, as well as anyone that wants to create and manage anonymous groups. 

It enables anonymous signaling, such as voting, messaging, login, or endorsing, in various use cases like private organizations, GitHub repository contributors, and groups of wallets holding a specific NFT, for example.

## CryptKeeper

Github: https://github.com/CryptKeeperZK

CryptKeeper is a browser extension that generates Semaphore and RLN proofs for websites, providing a secure and portable solution for managing anonymous identity secrets across different applications.

It simplifies the integration of zero-knowledge (ZK) identities and proofs into applications, allowing developers to focus on building the front-end and logic of their applications.

By handling complex aspects of cryptography, circuits, caching, and storage, CryptKeeper enables users to interact with decentralized applications (dapps) without revealing their private identity secrets. It is aimed at building secure community standards for the growing ZK ecosystem.

## TLSNotary

**Github**: https://github.com/tlsnotary/tlsn
**Website**: https://tlsnotary.org/

TLSNotary allows you to export data from any web application and prove facts about it without compromising on privacy. With TLSNotary, you can create cryptographic proofs of authenticity for any data on the web, even your own private data.

One may assume that TLSNotary requires a “man-in-the-middle” setup where the Notary snoops on the connection with the webserver. Fortunately, this is not true! Data is kept private even from the Notary.

# 💪 Exercises

## Written Questions

### Specific Questions

Here are also a few specific questions to answer:

1. What does a nullifier do and why is it important?
2. What does a trapdoor do and why is it important?
3. Can you compare and contrast Semaphore, UniRep, and RLN?
4. What key cryptographic concepts do you see being used in these projects?

### General Questions

For each of the projects (Semaphore, UniRep, RLN) listed above, answer the following:

1. **Explain the Motivation and Functionality in Detail**: What drove the creation of this project, and what does it primarily do? Explain its core functionality and goals in your own words.
2. **Provide Example Use-Cases**: Identify and describe some practical use-cases that can be built with this project. How can it be applied in real-world scenarios? Can you explain these use-cases to someone without a technical background?
4. **Hurdles to Overcome**: What are some downsides to the project? Are there requirements that might make adoption difficult? Reflect on potential improvements to the project.
5. **Circuit Analysis (Optional)**: Where applicable, take a look at the circuits used within the project. Although you may not yet be familiar with the syntax of Circom, try your best to explain what is happening within them.
6. **Hands-On Implementation (Optional)**: If time permits, create a simple prototype or demo using the project. Provide a brief explanation of what you built and how it illustrates a feature of the project.

Items 4 and 5 might be quite challenging, so do not feel obligated to complete these. However, completing them will give you a more refined understanding of how these protocols work.

**Optional** - Answer the same questions above (where applicable) for the projects mentioned under "Newer Projects".