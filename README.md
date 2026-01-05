# Introduction to SMPC: A fork of TinySMPC with Lectures and Exercises, and an added Secret Comparison operator

This is a fork of Kenny Song's [TinySMPC](https://github.com/kennysong/tinysmpc).  The main changes are:
- Added a secret comparison function that works with more than two parties, implemented in `shared_comparison.py`, called with `greater_than` (and, under the hood, `private_compare_without_decomp`).  (Also added tests to `tests.ipynb` for this.)
- Added some slides and lecture materials in `slides_and_lecture_materials`.

Like the original, this code is intended for educational rather than practical purposes.

## Getting Started

Run the jupyter notebook located at
```
slides_and_lecture_materials/pcmpc.ipynb 
```
which will walk you through a short tutorial for MPC in general!

## Implementation

TinySMPC implements [additive secret sharing](https://cs.nyu.edu/courses/spring07/G22.3033-013/scribe/lecture01.pdf) for creating encrypted shares on private data.

On top of additive secret sharing, we implement several [SMPC](https://en.wikipedia.org/wiki/Secure_multi-party_computation) protocols, which allow us to directly perform computations on encrypted data.

Here's a summary of the encrypted operations that TinySMPC supports.

|                    | Supported?              | Implementation                                                                          |
|--------------------|-------------------------|-----------------------------------------------------------------------------------------|
| **Addition**       | ✅                       | [SPDZ](https://eprint.iacr.org/2011/535.pdf) algorithm. <br/> See [shared_addition.py](https://github.com/kennysong/tinysmpc/blob/master/tinysmpc/shared_addition.py)             |
| **Subtraction**    | ✅                       | In terms of addition and multiplication.                                                 |
| **Multiplication** | ✅                       | [SPDZ](https://eprint.iacr.org/2011/535.pdf) algorithm.  <br/> See [shared_multiplication.py](https://github.com/kennysong/tinysmpc/blob/master/tinysmpc/shared_multiplication.py) |
| **Division**       | ❌ (too complicated)     | Possible with [SecureNN](https://eprint.iacr.org/2018/442.pdf).                                                                                       |
| **Exponentiation**       | ✅ (public integer only)     | In terms of multiplication.                                                                                       |
| **Greater Than**   | ✅ (prime moduli)<br/> ✅  (int64 moduli: 2-party, public integer only) | [Sharemind](https://sharemind.cyber.ee/files/papers/sharemind_with_shamir_turban_2014.pdf) algorithm. <br/> [SecureNN](https://eprint.iacr.org/2018/442.pdf) algorithm.     |

