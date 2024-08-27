# Module 6 Answers

### 2.1 Trusted Setup

1. What does the circuit in `HelloWorld.circom` do?
    - *Answer*: It multiplies two input signals to produce an output signal.
2. Lines 7-12 of `compile-HelloWorld.sh` download a file called `powersOfTau28_hez_final_10.ptau` for Phase 1 trusted setup. What is a Powers of Tau ceremony? Explain why this is important in the setup of zk-SNARK applications.
    - *Answer*: The trusted setup ceremony MPC schemes are interactive protocols involving multiple parties who contribute randomness to iteratively construct the common reference string (CRS). The key to this technique is that all parties need to keep their inputs (their sampled randomness) hidden. As long as the answer talks about the setup ceremony it’s ok, no need to be Powers of Tau specific.
3. Line 24 of `compile-HelloWorld.sh` makes a random entropy contribution as a Phase 2 trusted setup. How are Phase 1 and Phase 2 trusted setup ceremonies different from each other?
    - *Answer*: Phase 1 is universal, Phase 2 is circuit-specific.

### 2.2 Non-Quadratic Constraints

Here, you will learn about an important restriction on Circom circuits.

1. In the empty `scripts/compile-Multiplier3-groth16.sh`, create a script to compile `contracts/circuits/Multiplier3.circom` and create a verifier contract modeled after `compile-HelloWorld.sh`.
```bash
#!/bin/bash

# [assignment] create your own bash script to compile Multiplier3.circom modeling after compile-HelloWorld.sh below

cd contracts/circuits

mkdir Multiplier3

if [ -f ./powersOfTau28_hez_final_10.ptau ]; then
    echo "powersOfTau28_hez_final_10.ptau already exists. Skipping."
else
    echo 'Downloading powersOfTau28_hez_final_10.ptau'
    wget https://hermez.s3-eu-west-1.amazonaws.com/powersOfTau28_hez_final_10.ptau
fi

echo "Compiling Multiplier3.circom..."

# compile circuit

circom Multiplier3.circom --r1cs --wasm --sym -o Multiplier3
snarkjs r1cs info Multiplier3/Multiplier3.r1cs  # print the number of constraints in Multiplier3.r1cs

# Start a new zkey and make a contribution

snarkjs groth16 setup Multiplier3/Multiplier3.r1cs powersOfTau28_hez_final_10.ptau Multiplier3/circuit_0000.zkey
snarkjs zkey contribute Multiplier3/circuit_0000.zkey Multiplier3/circuit_final.zkey --name="1st Contributor Name" -v -e="random text"
snarkjs zkey export verificationkey Multiplier3/circuit_final.zkey Multiplier3/verification_key.json

# generate solidity contract
snarkjs zkey export solidityverifier Multiplier3/circuit_final.zkey ../Multiplier3Verifier.sol

cd ../..    
```
2. Try to run `compile-Multiplier3-groth16.sh`. You should encounter an `error[T3001]` with the circuit as-is. Explain what the error means and how it arises.
    - *Answer*: The error is a non-quadratic constraint. You should use an intermediate signal to do the multiplication of two input signals first, and then the third.
3. Modify `Multiplier3.circom` to perform a multiplication of three input signals under the restrictions of circom.
```circom
pragma circom 2.0.0;

// [assignment] Modify the circuit below to perform a multiplication of three signals

template Multiplier3 () {  

   // Declaration of signals.  
   signal input a;  
   signal input b;
   signal input c;
   signal temp;
   signal output d;  

   // Constraints.
   temp <== a * b;
   d <== temp * c;
}

component main = Multiplier3();
```

### 2.3 Groth16 and PLONK

In the empty `scripts/compile-Multiplier3-plonk.sh`, create a script to compile `circuit/Multiplier3.circom` using PLONK in SnarkJS. Add a `_plonk` suffix to the build folder and the output contract to distinguish the two sets of output.

1. You will encounter an error `zkey file is not groth16` if you just change `snarkjs groth16 setup` to `snarkjs plonk setup`. Resolve this error and answer the following question: *How is the process of compiling with PLONK different from compiling with Groth16?*
    - *Answer*: Phase 2 (circuit-specific) contribution not required.
