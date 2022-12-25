# 配列

配列とは、複数の値をまとめて扱うためのデータ構造です。

## 配列の宣言

配列は、`[]`を使って宣言します。

```cpp
型名 配列名[要素数];
```

実際に、整数の配列を宣言してみましょう。

```cpp
int array[10];
```

通常は全て0で初期化されます。（環境依存）

<br>

## 配列の要素へのアクセス

配列の要素にアクセスするには、`配列名[インデックス]`という形式で書きます。

```cpp
#include <cstdio>

int main(void)
{
    int array[10];
    array[0] = 1;
    array[1] = 2;
    array[2] = 3;
    array[3] = 4;
    array[4] = 5;
    array[5] = 6;
    array[6] = 7;
    array[7] = 8;
    array[8] = 9;
    array[9] = 10;

    for (int i = 0; i < 10; i++)
    {
        printf("%d, ", array[i]);
    }
    printf("\n");
}
```

<br>

## 配列の初期化

配列を宣言するときに、初期値を指定することができます。

```cpp
int array[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
```

## 配列の要素数の取得

配列の要素数を取得するには、`sizeof(配列名) / sizeof(配列の要素の型)`という形式で書きます。

```cpp
#include <cstdio>

int main(void)
{
    int array[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    printf("size = %ld\n", sizeof(array) / sizeof(int));
}
```

文字列は配列ですが、文字列の長さを取得するには、`sizeof`ではなく、`strlen`を使います。

仮に、`sizeof`を使って文字列の長さを取得しようとすると、文字列の終端を表す`'\0'`も含めた長さが取得されてしまいます。

```cpp
#include <cstdio>
#include <cstring>

int main(void)
{
    char str[] = "Hello, World!";
    printf("sizeof = %ld\n", sizeof(str));
    printf("strlen = %ld\n", strlen(str));
}
```

結果

```bash
sizeof = 14
strlen = 13
```

<br>
