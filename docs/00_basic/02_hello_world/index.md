# Hello World

プログラムの最初の一歩は、Hello Worldと表示するプログラムです。

`code ./hello_world.cpp`

```cpp
#include <cstudio>

int main()
{
    printf("Hello World\n");
    return 0;
}
```

コンパイルしてみましょう。

```bash
g++ hello_world.cpp -o hello_world_exec
```

コンパイルにはC++向けのコンパイルツール `g++` を使用します。引数にはソースコードの他に、出力ファイル名を指定します。

`g++ ソースコード1 ソースコード2 ... -o 出力ファイル名`

<br>

実行してみましょう。

`hello_world_exec`はLinuxで実行可能なファイルです。


```bash
./hello_world_exec
```

出力結果は `Hello World` となります。

## 課題
