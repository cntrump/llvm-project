Before building, you should checkout branch

## Build llvm

```bash
cd llvm && build_llvm.sh
```

## Build [Hikari-llvm](https://github.com/HikariObfuscator/Hikari)

Read the [code-signing.txt](https://github.com/llvm-mirror/lldb/blob/master/docs/code-signing.txt) first.

```bash
cd hikari && build_llvm.sh
```

## Build [Obfuscator-llvm](https://github.com/heroims/obfuscator) (heroims's fork)

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
      -DLLDB_CODESIGN_IDENTITY='' \
      -DLLVM_ENABLE_PROJECTS="clang;clang-tools-extra;libcxx;libcxxabi;compiler-rt;libunwind;polly;lld" \
      -DLLVM_CREATE_XCODE_TOOLCHAIN=ON \
      -GNinja \
      ..

ninja
ninja install-xcode-toolchain

echo build finish.
echo toolchain installed at ${output}
```
