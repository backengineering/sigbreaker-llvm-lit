# CodeDefender - LLVM LIT

This repository provides a reproducible way to demonstrate CodeDefender’s stability and performance under extreme conditions. The binaries here are obfuscated to the absolute maximum—applying every available obfuscation feature with multiple iterations.

These binaries do not represent the typical output of our obfuscator. Instead, they showcase that even under insane levels of obfuscation, CodeDefender remains stable and performant. Every possible function within these binaries has been obfuscated to its fullest extent.

## Setup

Requirements:

- Git
- Visual Studios 2022
- cmake
- Python 3.x (> 3.8)

```sh
git clone --recursive -b tags/llvmorg-20.1.0 https://github.com/llvm/llvm-project.git
cd llvm-project
cmake -S llvm -B build \
    -DLLVM_ENABLE_PROJECTS="clang;clang-tools-extra;lld;lldb;polly;bolt;mlir;openmp" \
    -DLLVM_ENABLE_RUNTIMES="libcxx;libcxxabi;libunwind;compiler-rt" \
    -DCMAKE_BUILD_TYPE=Release

# Open build/LLVM.sln in Visual Studios 2022
```

## LLVM-LIT Tests

Each LLVM project comes with its own set of lit tests, designed to verify complex functionality and maintain backward compatibility. This is ideal for our needs, as these tests cover a vast portion of the executable paths within our obfuscated binaries. A huge thanks to LLVM for providing such extensive test coverage!

You can checkout the docs for [llvm-lit here](https://llvm.org/docs/CommandGuide/lit.html)

- https://github.com/llvm/llvm-project/tree/llvmorg-20.1.0/bolt/test
- https://github.com/llvm/llvm-project/tree/llvmorg-20.1.0/llvm/test
- https://github.com/llvm/llvm-project/tree/llvmorg-20.1.0/clang/test
- https://github.com/llvm/llvm-project/tree/llvmorg-20.1.0/lld/test

> There are tons of other tests and subtests for each project. An associate of Back Engineering Labs has worked on the llvm linker (lld) and expressed how complex their lit tests are.