3. What are the practical differences between Groth16 and PLONK? Hint: compare and contrast the resulting contracts and running time of unit tests (see the next question below) from the two protocols.
    - *Answer*: PLONK contract size is larger, gas cost is higher, and verification is time longer.

### 2.4 Verify and Test

So far we have not tested our circuit yet. While you can verify your circuit in the terminal using `snarkjs groth16 fullprove`, you can also do so directly in a Node.js script. We will practice doing so by creating some unit tests to try out our verifier contract(s):

1. Running `npx hardhat test` will prompt an `error HH606`. Before we can test our verifier contracts with hardhat, we must modify the Solidity version. In `scripts/bump-solidity.js`, we have already written the regular expressions to modify `HelloWorldVerifier.sol`. Add some code to `bump-solidity.js` to do the same for your new contract for `Multiplier3`.

```bash
const fs = require("fs");
const solidityRegex = /pragma solidity \^\d+\.\d+\.\d+/

const groth16VerifierRegex = /contract Groth16Verifier/

let content = fs.readFileSync("./contracts/HelloWorldVerifier.sol", { encoding: 'utf-8' });
let bumped = content.replace(solidityRegex, 'pragma solidity ^0.8.0');
bumped = bumped.replace(groth16VerifierRegex, 'contract HelloWorldVerifier');

fs.writeFileSync("./contracts/HelloWorldVerifier.sol", bumped);

// [assignment] add your own scripts below to modify the other verifier contracts you will build during the assignment

// Multiplier2 (with Groth16)
let content2 = fs.readFileSync("./contracts/Multiplier3Verifier.sol", { encoding: 'utf-8' });
let bumped2 = content2.replace(solidityRegex, 'pragma solidity ^0.8.0');
bumped2 = bumped2.replace(groth16VerifierRegex, 'contract Multiplier3Verifier');

fs.writeFileSync("./contracts/Multiplier3Verifier.sol", bumped2);

// Multiplier3 (with Plonk)
const plonkVerifierRegex = /contract PlonkVerifier/

let content3 = fs.readFileSync("./contracts/Multiplier3Verifier_plonk.sol", { encoding: 'utf-8' });
let bumped3 = content3.replace(solidityRegex, 'pragma solidity ^0.8.0');
bumped3 = bumped3.replace(plonkVerifierRegex, 'contract Multiplier3Verifier_plonk');

fs.writeFileSync("./contracts/Multiplier3Verifier_plonk.sol", bumped3);
```

2. You can now perform the unit tests for `HelloWorldVerifier` by running `npm run test`. Add comments to explain what each line in `test/test.js` is doing.
3. In `test/test.js`, add the unit tests for `Multiplier3` for both the Groth16 and PLONK versions. Ensure all tests pass (for `HelloWorld`, `Multiplier3 with Groth16`, and `Multiplier3 with PLONK`).

`test/test.js`:

