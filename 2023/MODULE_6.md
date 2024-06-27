# Module 6 - Intro to Circuits

As you know from Module 4, one of the first steps of creating zero knowledge proofs is to convert your problem into circuits. There are currently two popular ways of writing circuits, Circom and Halo2.

Circom is a language designed specifically for writing zk-SNARK circuits. It plays a crucial role in creating zero-knowledge proofs, allowing for privacy and scalability in blockchain applications. Halo2, on the other hand, is a newer framework that offers some unique advantages. While it may not have as many resources available for learning, it's gaining traction in the community.


Given that Circom has been around longer, in this module, we will focus on getting you setup with Circom and to start writing some simple circuits with it.

## 1. Getting Started with Circom

To get started, we will go through a few of the pages of the Circom 2 documentation:

1. [**Installation [of Circom and SnarkJS]**](https://docs.circom.io/getting-started/installation/)
2. [**Writing Circuits**](https://docs.circom.io/getting-started/writing-circuits/)
3. [**Compiling Circuits**](https://docs.circom.io/getting-started/compiling-circuits/)  ([note for Apple Silicon users](https://github.com/iden3/circom/issues/201))
4. [**Computing the Witness**](https://docs.circom.io/getting-started/computing-the-witness/)
5. [**Proving Circuits**](https://docs.circom.io/getting-started/proving-circuits/)

You might also find the following tutorials useful:

- https://github.com/enricobottazzi/ZKverse
- https://www.samsclass.info/141/proj/C523.htm

## 2. Circom Crash Course 💪

Now that you have a basic idea of Circom and SnarkJS, let's play around with it a bit more. **This section will include questions that you should answer for this module.**

The content below is an updated and adapted version of a [set of exercises](https://zku.gnomio.com/mod/assign/view.php?id=117) from ZK University (ZKU). You can still access the original content if you click the "Access as a guest" button in the link above, but we will continue here:

1. Fork and clone this repo: https://github.com/adrianmcli/week1 
2. Go into the Q2 directory and run `npm install`

### 2.1 Trusted Setup

In the `contracts/circuits` folder, you will find `HelloWorld.circom`. Run the bash script `scripts/compile-HelloWorld.sh` to compile the circuit. Answer the following questions:

1. What does the circuit in `HelloWorld.circom` do?
2. Lines 7-12 of `compile-HelloWorld.sh` download a file called `powersOfTau28_hez_final_10.ptau` for Phase 1 trusted setup. What is a Powers of Tau ceremony? Explain why this is important in the setup of zk-SNARK applications.
3. Line 24 of `compile-HelloWorld.sh` makes a random entropy contribution as a Phase 2 trusted setup. How are Phase 1 and Phase 2 trusted setup ceremonies different from each other?

### 2.2 Non-Quadratic Constraints

Here, you will learn about an important restriction on Circom circuits.

1. In the empty `scripts/compile-Multiplier3-groth16.sh`, create a script to compile `contracts/circuits/Multiplier3.circom` and create a verifier contract modelled after `compile-HelloWorld.sh`.
2. Try to run `compile-Multiplier3-groth16.sh`. You should encounter an `error[T3001]` with the circuit as-is. Explain what the error means and how it arises.
3. Modify `Multiplier3.circom` to perform a multiplication of three input signals under the restrictions of circom.

### 2.3 Groth16 and PLONK

In the empty `scripts/compile-Multiplier3-plonk.sh`, create a script to compile `circuit/Multiplier3.circom` using PLONK in SnarkJS. Add a `_plonk` suffix to the build folder and the output contract to distinguish the two sets of output.

1. You will encounter an error `zkey file is not groth16` if you just change `snarkjs groth16 setup` to `snarkjs plonk setup`. Resolve this error and answer the following question: *How is the process of compiling with PLONK different from compiling with Groth16?*
2. What are the practical differences between Groth16 and PLONK? Hint: compare and contrast the resulting contracts and running time of unit tests (see the next question below) from the two protocols.

### 2.4 Verify and Test

So far we have not tested our circuit yet. While you can verify your circuit in the terminal using `snarkjs groth16 fullprove`, you can also do so directly in a Node.js script. We will practice doing so by creating some unit tests to try out our verifier contract(s):

1. Running `npx hardhat test` will prompt an `error HH606`. Before we can test our verifier contracts with hardhat, we must modify the Solidity version. In `scripts/bump-solidity.js`, we have already written the regular expressions to modify `HelloWorldVerifier.sol`. Add some code to `bump-solidity.js` to do the same for your new contract for `Multiplier3`.
2. You can now perform the unit tests for `HelloWorldVerifier` by running `npm run test`. Add comments to explain what each line in `test/test.js` is doing.
3. In `test/test.js`, add the unit tests for `Multiplier3` for both the Groth16 and PLONK versions. Ensure all tests pass (for `HelloWorld`, `Multiplier3 with Groth16`, and `Multiplier3 with PLONK`).

#### Hint: SnarkJS API for Solidity Call Data Export

The value returned by `plonk.exportSolidityCallData(proof, publicSignals)` can be found [here](https://github.com/iden3/snarkjs/blob/master/src/plonk_exportsoliditycalldata.js) and it is a little non-standard. You might need to do some string manipulation:

```javascript
let rawCalldata = await plonk.exportSolidityCallData(proof, publicSignals);

// fix string by replacing "][" with ", "
const fixedStr = rawCalldata.replace(/\]\[/g, ", ");

// convert the calldata string into an array of BigInts
const fixedArray = fixedStr
  .replace(/["[\]\s]/g, "")
  .split(",")
  .map((x) => BigInt(x).toString());

// drop the last element of the array (the inputs)
const calldata = [...fixedArray.slice(0, -1)];
```

### 2.5 Circuit Libraries

In this section, you will be learning about libraries that you can import to create more complicated circuits. The original exercises are found in the Q3 directory, however we will present the code here for your convenience.

#### Tip: For this section, use [**zkREPL**](https://zkrepl.dev/) for quick compiling and testing of circuits

### 2.5.1 circomlib

[circomlib](https://github.com/iden3/circomlib) is the official library of circuit templates released by iden3, the creator of Circom. One important template included is [comparators.circom](https://github.com/iden3/circomlib/blob/master/circuits/comparators.circom), which implements value comparisons between two numbers.

Here is `LessThan10.circom`:

```circom
pragma circom 2.1.4;

include "circomlib/comparators.circom";

template LessThan10() {
    signal input in;
    signal output out;

    component lt = LessThan(32); 

    lt.in[0] <== in;
    lt.in[1] <== 10;

    out <== lt.out;
}

component main { public [ in ] } = LessThan10();

/* INPUT = {
    "in": "10"
} */
```

- `LessThan10.circom` implements a circuit that verifies an input is less than 10 using the [LessThan](https://github.com/iden3/circomlib/blob/master/circuits/comparators.circom#L89) template. Study how the template is used in this circuit. What does the 32 in Line 9 stand for?
- What are the possible outputs for the `LessThan` template and what do they mean respectively? If you cannot figure this out by reading the code alone, feel free to compile the circuit and test with different input values.
- Proving a number is within a range without revealing the actual number could be useful in applications like proving our income when applying for a credit card. In the following code `RangeProof.circom`, create a template that uses `GreaterEqThan` and `LessEqThan` to perform a range proof.

Here is the initial template for `RangeProof.circom`:

```circom
pragma circom 2.1.4;

include "circomlib/comparators.circom";

template RangeProof(n) {
    assert(n <= 252);
    signal input in; // this is the number to be proved inside the range
    signal input range[2]; // the two elements should be the range, i.e. [lower bound, upper bound]
    signal output out;

    component lt = LessEqThan(n);
    component gt = GreaterEqThan(n);

    // [assignment] insert your code here
}

component main { public [ range ] } = RangeProof(32);

/* INPUT = {
    "in": "5",
    "range": ["1", "10"]
} */
```

### 2.5.2 circomlib-matrix and Sudoku

[circomlib-matrix](https://github.com/socathie/circomlib-matrix) is a library covering basic matrix operations, modelled after circomlib, and created by our very own PSE member, Cathie So. Matrix operations can be useful in puzzles (e.g. [zkPuzzles](https://github.com/zku-cohort-3/zkPuzzles), [zkGames](https://github.com/vplasencia/zkGames)), image processing (e.g [zkPhoto](https://github.com/socathie/zkPhoto)), and machine learning (e.g. [zk-mnist](https://github.com/0xZKML/zk-mnist), [zk-ml](https://github.com/zk-ml/linear-regression-demo)). Let’s take a look at matrix operations in action in a Sudoku circuit.

Modify the following code so that it implements the check on the inputs to be between 0 and 9 (inclusive) using your RangeProof template from above.

👉 [**sudoku.circom**](https://gist.github.com/adrianmcli/776d86438592c0486603f04ac6cee26e)

Paste the above code into zkREPL to start working with it. Good luck on your final challenge of this module!

## Further Reading

Congratulations on reaching the end of this module. If you have extra time, it is ***highly recommended*** that you go through the following tutorial by PSE member, Vivian Plasencia:

👉 [**How to create a Zero Knowledge DApp: From zero to production**](https://vivianblog.hashnode.dev/how-to-create-a-zero-knowledge-dapp-from-zero-to-production)

It not only takes you through the process of creating your own circuits, but also guides you in the compilation of the associated smart contracts and the building of your frontend.

## Conclusion

This marks the end of this module and also the first stage of this program. The aim of the program was to give a broad overview of the technical theory, mathematical background, and hands-on practical usage of the technology underlying the future of Ethereum's scaling and privacy.

Going forward, we will practice more with writing circuits and eventually have you contribute to the open source community with your new skills!