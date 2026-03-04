# LC2K ISA Specification (EECS 470 Edition)

Welcome to the EECS 470 LC2K ISA specification! This document describes the assembly language and machine encoding of the instructions supported by the Little Computer 2000, an ISA used for educational purposes at the University of Michigan. 

> [!NOTE]
> The instruction set described here is based off of the [original EECS 370 LC2K specification](https://eecs370.github.io/project_1_spec/), with additional instructions added to make it a viable target for a C compiler. Any _assembly_ written in EECS 370 LC2K is guaranteed to be compatible with EECS 470 LC2K, but not the other way around, and machine code is generally _incompatible_ between versions.
> 
> Henceforth, assume "LC2K" refers to EECS 470 LC2K unless otherwise specified.

## Overview

- LC2K has 16 general-purpose registers, referred to by the numbers `0` to `15`. Each register is 32 bits wide. 
- Register `0` is hardwired to the value `0`. 
- Each memory address is 32 bits wide and corresponds to a 32-bit word (NOTE: This is UNLIKE modern systems where each address corresponds to a byte). 
- Primitive values that are larger than 32 bits (e.g. `uint64_t`) are stored in little-endian order.

## Instruction Encodings

![R-Type Encoding](images/r-type-light.svg#gh-light-mode-only)
![I-Type Encoding](images/i-type-light.svg#gh-light-mode-only)
![J-Type Encoding](images/j-type-light.svg#gh-light-mode-only)
![O-Type Encoding](images/o-type-light.svg#gh-light-mode-only)

![R-Type Encoding](images/r-type-dark.svg#gh-dark-mode-only)
![I-Type Encoding](images/i-type-dark.svg#gh-dark-mode-only)
![J-Type Encoding](images/j-type-dark.svg#gh-dark-mode-only)
![O-Type Encoding](images/o-type-dark.svg#gh-dark-mode-only)

## Instruction Set

| Mnemonic | Encoding | Opcode | Operation                                                                                                     |
|----------|----------|--------|---------------------------------------------------------------------------------------------------------------|
| `add`    | R-type   | `0x0`  | `destReg = regA + regB`                                                                                       |
| `nor`    | R-type   | `0x1`  | `destReg = ~(regA \| regB)`                                                                                   |
| `lw`     | I-type   | `0x2`  | `regB = mem[offset + regA]`                                                                                   |
| `sw`     | I-type   | `0x3`  | `mem[offset + regA] = regB`                                                                                   |
| `beq`    | I-type   | `0x4`  | `PC = (regA == regB) ? PC + 1 + offset : PC + 1`                                                              |
| `jalr`   | J-type   | `0x5`  | `regB = PC + 1`<br>`PC = regA`                                                                                |
| `halt`   | O-type   | `0x6`  | N/A                                                                                                           |
| `noop`   | O-type   | `0x7`  | N/A                                                                                                           |
| `addi`   | I-type   | `0x8`  | `regB = regA + offset`                                                                                        |
| `blt`    | I-type   | `0x9`  | `PC = (regA < regB) ? PC + 1 + offset : PC + 1`<br>NOTE: Assume values in `regA` and `regB` are signed        |
| `bltu`   | I-type   | `0xA`  | `PC = (regA < regB) ? PC + 1 + offset : PC + 1`<br>NOTE: Assume values in `regA` and `regB` are unsigned      |
| `lsr`    | J-type   | `0xB`  | `regB = regA >> 1`<br>NOTE: Assume value in `regA` is unsigned                                                |
| `asr`    | J-type   | `0xC`  | `regB = regA >> 1`<br>NOTE: Assume value in `regA` is signed                                                  |

## Assembly Language Syntax

TODO

## ABI

TODO
