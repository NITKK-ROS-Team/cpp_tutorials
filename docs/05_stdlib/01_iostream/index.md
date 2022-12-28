# iostream

iostreamは、C++の標準ライブラリの一部です。

主に、標準入出力を行うためのクラスを提供しています。

## 標準出力

標準出力を行うためのクラスは、`std::cout`です。

`std::cout`は、`std::ostream`クラスのオブジェクトです。

`std::basic_ostream`クラスは、`<<`演算子をオーバーロードしているため、`<<`演算子を用いて標準出力を行うことができます。

"\n"を出力するには、`std::endl`を用います。


```cpp
#include <iostream>

int main()
{
    std::cout << "Hello, world!" << std::endl;
    return 0;
}
```

### コンパイル

g++を用いてコンパイルします。gccの場合は、`-lstdc++`オプションを付けてください。

<br>

## 標準入力

標準入力を行うためのクラスは、`std::cin`です。

`std::cin`は、`std::istream`クラスのオブジェクトです。

`std::basic_istream`クラスは、`>>`演算子をオーバーロードしているため、`>>`演算子を用いて標準入力を行うことができます。

入力待ちにもなります。

```cpp
#include <iostream>

int main()
{
    int a;
    std::cin >> a;
    // 入力された値を出力
    std::cout << "a = " << a << std::endl;
    return 0;
}
```

<br>

## 標準エラー出力

標準エラー出力を行うためのクラスは、`std::cerr`です。

標準入力標準エラー出力は、`std::clog`です。


```cpp
#include <iostream>

int main()
{
    std::clog << "Hello, world!" << std::endl;
    std::cerr << "Error!" << std::endl;
    return 0;
}
```

<br>

## iostreamヘッダ

iostreamはそれ自体が`string`や`cstdio`などを内包しているため、これの宣言のみで多くの機能を使えます。

そのため、それらが省略されることがしばしばあります。

<br>
