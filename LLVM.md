# What is an LLVM?  

LLVM is a modular **compiler infrastructure** and toolchain project, not a
traditional virtual machine or a single compiler. Originally standing for "Low
Level Virtual Machine," the name is now an orphan initialism representing the
entire ecosystem of reusable compiler technologies developed starting in 2000 at
the University of Illinois.

## Core Function: Intermediate Representation

The central concept of LLVM is the **Intermediate Representation (IR)**. Instead
of compiling source code directly to machine code, LLVM translates code into
this language-independent, architecture-neutral format. This IR serves as a "
portable high-level assembly" that can be optimized and then translated into
machine code for any target hardware (such as x86, ARM, or GPUs) by LLVM's
backend.

## Key Components

* **Frontends:** These translate source code (like C, C++, or Rust) into LLVM
  IR. The most famous frontend is **Clang**, which is the standard compiler for
  C, C++, and Objective-C on macOS and iOS.
* **Optimizers:** LLVM provides a powerful pipeline of optimization passes that
  analyze and improve the IR for performance, size, and efficiency.
* **Backends:** These translate the optimized IR into specific machine code for
  different processors.

## Common Uses

LLVM is the backbone for many modern programming languages and tools:

* **Clang:** The C/C++ compiler used by Apple.
* **Rust:** The Rust programming language uses LLVM for code generation.
* **Swift:** Apple's Swift language relies on LLVM for compilation.
* **JIT Compilation:** Languages like **Julia** and **Numba** (Python) use LLVM
  to compile code at runtime for high performance.
* **WebAssembly:** LLVM is used to compile code to WebAssembly, enabling
  languages like Rust to run in web browsers.

## LLVM vs. GCC

While **GCC** (GNU Compiler Collection) is a traditional compiler suite with
tightly coupled frontends and backends, **LLVM** is designed as a library and
framework. This modularity allows developers to build custom compilers,
language-specific tools, and JIT compilers more easily than with GCC.
