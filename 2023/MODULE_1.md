# Module 1 - Intro to ZK

Welcome aboard! You've just embarked on an incredible journey into the realm of Zero-Knowledge Proofs (ZKPs). This fascinating aspect of cryptography provides the backbone for various privacy-preserving technologies. Notably, it's used in Ethereum, one of the most well-known blockchain platforms.

In this module, our primary goal is to introduce you to key concepts of ZKPs, such as soundness, completeness, and zero-knowledge itself. Additionally, we aim to cultivate your understanding of basic modular arithmetic through hands-on examples and exercises, which will prove vital for the subsequent modules.

Let’s get started!

## Tips to Learn Zero Knowledge

One really useful mental model to learn zero knowledge is to blackbox the concepts so that you don't get intimidated by the complexity of the topic. This doesn't mean you ignore the details, but rather, you focus on understanding the high-level concepts first and then dive into the details later.

When you study the topic for the first time, only read the required reading. Skip the optional reading unless you are really curious about the details. This will help you to understand the topic without getting overwhelmed by the details.

## A Primer for Zero Knowledge Proofs

Before we delve into the core content of the module, consider acquainting yourself with some high-level concepts of Zero-Knowledge Proofs. The following introductory articles will help you build a robust foundational understanding:

- [Zero-knowledge proofs | ethereum.org](https://ethereum.org/en/zero-knowledge-proofs/)
- [A Primer on Zero-Knowledge Proofs 🔏](https://medium.com/hackernoon/a-primer-on-zero-knowledge-proofs-892e6e277142)
- [Zero Knowledge Proofs: An illustrated primer [Part 1]](https://blog.cryptographyengineering.com/2014/11/27/zero-knowledge-proofs-illustrated-primer/)
- [Zero Knowledge Proofs: An illustrated primer [Part 2]](https://blog.cryptographyengineering.com/2017/01/21/zero-knowledge-proofs-an-illustrated-primer-part-2/)

You **DO NOT** have to read all of these articles, they are simply a starting point. However, throughout this course, we will provide you with a set of reflection questions to check your understanding.

:::info
**🤔 Consider the following:**
1. What are Zero-Knowledge Proofs?
2. What are the principles of soundness, completeness, and zero-knowledge?
3. What distinguishes interactive from non-interactive proofs?
:::

## Thought Experiments

Engaging with these thought experiments will make abstract concepts more tangible and facilitate a deeper understanding of ZKPs. Each of these examples offers a unique perspective on the concept of zero-knowledge proofs:

  - [Example 1: Where’s Waldo?](https://medium.com/swlh/a-zero-knowledge-proof-for-wheres-wally-930c21e55399)
  - [Example 2: Colored Balls (interactive)](https://en.wikipedia.org/wiki/Zero-knowledge_proof#Two_balls_and_the_colour-blind_friend)
  - [Example 3: Sudoku (non-interactive)](https://www.wisdom.weizmann.ac.il/~naor/PAPERS/SUDOKU_DEMO/)

:::info
**🤔 Consider the following:**
1. Which example did you find most enlightening, and why?
2. How do these examples demonstrate the principles of zero-knowledge proofs?
3. Can you think of any potential applications of these concepts in everyday life?
:::

## Use-Cases and Applications

To connect theory with practice, let's delve into the practical implications of ZKPs. The following resources illustrate how ZKPs are employed in real-world applications, particularly in the domain of blockchain:

- [Ethereum Use Cases for ZKPs](https://ethereum.org/en/zero-knowledge-proofs/#use-cases-for-zero-knowledge-proofs)
- [More Applications](https://link.springer.com/article/10.1007/s42452-019-0989-z#Sec4)

:::info
**🤔 Consider the following:**
1. Which application of ZKP do you find most intriguing, and why?
2. Can you imagine any other potential applications of ZKP?
:::

## Supplemental Materials on ZKPs [optional]

For more content (especially for those who prefer videos), check out the following:

- Video Lectures:
    - ['Introduction to Zero Knowledge Proofs' - Elena Nadolinski [19:59]](https://www.youtube.com/watch?v=BT88s7_VtC8)
    - [ZKP MOOC Lecture 1: Introduction and History of ZKP [1:38:32]](https://www.youtube.com/watch?v=uchjTIlPzFo)
    - [ZK Whiteboard Sessions - Module One: What is a SNARK? by Dan Boneh [42:08]](https://youtu.be/h-94UhJLeck)
    - [Detailed Explanation of Zero-Knowledge Proofs](https://youtu.be/9je336QIqAQ?t=650)
- [Thinking in Zero Knowledge](https://mirror.xyz/0x3FD6f213ae1B8a7B6bd8f14BE9BF316a5e5A5d28/VTGpmEYLKIslUPf66VQzHUneB0R7EhMpJJ_mGrMvTwY)

By this point in the module, you should have a broad and multifaceted understanding of ZKPs. However, we're not done yet. Next, we'll tackle some key mathematical concepts that underpin this topic.

## Number Theory [self research]

Building a strong foundation in number theory is essential for understanding upcoming modules. The following module from Khan Academy provides an excellent introduction to this topic:

- [An Introduction to Modular Math by Khan Academy](https://www.khanacademy.org/computing/computer-science/cryptography/modarithmetic/a/what-is-modular-arithmetic)

Below are topics that you will need to research independently (or with a teammate). This could mean searching these specific terms on Google, YouTube, Wikipedia, or even asking ChatGPT.

Don't forget to reach out to your team and the mentors on Discord when you're stuck!

### Topics to Research

- Fundamentals:
  - Prime Numbers and Composite Numbers
  - Greatest Common Divisors (GCD)

- Modular Arithmetic and Congruence
  - What is modular arithmetic?
  - Exploring congruence classes

- Group Theory
  - What is a group structure?
  - What is a group operation?

- Diving Deeper:
  - What is a finite group?
  - What is a cyclic group?
  - What is a generator?
  - What are finite fields?

:::info
**🤔 Consider the following:**
1. Which of these concepts did you find most challenging, and why?
2. Can you explain these concepts in your own words?
:::

# 💪 Exercises

Here are the exercises for this module. Collaborate with your team to find the answers, and remember to support each other!

## Comprehension

Summarize each of the following concepts in a few sentences:

1. Three-Colouring Graph problem with Hats
2.  Ali Baba’s Cave analogy
3.   The difference between interactive and non-interactive proofs

## Modular Arithmetic

Solve the following problems and gain a practical understanding of modular arithmetic:

1. $7\ mod\ 13$
2. $15\ mod\ 13$
3. $(7+15)\ mod\ 13$
4. $(7\ mod\ 13 + 15\ mod\ 13)\ mod\ 13$

If the results of the third and fourth calculations match, they follow a "group structure". Can you determine if these do?

## Generators

Consider the cyclic group $(Z_{12}, +\ mod\ 12)$, commonly referred to as the "additive group of integers modulo 12". Address the following points:

1. What does the term 'generator' mean?
2. Can you find a generator for this group?
3. Are there other generators for this group? If yes, what are they?

## Implementing a Modular Arithmetic Calculator

Your task is to implement a simple modular arithmetic calculator in JavaScript. The calculator should support three operations: addition, subtraction, and multiplication. 

The function `modularCalculator` should take four parameters:
- A string, `op`, indicating the operation. It will be one of '+', '-', or '*'.
- Two integers, `num1` and `num2`, which are the operands for the operation.
- An integer, `mod`, which is the modulus.

The function should return the result of performing the indicated operation on `num1` and `num2`, then taking the result modulo `mod`. 

Remember, the result of subtraction could be negative, and in this case, you should add `mod` to the result to ensure it's positive. 

For addition and multiplication, remember that JavaScript's % operator gives the remainder, not the modulus, but these will be the same for positive numbers.

**Code Template:**

```javascript
function modularCalculator(op, num1, num2, mod) {
    // Your code here
}

modularCalculator('+', 10, 15, 12); // Should return: 1
modularCalculator('-', 10, 15, 12); // Should return: 7
modularCalculator('*', 10, 15, 12); // Should return: 6
```

Feel free to use `console.log` statements in your code to verify that your function is working as expected. For convenience, consider using https://repljs.com/ and pasting in the above code snippet to get started.

## Conclusion
By the end of this module, you will have gained an understanding of the fundamental concepts in Zero-Knowledge Proofs (ZKPs). These principles will guide you in your journey towards mastering the advanced topics that will be covered in the following modules.
