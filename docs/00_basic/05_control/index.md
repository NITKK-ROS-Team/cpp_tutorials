# 制御文

あらゆる事象には分岐点があります。

例えば、コイントスで表が出たら「ご飯を食べる」、裏が出たら「パンを食べる」というように、何かしらの条件によって全く異なる状況になります。

プログラムでは、このような分岐がしばしば必要になります。

ここでは、分岐や繰り返し、例外処理などの制御文について説明します。

<br>

## 条件分岐 (if文)

条件分岐は、条件によって処理を分岐させる制御文です。

条件分岐は、以下のような構文を持ちます。

以下のプログラムは、コマンドライン引数で指定した値が正か負か0かを判定します。

```cpp
#include <cstdio>
#include <cstdlib>

int main(int argc, char *argv[])
{
    // 1つめの引数を取得
    int data_a = atoi(argv[1]);

    if (data_a == 0) {
        printf("data_a is zero\n");
    } else if (data_a > 0) {
        printf("data_a is positive\n");
    } else {
        printf("data_a is negative\n");
    }
    return 0;
}
```

その前に`int argc, char *argv[]`と`atoi(argv[1])`について説明します。

`int argc, char *argv[]`は、コマンドライン引数を受け取るための変数です。

`argc`は、コマンドライン引数の数を表します。引数が1つのみであれば、`argc`は1になります。

`argv`は、コマンドライン引数の配列です。`argv[0]`は、実行ファイルのパスです。`argv[1]`は、1つ目の引数です。

`atoi(argv[1])`は、文字列を整数に変換する関数です。

つまり、このプログラムは、コマンドライン引数で入力された値が`argv[1]`に格納されてその条件を分岐することができます。

<br>

格納された値が0の場合、`data_a == 0`が成り立ち、`printf("data_a is zero\n");`が実行されます。

格納された値が0より大きい場合、`data_a > 0`が成り立ち、`printf("data_a is positive\n");`が実行されます。

格納された値が0より小さい場合、`data_a < 0`が成り立ち、`printf("data_a is negative\n");`が実行されます。

<br>

実行方法は以下の通りです。

```bash
g++ if.cpp -o if_exec
./if_exec 1
```

結果は以下の通りです。

```bash
data_a is positive
```

<br>

しかし、現在のプログラムでは、コマンドライン引数が1つでない場合にエラーが発生します。

当然ですが、コマンドライン引数が1つもない場合には、`argv[1]`が存在しないため、エラーが発生します。

そのため、以下のように、コマンドライン引数が1つでない場合には、エラーを出力するようにプログラムを修正します。

```cpp
#include <cstdio>
#include <cstdlib>

int main(int argc, char *argv[])
{
    // コマンドライン引数が1つでない場合はエラーを出力
    if (argc != 2) {
        printf("error: invalid number of arguments\n");
        return 1;
    }

    // 1つめの引数を取得
    int data_a = atoi(argv[1]);

    if (data_a == 0) {
        printf("data_a is zero\n");
    } else if (data_a > 0) {
        printf("data_a is positive\n");
    } else {
        printf("data_a is negative\n");
    }
    return 0;
}
```

条件式で、`argc != 2`とすることで、コマンドライン引数が2つでない（引数は1でない）場合に、`printf("error: invalid number of arguments\n");`が実行されて、エラー終了します。

`return 1`は、プログラミングでは、エラー終了を表すためによく使われます。

<br>

## 条件分岐 (switch文)

switch文は、値を比較して、条件に合う処理を実行する制御文です。

if文よりも、条件が多い場合に、プログラムが簡潔になります。

ここでは、引数に応じて、処理を分岐するプログラムを作成します。

```cpp
#include <cstdio>
#include <cstdlib>

int main(int argc, char *argv[])
{
    // コマンドライン引数が1つでない場合はエラーを出力
    if (argc != 2) {
        printf("error: invalid number of arguments\n");
        return 1;
    }

    // 1つめの引数を取得
    int data_a = atoi(argv[1]);

    switch (data_a) {
        case 0:
            printf("data_a is zero\n");
            break;
        case 1:
            printf("data_a is one\n");
            break;
        case 2:
            printf("data_a is two\n");
            break;
        default:
            printf("data_a is other\n");
            break;
    }
    return 0;
}
```

`switch (data_a)`の部分で、`data_a`の値を比較します。

`case 0:`の部分で、`data_a`が0の場合に、`printf("data_a is zero\n");`が実行されます。

`case 1:`の部分で、`data_a`が1の場合に、`printf("data_a is one\n");`が実行されます。

`case 2:`の部分で、`data_a`が2の場合に、`printf("data_a is two\n");`が実行されます。

`default:`の部分で、`data_a`が0, 1, 2以外の場合に、`printf("data_a is other\n");`が実行されます。

<br>

switch文では、`break`を忘れないようにしましょう。

これがないと、次のcaseに進んでしまいます。

また、switchの中で、変数を宣言することもできます。

ただし、caseの中で、変数を宣言すると、caseの外では、その変数を使用することができません。