```javascript
const { expect, assert } = require("chai");
const { ethers } = require("hardhat");
const { groth16, plonk } = require("snarkjs");

const wasm_tester = require("circom_tester").wasm;

const F1Field = require("ffjavascript").F1Field;
const Scalar = require("ffjavascript").Scalar;
exports.p = Scalar.fromString(
  "21888242871839275222246405745257275088548364400416034343698204186575808495617"
);
const Fr = new F1Field(exports.p);

describe("HelloWorld", function () {
  this.timeout(100000000);
  let Verifier;
  let verifier;

  beforeEach(async function () {
    Verifier = await ethers.getContractFactory("HelloWorldVerifier");
    verifier = await Verifier.deploy();
    await verifier.deployed();
  });

  it("Circuit should multiply two numbers correctly", async function () {
    const circuit = await wasm_tester("contracts/circuits/HelloWorld.circom");

    const INPUT = {
      a: 2,
      b: 3,
    };

    const witness = await circuit.calculateWitness(INPUT, true);

    //console.log(witness);

    assert(Fr.eq(Fr.e(witness[0]), Fr.e(1)));
    assert(Fr.eq(Fr.e(witness[1]), Fr.e(6)));
  });

  it("Should return true for correct proof", async function () {
    //[assignment] Add comments to explain what each line is doing

    // create a proof and public signals from the circuit and some input
    const { proof, publicSignals } = await groth16.fullProve(
      { a: "2", b: "3" },
      "contracts/circuits/HelloWorld/HelloWorld_js/HelloWorld.wasm",
      "contracts/circuits/HelloWorld/circuit_final.zkey"
    );

    // print out "c" in the circuit (i.e. the result of the private inputs)
    console.log("2x3 =", publicSignals[0]);

    // create a string of the calldata for the verifier contract
    const calldata = await groth16.exportSolidityCallData(proof, publicSignals);

    // convert the calldata string into an array of BigInts
    const argv = calldata
      .replace(/["[\]\s]/g, "")
      .split(",")
      .map((x) => BigInt(x).toString());

    const a = [argv[0], argv[1]];
    const b = [
      [argv[2], argv[3]],
      [argv[4], argv[5]],
    ];
    const c = [argv[6], argv[7]];
    const Input = argv.slice(8);

    expect(await verifier.verifyProof(a, b, c, Input)).to.be.true;
  });
  it("Should return false for invalid proof", async function () {
    let a = [0, 0];
    let b = [
      [0, 0],
      [0, 0],
    ];
    let c = [0, 0];
    let d = [0];
    expect(await verifier.verifyProof(a, b, c, d)).to.be.false;
  });
});

describe("Multiplier3 with Groth16", function () {
  beforeEach(async function () {
    //[assignment] insert your script here
    Verifier = await ethers.getContractFactory("Multiplier3Verifier");
    verifier = await Verifier.deploy();
    await verifier.deployed();
  });

  it("Circuit should multiply three numbers correctly", async function () {
    //[assignment] insert your script here
    const circuit = await wasm_tester("contracts/circuits/Multiplier3.circom");

    const INPUT = {
      a: 2,
      b: 3,
      c: 4,
    };

    const witness = await circuit.calculateWitness(INPUT, true);

    assert(Fr.eq(Fr.e(witness[0]), Fr.e(1)));
    assert(Fr.eq(Fr.e(witness[1]), Fr.e(24)));
  });

  it("Should return true for correct proof", async function () {
    //[assignment] insert your script here

    const { proof, publicSignals } = await groth16.fullProve(
      { a: "2", b: "3", c: "4" },
      "contracts/circuits/Multiplier3/Multiplier3_js/Multiplier3.wasm",
      "contracts/circuits/Multiplier3/circuit_final.zkey"
    );

    console.log("2x3x4 =", publicSignals[0]);

    const calldata = await groth16.exportSolidityCallData(proof, publicSignals);

    const argv = calldata
      .replace(/["[\]\s]/g, "")
      .split(",")
      .map((x) => BigInt(x).toString());

    const a = [argv[0], argv[1]];
    const b = [
      [argv[2], argv[3]],
      [argv[4], argv[5]],
    ];
    const c = [argv[6], argv[7]];

    const Input = argv.slice(8);

    expect(await verifier.verifyProof(a, b, c, Input)).to.be.true;
  });

  it("Should return false for invalid proof", async function () {
    //[assignment] insert your script here
    let a = [0, 0];
    let b = [
      [0, 0],
      [0, 0],
    ];
    let c = [0, 0];
    let d = [0];
    expect(await verifier.verifyProof(a, b, c, d)).to.be.false;
  });
});

describe("Multiplier3 with PLONK", function () {
  beforeEach(async function () {
    //[assignment] insert your script here
    Verifier = await ethers.getContractFactory("Multiplier3Verifier_plonk");
    verifier = await Verifier.deploy();
    await verifier.deployed();
  });

  it("Should return true for correct proof", async function () {
    //[assignment] insert your script here
    const { proof, publicSignals } = await plonk.fullProve(
      { a: "2", b: "3", c: "4" },
      "contracts/circuits/Multiplier3_plonk/Multiplier3_js/Multiplier3.wasm",
      "contracts/circuits/Multiplier3_plonk/circuit_final.zkey"
    );

    console.log("2x3x4 =", publicSignals[0]);

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

    expect(await verifier.verifyProof(calldata, publicSignals)).to.be.true;
  });

  it("Should return false for invalid proof", async function () {
    //[assignment] insert your script here
    let calldata = new Array(24).fill(0);
    let publicSignals = [0];
    expect(await verifier.verifyProof(calldata, publicSignals)).to.be.false;
  });
});
```

