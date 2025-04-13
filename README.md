# CodeDefender - LLVM LIT

This repository offers a reproducible setup for evaluating CodeDefender’s stability and performance across various scenarios. Each ZIP archive includes a distinct set of binaries tailored for specific testing conditions:

- `original.zip` contains the original llvm compiled binaries for `clang` and `lld` lit tests
- `rewrite.zip` contains rewritten binaries (no obfuscation)
- `recompiled.zip` contains recompiled binaries (no obfuscation)
- `sigbreaker-1.0.zip` contains `SigBreaker 1.0` scrambled binaries

## Setup

Requirements:

- Git
- Visual Studios 2022
- cmake
- Python 3.x (> 3.8)

### Run Tests

```sh
# Run this in a powershell!
git clone --recursive -b llvmorg-20.1.0 https://github.com/llvm/llvm-project.git
cd llvm-project
cmake -S llvm -B build \
    -DLLVM_ENABLE_PROJECTS="clang;clang-tools-extra;lld;lldb;polly;bolt;mlir;openmp" \
    -DLLVM_ENABLE_RUNTIMES="libcxx;libcxxabi;libunwind;compiler-rt" \
    -DCMAKE_BUILD_TYPE=Release

# Unzip the original binaries into the build folder
Expand-Archive -Path "../original.zip" -DestinationPath "./build/Release/bin/" -Force
cd "./build/Release/bin/"

#
# Run the original binaries to get baseline test results
#

# Run clang lit tests
python llvm-lit.py ../../../clang/test/ > original-clang-lit-results.txt
# Run lld lit tests
python llvm-lit.py ../../../lld/test/ > original-lld-lit-results.txt
```

## LLVM-LIT Tests

Each LLVM project comes with its own set of lit tests, designed to verify complex functionality and maintain backward compatibility. This is ideal for our needs, as these tests cover a vast portion of the executable paths within our obfuscated binaries. A huge thanks to LLVM for providing such extensive test coverage!

You can checkout the docs for [llvm-lit here](https://llvm.org/docs/CommandGuide/lit.html)

- https://github.com/llvm/llvm-project/tree/llvmorg-20.1.0/llvm/test
- https://github.com/llvm/llvm-project/tree/llvmorg-20.1.0/clang/test
- https://github.com/llvm/llvm-project/tree/llvmorg-20.1.0/lld/test

> There are tons of other tests and subtests for each project. An associate of Back Engineering Labs has worked on the llvm linker (lld) and expressed how complex their lit tests are. You can explore the ELF tests here: https://github.com/llvm/llvm-project/tree/llvmorg-20.1.0/lld/test/ELF
