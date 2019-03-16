Before building, you should checkout branch

## Build llvm

```bash
cd llvm && build_llvm.sh
```

## Build Hikari-llvm

```bash
cd hikari && build_llvm.sh
```

## Build Obfuscator-llvm

```bash
cd obfuscator && build_llvm.sh
```

### build_llvm.sh

```bash
#!/bin/bash
set -e

mkdir build && cd build

output=/tmp/llvm-build

cmake -DCMAKE_INSTALL_PREFIX=${output} \
      -DCMAKE_BUILD_TYPE=Release \
      -DLLVM_INCLUDE_TESTS=Off \
      -DLLVM_INCLUDE_EXAMPLES=Off \
      -DLLVM_ENABLE_LIBCXX=ON \
      -DLLVM_ENABLE_CXX1Y=ON \
      -DLLVM_ENABLE_PROJECTS="clang;clang-tools-extra;libcxx;libcxxabi;compiler-rt;libunwind;polly;lld" \
      -DLLVM_CREATE_XCODE_TOOLCHAIN=ON \
      -GNinja \
      ..

ninja
ninja install-xcode-toolchain

echo build finish.
echo toolchain installed at ${output}
```