### 2.5 Circuit Libraries

In this section, you will be learning about libraries that you can import to create more complicated circuits. The original exercises are found in the Q3 directory, however we will present the code here for your convenience.

#### Tip: For this section, use [**zkREPL**](https://zkrepl.dev/) for quick compiling and testing of circuits

### 2.5.1 circomlib

- `LessThan10.circom` implements a circuit that verifies an input is less than 10 using the [LessThan](https://github.com/iden3/circomlib/blob/master/circuits/comparators.circom#L89) template. Study how the template is used in this circuit. What does the 32 in Line 9 stand for?
    - *Answer*: Maximum number of bits of the input.
- What are the possible outputs for the `LessThan` template and what do they mean respectively? If you cannot figure this out by reading the code alone, feel free to compile the circuit and test with different input values.
    - *Answer*: 1 if true, 0 if false
- Proving a number is within a range without revealing the actual number could be useful in applications like proving our income when applying for a credit card. In the following code `RangeProof.circom`, create a template that uses `GreaterEqThan` and `LessEqThan` to perform a range proof.

Answer for `RangeProof.circom`:

```circom
pragma circom 2.1.4;

include "circomlib/comparators.circom";

template RangeProof(n) {
    assert(n <= 252);
    signal input in; // this is the number to be proved inside the range
    signal input range[2]; // the two elements should be the range, i.e. [lower bound, upper bound]
    signal output out;
    signal result;

    component lt = LessEqThan(n);
    component gt = GreaterEqThan(n);

    // Check if in is greater or equal to the lower bound
    gt.in[0] <== in;
    gt.in[1] <== range[0];

    // Check if in is less or equal to the upper bound
    lt.in[0] <== in;
    lt.in[1] <== range[1];

    // The result is 1 if both conditions also return 1
    out <== gt.out * lt.out;
}

component main { public [ range ] } = RangeProof(32);

/* INPUT = {
    "in": "5",
    "range": ["1", "10"]
} */
```

### 2.5.2 circomlib-matrix and Sudoku

```circom
pragma circom 2.1.4;

include "https://github.com/socathie/circomlib-matrix/blob/master/circuits/matAdd.circom";
include "https://github.com/socathie/circomlib-matrix/blob/master/circuits/matElemMul.circom";
include "https://github.com/socathie/circomlib-matrix/blob/master/circuits/matElemSum.circom";
include "https://github.com/socathie/circomlib-matrix/blob/master/circuits/matElemPow.circom";
include "circomlib/poseidon.circom";
include "circomlib/comparators.circom";

template RangeProof(n) {
    assert(n <= 252);
    signal input in; // this is the number to be proved inside the range
    signal input range[2]; // the two elements should be the range, i.e. [lower bound, upper bound]
    signal output out;
    signal result;

    component lt = LessEqThan(n);
    component gt = GreaterEqThan(n);

    // Check if in is greater or equal to the lower bound
    gt.in[0] <== in;
    gt.in[1] <== range[0];

    // Check if in is less or equal to the upper bound
    lt.in[0] <== in;
    lt.in[1] <== range[1];

    // The result is 1 if both conditions also return 1
    out <== gt.out * lt.out;
}

template sudoku() {
    signal input puzzle[9][9]; // 0  where blank
    signal input solution[9][9]; // 0 where original puzzle is not blank
    signal output out;

    // check whether the solution is zero everywhere the puzzle has values (to avoid trick solution)

    component mul = matElemMul(9,9);
    
    //[assignment] hint: you will need to initialize your RangeProof components here
    component puzRange[9][9];
    component solRange[9][9];
    for (var i=0; i<9; i++) {
        for (var j=0; j<9; j++) {
            puzRange[i][j] = RangeProof(32);
            puzRange[i][j].range[0] <== 0;
            puzRange[i][j].range[1] <== 9;
            solRange[i][j] = RangeProof(32);
            solRange[i][j].range[0] <== 0;
            solRange[i][j].range[1] <== 9;
        }
    }
    
    for (var i=0; i<9; i++) {
        for (var j=0; j<9; j++) {
            puzRange[i][j].in <== puzzle[i][j];
            solRange[i][j].in <== puzzle[i][j];
            assert(puzRange[i][j].out == 1);
            assert(solRange[i][j].out == 1);
            mul.a[i][j] <== puzzle[i][j];
            mul.b[i][j] <== solution[i][j];
        }
    }
    for (var i=0; i<9; i++) {
        for (var j=0; j<9; j++) {
            mul.out[i][j] === 0;
        }
    }

    // sum up the two inputs to get the full solution and square the full solution

    component add = matAdd(9,9);
    
    for (var i=0; i<9; i++) {
        for (var j=0; j<9; j++) {
            add.a[i][j] <== puzzle[i][j];
            add.b[i][j] <== solution[i][j];
        }
    }

    component square = matElemPow(9,9,2);

    for (var i=0; i<9; i++) {
        for (var j=0; j<9; j++) {
            square.a[i][j] <== add.out[i][j];
        }
    }

    // check all rows and columns and blocks sum to 45 and sum of squares = 285

    component row[9];
    component col[9];
    component block[9];
    component rowSq[9];
    component colSq[9];
    component blockSq[9];


    for (var k=0; k<9; k++) {
        row[k] = matElemSum(1,9);
        col[k] = matElemSum(1,9);
        block[k] = matElemSum(3,3);

        rowSq[k] = matElemSum(1,9);
        colSq[k] = matElemSum(1,9);
        blockSq[k] = matElemSum(3,3);

        for (var i=0; i<9; i++) {
            row[k].a[0][i] <== add.out[k][i];
            col[k].a[0][i] <== add.out[i][k];

            rowSq[k].a[0][i] <== square.out[k][i];
            colSq[k].a[0][i] <== square.out[i][k];
        }
        var x = 3*(k%3);
        var y = 3*(k\3);
        for (var i=0; i<3; i++) {
            for (var j=0; j<3; j++) {
                block[k].a[i][j] <== add.out[x+i][y+j];
                blockSq[k].a[i][j] <== square.out[x+i][y+j];
            }
        }
        row[k].out === 45;
        col[k].out === 45;
        block[k].out === 45;

        rowSq[k].out === 285;
        colSq[k].out === 285;
        blockSq[k].out === 285;
    }

    // hash the original puzzle and emit so that the dapp can listen for puzzle solved events

    component poseidon[9];
    component hash;

    hash = Poseidon(9);
    
    for (var i=0; i<9; i++) {
        poseidon[i] = Poseidon(9);
        for (var j=0; j<9; j++) {
            poseidon[i].inputs[j] <== puzzle[i][j];
        }
        hash.inputs[i] <== poseidon[i].out;
    }

    out <== hash.out;
}

component main = sudoku();

/* INPUT = {
    "puzzle": [
        ["1", "0", "0", "0", "0", "0", "0", "0", "0"],
        ["0", "8", "0", "0", "0", "0", "0", "0", "0"],
        ["0", "0", "6", "0", "0", "0", "0", "0", "0"],
        ["0", "0", "0", "5", "0", "0", "0", "0", "0"],
        ["0", "0", "0", "0", "3", "0", "0", "0", "0"],
        ["0", "0", "0", "0", "0", "1", "0", "0", "0"],
        ["0", "0", "0", "0", "0", "0", "9", "0", "0"],
        ["0", "0", "0", "0", "0", "0", "0", "7", "0"],
        ["0", "0", "0", "0", "0", "0", "0", "0", "5"]
    ],
    "solution": [
        ["0", "7", "4", "2", "8", "5", "3", "9", "6"],
        ["2", "0", "5", "3", "9", "6", "4", "1", "7"],
        ["3", "9", "0", "4", "1", "7", "5", "2", "8"],
        ["4", "1", "7", "0", "2", "8", "6", "3", "9"],
        ["5", "2", "8", "6", "0", "9", "7", "4", "1"],
        ["6", "3", "9", "7", "4", "0", "8", "5", "2"],
        ["7", "4", "1", "8", "5", "2", "0", "6", "3"],
        ["8", "5", "2", "9", "6", "3", "1", "0", "4"],
        ["9", "6", "3", "1", "7", "4", "2", "8", "0"]
    ]
} */
```
