# ポインタ

## メモリとは

コンピュータの記憶域の一つで、電気信号を記憶することができます。

メモリはCPUとディスクの間に位置し、CPUがディスクから情報を読み込むときに、一時的に情報を記憶するために使用されます。

メモリの広さは作業机の広さに例えられることが多く、メモリ量が多いほど一度に処理できる情報量が増加します。

<!-- TODO : 追記 -->

<br>

## ポインタとは

ポインタとは、メモリのアドレスを格納する変数です。

プログラムを動作させるときは、変数名も変数の型も関数もクラスも全てメモリのどこかにあります。

ポインタは、そのメモリのアドレスを格納する変数です。

関数が演算の時に変数を呼び出す時も、実際は変数のアドレスを呼び出しています。

<br>

## ポインタの宣言

ポインタは、`*` を変数の前につけることで宣言できます。

アドレスは`&`を変数の前につけることで取得できます。

```cpp
#include <cstdio>

int main(void)
{
    int data = 0;
    int* ptr = &data;
    printf("data pointer: %p\n", &data);
    printf("ptr pointer: %p\n", &ptr);
    return 0;
}
```

以上のコードでは、`data pointer`で`data=0`のアドレスを取得しています。

ちなみに、`int* ptr`の`*`は、`ptr`がポインタを格納していることを示していますが、これ自体も変数なので、`ptr`のアドレスを取得することができます。

<br>

関数にもポインタを渡すことができます。

これを利用して、データをコピーすることなく、関数内でデータを変更することができます。

次のコードは、dataを返り値なしで3に上書きするプログラムです。


```cpp
#include <cstdio>

void func(int* ptr)
{
    void (*this_pointer)(int*) = func;
    printf("\n---------- in function ----------\n");
    printf("func() pointer: \t%p\n", this_pointer);
    printf("pointer's pointer: \t%p\n", &ptr);
    printf("raw input pointer: \t%p\n", ptr);
    printf("input value: \t%d\n", *ptr);
    printf("---------- end of function --------\n\n");
    *ptr = 3;
}

int main(void)
{
    int data = 0;
    int* ptr = &data;

    // function pointer
    int (*main_pointer)(void) = main;
    void (*func_ptr)(int*) = func;

    printf("func() pointer: \t%p\n", func_ptr);
    printf("main pointer: \t\t%p\n", main_pointer);
    printf("data pointer: \t\t%p\n", ptr);
    

    // call function using pointer
    (*func_ptr)(ptr);

    printf("data: %d\n", data);

    return 0;
}
```

<br>

実行結果を以下に示します。（結果は実行タイミングによって全く異なります）

```bash
func() pointer:         0x55780f2d6189
main pointer:           0x55780f2d622a
data pointer:           0x7ffcadc3a15c

---------- in function ----------
func() pointer:         0x55780f2d6189
pointer's pointer:      0x7ffcadc3a128
raw input pointer:      0x7ffcadc3a15c
input value:    0
---------- end of function --------

data: 3
```

<br>

全てのプログラム・関数・クラスは、メモリ上に存在するため、アドレスを持っています。

例えば、`func()`関数のアドレスは`0x55780f2d6189`で、`main()`関数のアドレスは`0x55780f2d622a`です。

また、`data`のアドレスは`0x7ffcadc3a15c`です。

<br>

次に、`func()`に目を移してみましょう。`func`では引数にint型のポインタを渡しています。

渡されたポインタ(アドレス)をもとに直接値を上書きしています。通常は値のコピーを行うことで、値を変更することが多いですが、ポインタを使うことで、値のコピーを行わずに値を変更することができます。

> main内のポインタのポインタとfunc内のポインタのポインタは異なります。

`*ptr = 3`の`*`は、ポインタが指す値を示しています。

値の上書きを行った後、mainに戻って`data`の値を表示すると、`data: 3`となっています。

<br>

このように、ポインタを使うことで、データをコピーせずに値を変更することができます。

<br>

メモリのデータをアドレス直接指定で変更することは、バグの原因になりやすいため、基本的にはポインタを使わない方が良いです。

2.3ではスマートポインタを扱います。