## Comprehension

1. **Three-Coloring Graph problem with Hats**: To prove possession of a valid three-coloring for a given graph, the solution is written on the ground with each node covered with hats. The verifier can check the color under two connected hats without seeing the entire solution. The prover thus proves knowledge of a valid coloring without revealing it. This can be repeated multiple times to increase confidence. This is an interactive proof.

2. **Ali Baba’s Cave analogy**: In the cave, there's a magical door leading to two passages. The prover demonstrates knowledge of the secret word to open the door by complying with the verifier's request to exit through a chosen passage, without revealing the word itself. This can be repeated multiple times to increase confidence. This is an interactive proof.

3. **The difference between interactive and non-interactive proofs**:
    - **Interactive Proofs**: Require back-and-forth communication between the prover and verifier during the proof process.
    - **Non-Interactive Proofs**: The prover can send a single message to the verifier, who can then ascertain the validity of the proof without any further interaction.

## Modular Arithmetic

1. $7\ \text{mod}\ 13 = 7$
2. $15\ \text{mod}\ 13 = 2$
3. $(7+15)\ \text{mod}\ 13 = (22)\ \text{mod}\ 13 = 9$
4. $(7\ \text{mod}\ 13 + 15\ \text{mod}\ 13)\ \text{mod}\ 13 = (7+2)\ \text{mod}\ 13 = 9$

Since the results of the third and fourth calculations match, they do follow a "group structure." Notice that, it doesn't matter if you apply the `mod` immediately for each number (like in Q4) or at the end (like in Q3).

## Generators

1. **What does the term 'generator' mean?**
   A generator in a cyclic group is an element that, when repeatedly applied via the group's operation, produces every element in the group.

2. **Can you find a generator for this group?**
   Yes, in the group $(Z_{12}, +\ \text{mod}\ 12)$, the number 1 is a generator. Repeated addition by 1 modulo 12 produces every residue class.

3. **Are there other generators for this group? If yes, what are they?**
   Yes, there are other generators for this group. In $(Z_{12}, +\ \text{mod}\ 12)$, the numbers 5, 7, and 11 are also generators. You can verify this by checking that repeated addition by any of these numbers modulo 12 produces every residue class from 0 to 11.

## Implementing a Modular Arithmetic Calculator

Here's a JavaScript function for the modular arithmetic calculator:

```javascript
function modularCalculator(op, num1, num2, mod) {
    let result = 0;
    switch (op) {
        case '+':
            result = (num1 + num2) % mod;
            break;
        case '-':
            result = (num1 - num2) % mod;
            if (result < 0) result += mod;
            break;
        case '*':
            result = (num1 * num2) % mod;
            break;
        default:
            return "Invalid operation";
    }
    return result;
}

modularCalculator('+', 10, 15, 12); // Should return: 1
modularCalculator('-', 10, 15, 12); // Should return: 7
modularCalculator('*', 10, 15, 12); // Should return: 6
```

These answers should align well with the content provided in the module, helping students to understand and practice the concepts of Zero-Knowledge Proofs and modular arithmetic.
