---
sidebar_position: 2
slug: ./
---

# Overview of the zkVM

*To invite collaboration and open source development, this is an early-release of documentation-in-progress. 
If you have questions/feedback or if you find errors, please let us know on [Twitter](https://twitter.com/risczero) or [Discord](https://discord.gg/risczero).*

A zero-knowledge virtual machine (zkVM) is a virtual machine that runs trusted code and generates proofs that authenticate the zkVM output.  
RISC Zero's [zkVM](what_is_risc_zero.md) implementation, based on the RISC-V architecture, executes code and produces a [computational receipt](../proof-system/what_is_a_receipt.md).

This document describes, at a high level, the components involved in this process. 
After reading this, you should understand the general process of receipt creation and be familiar with the language we use to describe the zkVM's operations. 
To understand how these operations generate an argument of computational integrity, see our introduction to the [proof system](../proof-system/proof-system-sequence-diagram.md).

In a RISC Zero zkVM program, guest code written for the zkVM is compiled to an ELF binary and executed by the `prover`, which returns a computational receipt to the host program, as shown in the following Rust code snippet from the [RISC Zero Rust starter example](https://github.com/risc0/risc0-rust-starter/):

```
    let receipt = prover.run().unwrap();
```

Anyone with a copy of the receipt can verify the program's execution and read its publicly shared outputs. 
The diagram below illustrates the components involved in this process, which is described in greater detail below.

```mermaid
flowchart LR
A(multiply.rs)-->|compiles to an|B(ELF binary)
B-->|Whose execution produces an| C(Execution trace)
B-->|Whose hash forms a unique| D(Image ID)
D-->|That can be compared to the|E(Cryptographic seal)
C-->|That, if valid,<br>generates a|E(Cryptographic seal)
B-->|Whose operations can include<br>committing values to a|F(Journal)
subgraph Together, these form a receipt.
E
F
end
subgraph x[The receipt tells us:]
E---H(What binary executed in the ZKVM<br>Whether the execution<br>followed expected behavior<br/><br/>Whether the journal or image ID<br/>have changed)
F---I(The values of all contents<br>written to the public journal)
end
style B fill:#3c6464
style x fill:none, stroke:none
style H fill:none,stroke:none
style I fill:none,stroke:none
```

Before being executed on the zkVM, guest source code is converted into a RISC-V ELF binary. 
The binary file is hashed to create a `image ID` that uniquely identifies the binary being executed. 
The binary may include code instructions to publicly commit a value to the `journal`. Later, the journal contents can be read by anyone with the receipt.

After the binary is executed, an [execution trace](../proof-system/what_is_a_trace.md) contains a complete record of zkVM operation. 
The trace is inspected and the ELF file's instructions are compared to the operations that were actually performed. 
A valid trace means that the ELF file was faithfully executed according to the rules of the RISC-V instruction set architecture.

The execution trace and the journal are then used to generate a seal, a blob of cryptographic data that shows the receipt is valid. 
The seal has properties that reveal whether itself or the journal have been altered. 
When the receipt is verified, the seal will be checked to confirm the validity of the receipt. 
To check whether the correct binary was executed, the seal can be compared to the image ID of the expected ELF file.

## Video Explainer
- [How does RISC Zero work?](https://www.youtube.com/watch?v=8hwY88xJoyM&list=PLcPzhUaCxlCgig7ofeARMPwQ8vbuD6hC5&index=8)
