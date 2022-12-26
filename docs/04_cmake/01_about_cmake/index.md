# CMake

## CMakeとは

CMakeはプロジェクト単位でビルドできるツールです。

gccでは抱えきれない多くのオプションや、複数のソースファイルをまとめてビルドする必要がある場合に、CMakeを使うと便利です。

CMakeは、Makefileを生成するためのCMakeLists.txtというファイルを書くことで、プロジェクトをビルドできます。

<br>

## CMakeのインストール

CMakeは、以下のコマンドでインストールできます。

```bash
sudo apt install cmake
cmake --version
# cmake version 3.16.3
```

ビルドについては[こちらのURL](https://cmake.org/install/)に従ってください。

<br>

## CMakeLists.txt

CMakeLists.txtは、CMakeの設定ファイルです。

CMakeLists.txtは、プロジェクトの名前や、ソースファイルのパスを指定することで、プロジェクトをビルドできます。

最もシンプルなCMakeLists.txtは以下のようになります。

```cmake
add_executable(main main.cpp)
```

このCMakeLists.txtは、`main.cpp`をビルドして、`main`という名前の実行ファイルを生成します。

以下のスクリプトを空ファイル上で行ってください。

```bash
mkdir test_cpp
cd test_cpp

# create source file
echo "#include <cstdio>" > main.cpp
echo "int main(void) { printf(\"Hello World\n\"); return 0; }" >> main.cpp
echo "add_executable(main main.cpp)" > CMakeLists.txt

# create build dir
mkdir build
cd build

# cmake
cmake ..
make

# execute
./main
```

実行すると、`Hello World`と表示されます。

<br>

## ファイル構造

さて、このディレクトリの構造を見てみましょう。

プロジェクトのルートディレクトリにはもちろん、`main.cpp`と`CMakeLists.txt`があります。

そのほかにも、`build`というディレクトリがあります。

これはビルドに使用したキャッシュや、実行ファイルが生成されています。


```bash
example:~/test_cpp$ tree 
.
├── build
│   ├── CMakeCache.txt
│   ├── CMakeFiles
│   │   ├── 3.16.3
│   │   │   ├── CMakeCCompiler.cmake
│   │   │   ├── CMakeCXXCompiler.cmake
│   │   │   ├── CMakeDetermineCompilerABI_C.bin
│   │   │   ├── CMakeDetermineCompilerABI_CXX.bin
│   │   │   ├── CMakeSystem.cmake
│   │   │   ├── CompilerIdC
│   │   │   │   ├── a.out
│   │   │   │   ├── CMakeCCompilerId.c
│   │   │   │   └── tmp
│   │   │   └── CompilerIdCXX
│   │   │       ├── a.out
│   │   │       ├── CMakeCXXCompilerId.cpp
│   │   │       └── tmp
│   │   ├── cmake.check_cache
│   │   ├── CMakeDirectoryInformation.cmake
│   │   ├── CMakeOutput.log
│   │   ├── CMakeTmp
│   │   ├── main.dir
│   │   │   ├── build.make
│   │   │   ├── cmake_clean.cmake
│   │   │   ├── CXX.includecache
│   │   │   ├── DependInfo.cmake
│   │   │   ├── depend.internal
│   │   │   ├── depend.make
│   │   │   ├── flags.make
│   │   │   ├── link.txt
│   │   │   ├── main.cpp.o
│   │   │   └── progress.make
│   │   ├── Makefile2
│   │   ├── Makefile.cmake
│   │   ├── progress.marks
│   │   └── TargetDirectories.txt
│   ├── cmake_install.cmake
│   ├── main
│   └── Makefile
├── CMakeLists.txt
└── main.cpp

9 directories, 32 files
```

<br>

## キャッシュの消去

キャッシュを消去するには、`build`ディレクトリを削除して、再度ビルドを行います。

```bash
rm -rf build
```

<br>

