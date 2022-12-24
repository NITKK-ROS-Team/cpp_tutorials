# 変数と型

プログラムにおいて、演算の対象となる値を変数と呼びます。

変数には、数値や文字列などのデータを格納することができます。これらのデータの種類を型と呼びます。

<br>

## 変数の宣言

変数を宣言するには、型と変数名を指定します。

```cpp
#include <cstdio>

int main()
{
    int data_a = 0;
    printf("data_a = %d\n", data_a);
    data_a = 1;
    printf("data_a = %d\n", data_a);
    return 0;
}
```

変数の宣言には、型と変数名を指定します。また、初期値を指定することもできます。

値の出力には、`printf` 関数を使用します。`printf` 関数は、文字列を出力します。文字列中に `%d` という文字列があると、その部分に変数の値を出力します。

例えば、上記のコードでは `data_a` という変数を宣言しています。型は `int` で、初期値は `0` です。

その後、`data_a`の値に `1` を代入しています。`printf` 関数で `data_a` の値を出力すると、`1` が出力されます。

<br>

## 型

変数の型には、数値や文字列などがあります。

現行のLinux C++の仕様を示します。

| 型 | 説明 | バイト数 | 値の範囲 | 値の出力 | 値の例 |
| --- | --- | --- | --- | --- | --- |
| `int` | 整数 | 4 | -2147483648 ~ 2147483647 | `%d` | 1 |
| `long` | 整数 | 8 | -9223372036854775808 ~ 9223372036854775807 | `%ld` | 1 |
| `long long` | 整数 | 8 | -9223372036854775808 ~ 9223372036854775807 | `%lld` | 1 |
| `float` | 浮動小数点数 | 4 | 1.17549e-38 ~ 3.40282e+38 | `%f` | 1.0 |
| `double` | 浮動小数点数 | 8 | 2.22507e-308 ~ 1.79769e+308 | `%lf` | 1.0 |
| `char` | 文字 | 1 | -128 ~ 127 | `%c` | 'a' |
| `bool` | 真偽値 | 1 | true, false | `%d` | true |

<br>

文字列は、`char` 型の配列です。`char` 型の配列は、文字列として扱うことができます。

```cpp
#include <cstdio>

int main()
{
    char data_a[] = "Hello";
    printf("data_a = %s\n", data_a);
    return 0;
}
```

`%s` で文字列を出力します。


<br>

## 型の変換

型の変換は、以下のように行います。

```cpp
#include <cstdio>

int main()
{
    int data_a = 0;
    double data_b = 1.0;
    data_a = data_b;
    printf("data_a = %d\n", data_a);
    return 0;
}
```

`data_a` は `int` 型で、`data_b` は `double` 型です。`data_a` に `data_b` を代入すると、`data_b` の型が `int` に変換されます。

これでもいいですが、明示的に型を変換することもできます。

```cpp
#include <cstdio>

int main()
{
    int data_a = 0;
    double data_b = 1.0;
    data_a = (int)data_b;
    printf("data_a = %d\n", data_a);
    return 0;
}
```

`data_b` に `(int)` を追加することで、`data_b` の型を `int` に変換できます。

当然ながら、`int` から `double` に変換することもできます。

<br>

## 型の確認

変数の型を確認するには、`typeid` を使用します。

```cpp
#include <cstdio>
#include <typeinfo>

int main()
{
    int data_i = 0;
    long data_l = 1;
    double data_d = 1.0;
    float data_f = 1.0;
    char data_s[] = "Hello";
    char data_c = 'a';
    bool data_b = true;

    printf("data_i = %s\n", typeid(data_i).name());
    printf("data_l = %s\n", typeid(data_l).name());
    printf("data_d = %s\n", typeid(data_d).name());
    printf("data_f = %s\n", typeid(data_f).name());
    printf("data_s = %s\n", typeid(data_s).name());
    printf("data_c = %s\n", typeid(data_c).name());
    printf("data_b = %s\n", typeid(data_b).name());

    return 0;
}
```

出力結果は以下のようになります。

```bash
data_i = i
data_l = l
data_d = d
data_f = f
data_s = A6_c
data_c = c
data_b = b
```

<br>

## 課題