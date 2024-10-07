# Week 4 - PLONK

Recall that you should have some basic knowledge of Rust from completing [Rustlings](https://rustlings.cool/) in Week 0. The required exercise this week is to publish a blogpost on PLONK and present it at the end of the week with your group.

## Study

When you start to learn ZK proof system, you are really advised to start from PLONK than any other proof system. There're a bunch of amazing articles out there, but instead of jumping into rabbit hole, you should start from [Vitalik's blog post](https://vitalik.eth.limo/general/2019/09/22/plonk.html) and focus on reading it all.
With this article you can understand what is widely used plonkish style of circuit arithemization. For this article, you may be unable to understand all the details at once, but you should at least understand what this diagram mean:
![Vitalik's circuit](./assets/vitalik-circuit.png)

Let's examine PLONK from a broader perspective compared to the detailed analysis in the paper. [ZKP MOOC Lec 5](https://www.youtube.com/watch?v=A0oZVEXav24)

Read Plonkathon Referenced Version. If you want to challenge yourself, You can implement it.
https://github.com/0xPARC/plonkathon/tree/reference


### Reference Material (optional)

In order to understand PLONKathon, you might need to understand the following concepts, but only read it when you really feel like.

1. There's the [website for plonkathon](https://plonkathon.com/), at this moment, you should already understand elliptic curve, pairing. You might need to understand Fiat-Shamir heuristic and Fast Fourier Transform to understand the code. They also have [video play list explaining each stage](https://www.youtube.com/playlist?list=PLNK7oFq6eaEzHNYHpQ_zbgPEBDhLmyfFb)
2. Schwartz Zippel Lemma https://brilliant.org/wiki/schwartz-zippel-lemma/
3. Lagrange interpolation https://en.wikipedia.org/wiki/Lagrange_polynomial
4. FFT https://www.youtube.com/watch?v=h7apO7q16V0. Put it simply, FFT and Inverse FFT are turning polynomials from coefficient domain into evaluation domain and vice versa.
5. Fiat-Shamir heuristic. Put it simply, normally interactive proof is done by sending the challenge to the verifier and the verifier will send the challenge to the prover. It's a way to turn the interactive proof into non-interactive proof by hashing the existing computation trace and use it as the challenge. 
6. Library for PLONK implementation, with focus on a production level implementation: [Jellyfish](https://github.com/EspressoSystems/jellyfish), [Dusk-network](https://github.com/dusk-network/plonk)