```cpp
#include <cstdio>
#include <cstdlib>

int main(int argc, char *argv[])
{
    // コマンドライン引数が1つでない場合はエラーを出力
    if (argc != 2) {
        printf("error: invalid number of arguments\n");
        return 1;
    }

    // 1つめの引数を取得
    int data_a = atoi(argv[1]);

    switch (data_a) {
        case 0: {
            int data_b = 0;
            printf("data_a is zero\n");
            printf("data_b is %d\n", data_b);
            break;
        }
        case 1: {
            int data_b = 1;
            printf("data_a is one\n");
            printf("data_b is %d\n", data_b);
            break;
        }
        case 2: {
            int data_b = 2;
            printf("data_a is two\n");
            printf("data_b is %d\n", data_b);
            break;
        }
        default: {
            int data_b = 3;
            printf("data_a is other\n");
            printf("data_b is %d\n", data_b);
            break;
        }
    }
    return 0;
}
```

<br>

## 繰り返し (for文)

繰り返しは、条件が成り立つ限り、処理を繰り返す制御文です。

全く同じプログラムを10回繰り返すよりも、1回の処理を10回繰り返す方が、ミスや手間が減ります。

ここでは、値の出力を10回繰り返すプログラムを作成します。

```cpp
#include <cstdio>

int main()
{
    for (int i = 0; i < 10; i++) {
        printf("i = %d\n", i);
    }
    return 0;
}
```

`for (int i = 0; i < 10; i++)`は、`i`が0から始まり、10未満の間、`i`を1ずつ増やしながら、繰り返す制御文です。

`printf("i = %d\n", i);`は、`i`の値を出力するプログラムです。

<br>

実行方法は以下の通りです。

```bash
g++ for.cpp -o for_exec
./for_exec
```

結果は以下の通りです。

```bash
i = 0
i = 1
i = 2
i = 3
i = 4
i = 5
i = 6
i = 7
i = 8
i = 9
```

iが10にならないのは、`i < 10`となっているためです。詳しくは04_operatorを確認してください。

<br>

## 繰り返し (while文)

`for`文は、指定された回数だけ繰り返す制御文です。

一方で`while`文は、条件が成り立つ限り繰り返す制御文です。

そのため、whileでは「条件を満たすまで実行」という意味合いで使用されることが多いです。

<br>

以下のプログラムは、`data_a`が0になるまで、`data_a`を2で割り続けるプログラムです。

```cpp
#include <cstdio>

int main()
{
    int data_a = 100;
    while (data_a > 0) {
        data_a /= 2;
        printf("data_a = %d\n", data_a);
    }
    return 0;
}
```

`data_a`が0になるまで、`data_a`を2で割り続けるために、`data_a /= 2`としています。

ちなみに、int型で指定された変数は、小数点以下は切り捨てられます。

0.9は0になるので注意です。

<br>

実行方法は以下の通りです。

```bash
g++ while.cpp -o while_exec
./while_exec
```

結果は以下の通りです。

```bash
data_a = 50
data_a = 25
data_a = 12
data_a = 6
data_a = 3
data_a = 1
data_a = 0
```

<br>

## 繰り返し (do-while文)

`while`文は、条件が成り立つ限り繰り返す制御文です。

一方で`do-while`文は、条件が成り立つ限り繰り返す制御文ですが、`while`文と違い、最初に1回は処理を実行します。

そのため、whileと異なり、必ず1回は処理を実行することが保証されます。

<br>

## while(1)

`while(1)`は、無限ループを表す制御文です。

中断する術がないため、無限ループは、プログラムが終了しなくなります。

Linuxでは、Ctrl + Cで強制終了できます。

<br>

以下に、無限ループのプログラムを示します。

```cpp
#include <cstdio>

int main()
{
    while (1) {
        printf("Hello World\n");
    }
    return 1;
}
```

<br>

## break

`break`は、繰り返し処理を中断する制御文です。

<br>

以下のプログラムは、`data_a`が0になるまで、`data_a`を2で割り続けるプログラムです。

ただし、`data_a`が10になったら、繰り返し処理を中断します。

```cpp
#include <cstdio>

int main()
{
    int data_a = 100;
    while (data_a > 0) {
        data_a /= 2;
        printf("data_a = %d\n", data_a);
        if (data_a <= 10) {
            printf("break!\n");
            break;
        }
    }
    return 0;
}
```

<br>

実行方法は以下の通りです。

```bash
g++ break.cpp -o break_exec
./break_exec
```

結果は以下の通りです。

```bash
data_a = 50
data_a = 25
data_a = 12
data_a = 6
break!
```

breakでは、最も内側の繰り返し処理を中断します。

<br>

## continue

`continue`は、繰り返し処理を中断し、次の繰り返し処理を実行する制御文です。

breakと異なり、最も内側の繰り返し処理を中断しますが、次の繰り返し処理を実行します。

<br>

以下のプログラムは、`data_a`が0になるまで、`data_a`を2で割り続けるプログラムです。

途中までcontinueで出力をスキップさせてみます。

```cpp
#include <cstdio>

int main()
{
    int data_a = 100;
    while (data_a > 0) {
        data_a /= 2;
        if (data_a > 10) {
            continue;
        }
        printf("data_a = %d\n", data_a);
    }
    return 0;
}
```

<br>

実行方法は以下の通りです。

```bash
g++ continue.cpp -o continue_exec
./continue_exec
```

結果は以下の通りです。

```bash
data_a = 6
data_a = 3
data_a = 1
data_a = 0
```

<br>

## 課題