# 컴파일

## cmake msvc
```console
git clone https://github.com/llvm/llvm-project.git
cd llvm-project
mkdir build 
cd build
cmake ../llvm -G "Visual Studio 17 2022" -DCMAKE_BUILD_TYPE=RelWithDebInfo -DLLVM_ENABLE_PROJECTS="clang;clang-tools-extra" ^
    -DCMAKE_GENERATOR_PLATFORM=x64 ^
    -Thost=x64 ^
    -DLLVM_DEFAULT_TARGET_TRIPLE=x86_64-pc-windows-msvc ^
    -DLLVM_INCLUDE_TESTS=OFF ^
    -DLLVM_BUILD_TOOLS=OFF ^
    -DLLVM_INCLUDE_UTILS=OFF ^
    -DLLVM_TARGETS_TO_BUILD="" ^
    -DCLANG_ENABLE_STATIC_ANALYZER=OFF ^
    -DCLANG_ENABLE_ARCMT=OFF

cmake --build . --target clang-tidy --config RelWithDebInfo
cmake --build . --target clang-query --config RelWithDebInfo
```


# clang-tidy

## new check

```console
cd llvm-project\clang-tools-extra\clang-tidy
python add_new_check.py misc my-first-check
cmake --build . --target clang-tidy --config RelWithDebInfo
clang-tidy.exe -checks=-*,misc-my-first-check testfile.cpp --
```

# 참고
[Exploring Clang Tooling](https://devblogs.microsoft.com/cppblog/exploring-clang-tooling-part-1-extending-clang-tidy/)