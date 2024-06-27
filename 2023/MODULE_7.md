# Module 7 - Circuit Writing Crash Course

Welcome to Module 7 of the program! From here, things become more self-guided, leading into the contribution stage of our program. This means fewer specific instructions and more freedom to explore areas that interest you.

In the next two weeks, we aim to help you get comfortable with reading and writing Circom circuits. The first week provides a list of learning materials and challenges (see below), while the second week invites you to create your own circuit ideas.

It’s normal to have different levels of comfort with this material, and that’s okay. Remember, this is just one step in a lifelong learning process.

Open-source community members often work to improve things just for the sake of improvement. That’s a value we hope to instill in you as well.

So the most crucial advice is to **go at your own pace and enjoy the process 🤗**. Going slow to understand thoroughly is better than rushing and getting frustrated.

Without further ado, let’s start with a quick overview (including an explanation of what Circom, Halo2, and Noir).

**Start here:**

👉 **[A beginner’s intro to coding zero-knowledge proofs](https://dev.to/spalladino/a-beginners-intro-to-coding-zero-knowledge-proofs-c56)**

Enjoy the journey!

## A note about **Halo2**

Some of you might choose to focus on Halo2 for this portion of the program (instead of Circom). This is great because Halo2 is one of the up-and-coming ecosystems for circuit development.

However, since it is quite new, there are far fewer resources for learning how to use it. You will not only require a good knowledge of Rust (the programming language), you will also need to be comfortable looking through documentation and reaching out to others for help.

All of the Circom challenges below can be attempted via Halo2, but you will be required to figure out how to adapt them for Halo2.

To get you started, here are some of the resources we recommend you go through:

**Tutorial and Lectures**

1. Read Consensys Diligence’s **[introductory article on Halo2](https://consensys.io/diligence/blog/2023/07/endeavors-into-the-zero-knowledge-halo2-proving-system/)**.
2. Read Axiom’s **[Getting Started with Halo2](https://docs.axiom.xyz/zero-knowledge-proofs/getting-started-with-halo2)**.
3. Read Axiom’s **[Halo2 Cheatsheet](https://hackmd.io/@axiom/HyoXzD7Zh)**.
4. Work through 0xParc’s **[Halo2 lecture series](https://learn.0xparc.org/materials/halo2/learning-group-1/introduction)**.
5. (Optional) [An encyclopedia of halo2](https://halo2.club/)

**Reference Material**

1. Use the **[Halo2 Book](https://zcash.github.io/halo2/)** for reference. This **[Simple Example](https://zcash.github.io/halo2/user/simple-example.html)** can be a good start.
2. Reference **[this presentation](https://docs.google.com/presentation/d/1UpMo2Ze5iwzpwICPoKkeT04-xGFRp7ZzVPhgnidr-vs/edit#slide=id.p)** for details on PLONKish arithmetization and Halo2.

# **Module 7 - Week 1**

For this week, we have three major modules for you to work through. Notice that the modules are not denoted by date. You should work through them at your own pace, and if there are items here that you would like to skip, feel free to do so as well.

## **1. Review and Foundations**

### **1.1 Learn**

- Review the concepts in Module 6 of the previous stage.
- As a reminder, read through this **[introductory article](https://dev.to/tonyolendo/the-complete-full-stack-guide-to-getting-started-with-zero-knowledge-proofs-using-circom-and-zk-snarks-part-2-58o)**.
- Read through the official **[Circom Language](https://docs.circom.io/circom-language/signals/)** documentation.
- Read and understand the official **[Basic Circuits](https://docs.circom.io/more-circuits/more-basic-circuits/)**.
- Work through the **[first workshop](https://learn.0xparc.org/materials/circom/learning-group-1/circom-1)** from 0xParc’s Circom Workshop series.
- Read and understand the **[Sudoku Solution Proof Circuit](https://github.com/zku-cohort-3/zkPuzzles/blob/fa89bf49ae4a8ffe57a05b3df2137ac65d01abe2/circuits/sudoku.circom)** featured in the previous module.

### **1.2 Challenges**

Consider the basic arithmetic and hash functions needed for the following challenges.

- **Challenge 1**: Write a Circuit to Prove You Know an Input to a Hash
- **Challenge 2**: Write a Circuit to Prove You Know the Private Key to a Public Key

## **2. Building Basic Circuits**

### **2.1 Learn**

- Work through the **[second workshop](https://learn.0xparc.org/materials/circom/learning-group-1/circom-2)** from 0xParc’s Circom Workshop series.
- Work through the **[Week 2](https://zku.gnomio.com/mod/assign/view.php?id=119)** and **[Week 3](https://zku.gnomio.com/mod/assign/view.php?id=121)** assignments from the ZKU course.
  - Click the “Access as a guest” button to read the content.

### **2.2 Challenges**

- **Challenge 1**: Prove Membership of an Element in a Merkle Tree
- **Challenge 2**: Prove You Are Part of a Group
  - _Note_: Think about cryptographic methods for proving membership in a particular set or group.

## **3. How Token Mixers Work**

### **3.1 Learn**

- Watch **[Breaking Down Tornado Cash](https://learn.0xparc.org/materials/circom/learning-group-1/breaking-down-tornado)** workshop by 0xParc.
- Watch **[Poseidon-Tornado and Unit Testing](https://www.youtube.com/watch?v=-N6lI6kD65M)** by Chih-Cheng Liang.
  - Follow along with \*\*[his notes](https://hackmd.io/ISJ8sw7HTgysMNe0hW8iTA?view).
- Study **[Tornado Cash Circuits](https://github.com/tornadocash/tornado-core)**.
- Watch **[this video](https://www.youtube.com/watch?v=tJjDVlnkmyA&list=PL_SqG412uYVYtEM8B8xNccFyhrGsMV1MG&index=9)** covering the Tornado Cash whitepaper by Darth Cy.
  - If the whitepaper section is too dry, consider fast-forwarding to the “Implementation Planning” part of the video.
- Consider watching other videos in Darth Cy’s **[Tornado Cash series](https://www.youtube.com/playlist?list=PL_SqG412uYVYtEM8B8xNccFyhrGsMV1MG)**.
  - The **[final video](https://www.youtube.com/watch?v/4wyRZc_tKjw&list=PL_SqG412uYVYtEM8B8xNccFyhrGsMV1MG)** in the series is particularly enlightening (although quite long).
- Reflect on what nullifiers are and how they are used to keep anonymity in Tornado Cash.

### **3.2 Challenges**

- **Challenge 1**: Create a Token Mixer
  - _Note_: Attempt to make a barebones simplified version of a token mixer circuit. If you have time, try to make the smart contracts and a frontend for it too.

## **4. Bonus Content**

### **4.1 Semaphore and RLN**

Take a look at the circuits from **[Semaphore](https://github.com/semaphore-protocol/semaphore/tree/main/packages/circuits)** and **[RLN](https://github.com/Rate-Limiting-Nullifier/circom-rln)** and try to understand how they work.

### **4.2 Battlezips**

Previous PSE grantee, **[jp4g.eth](https://twitter.com/jp4g_)**, has an excellent series on Battlezips. This is the ZK version of the classic **[Battleship board game](<https://en.wikipedia.org/wiki/Battleship_(game)>)**.

All **[five videos](https://www.youtube.com/playlist?list=PLWACGbvIsEgn44LlTiPgVkOC4nG8tnJX-)** combined is only about 1.5 hours long. The **[channel](https://www.youtube.com/@battlezipszeroknowledgecra7405/playlists)** itself also has some videos on Noir and Halo2, for those who are interested.

# **Module 7 - Week 2**

Now it’s time to get acquainted with open-source, Github, and starting your own project!

## **Day 1 - Stage 1 Curriculum Feedback**

One of the ultimate goals of this program is to encourage you to explore the world of open-source development. As such, we will take one day away from the technical content and ask you for your feedback on the Stage 1 curriculum.

It’s important to keep in mind that this is the first time this program has been run. So there are likely many issues and inefficiencies you have experienced so far and we would like to hear about them.

Some of the most famous open-source programmers started their open-source careers just correcting spelling and grammar mistakes. No change is too small! This exercise is meant to get you acquainted with the Github workflow.

If you’re not familiar with Git and Github, please take a look at **[this video](https://www.youtube.com/watch?v=tRZGeaHPoaw)** for a quick introduction to Git and Github.

For making a pull request, checkout **[this video](https://www.youtube.com/watch?v=8lGpZkjnkt4)**.

Finally, check out **[this article](https://www.freecodecamp.org/news/how-to-use-git-best-practices-for-beginners/)** on best practices with Git and Github.

### **Steps**

Once you feel ready, please attempt the following:

1. Take a look at this **[repository](https://github.com/adrianmcli/summer-contribution-program)**.
2. File an “Issue” under the issue tab with what you’d like to improve (or a problem you want to point out).
3. Engage in conversation with the repository maintainer.
4. Volunteer to take up an issue and submit a “pull request” (PR).
   - _Note_: You’ll need to fork and clone the repo first, and then make a new branch. This is explained in the pull request video above.
5. Wait for some feedback and make changes as necessary.
6. See your changes get merged!

As with the rest of this program, this part is also an experiment. So please bear with us throughout this process!

## **Day 2 to Day 5 - Explore your own project!**

For the rest of this week, we invite you to come up with your own ideas! Please talk to your mentors (and each other) and come up with something you would like to build.

Feel free to take some inspiration from the projects you’ve learned about in this course. Sometimes, a small variation on an existing project can be just as exciting!

### **Steps**

1. Analyze everything you’ve learned so far, as well as projects that you’ve come across.
2. Come up with a few ideas for what you want to build.
3. Engage mentors (and peers) for feedback on your idea.
4. Create a new repository on [Github](https://github.com/new).
5. Create issues for each of the tasks required to complete this project (this will be your TODO list).
6. Get started building and remember to practice good [Git hygiene](https://grotoned.medium.com/git-hygiene-fadf533eb256)!
