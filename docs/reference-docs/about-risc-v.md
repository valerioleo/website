# About RISC-V
[RISC-V](https://en.wikipedia.org/wiki/RISC-V) is a minimal, modular [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture). 

## Relevance in RISC Zero
The simplicity of RISC-V as well as the maturity of the RISC-V ecosystem makes it ideal for a zero-knowledge virtual machine.
RISC Zero's [zkVM](../explainers/zkvm/zkvm_overview.md) implements the RISC-V rv32im specification, which consists of the rv32i base with the multiplication extension. 

## Documentation
The specification of rv32im is defined in [The RISC-V Instruction Set Manual, Volume I: User-Level ISA](https://riscv.org/wp-content/uploads/2019/12/riscv-spec-20191213.pdf). 
A succinct summary of the architecture is available here (TODO) 

## Suggested Reading and Videos
For more on how these ideas fit into RISC Zero's system, we recommend:
- RISC Zero's talk from zk Summit 7: [Encoding Von-Neumann Architectures in Zero-Knowledge Proof Systems](https://www.youtube.com/watch?v=od033ugtlYQ&list=PLcPzhUaCxlCgCvzkkaBWzVuHdBRsTNxj1&index=7) 
- RISC Zero Study Club: What is RISC-V and what does it have to do with RISC Zero's zkVM -- [video](https://www.youtube.com/watch?v=11DIflEwx50&list=PLcPzhUaCxlCjdhONxEYZ1dgKjZh3ZvPtl&index=5&t=1s) and [slides](https://drive.google.com/file/d/1p7E5Sgi__5_CevGKHpTwrlb0KWjSaYPU/view)