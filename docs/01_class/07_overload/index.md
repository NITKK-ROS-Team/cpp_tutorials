# オーバーロード

## オーバーロードとは

オーバーロードとは、同じ名前の関数やメソッドを複数定義することです。

オーバーロードとは「ライド（乗る）」の意味で、オーバーライドとは「ライド（乗せる）」の意味で区別できます。

## オーバーロードの例

```cpp
#include <cstdio>

class Human {
public:

    Human() = default;

    // オーバーロードの例
    void greet()
    {
        printf("Hello\n");
    }

    void greet(const char* name)
    {
        printf("Hello, I'm %s. I'm %d years old.\n", name, age);
    }

    void greet(const char* name, int age)
    {
        printf("Hello, I'm %s. I'm %d years old.\n", name, age);
    }
};

int main()
{
    Human human;
    human.greet();
    human.greet("Taro");
    human.greet("Taro", 20);
}
```

実行結果

```bash
Hello.
Hello, I'm Taro.
Hello, I'm Taro. I'm 20 years old.
```

<br>

## オーバーロードの注意点

オーバーロードを使用する場合、以下の点に注意する必要があります。

- オーバーロードする関数やメソッドの引数の数が異なる
- オーバーロードする関数やメソッドの引数の型が異なる
- オーバーロードする関数やメソッドの引数の順番が異なる

オーバーライドで定義する場合は、最初から全て用意しておく必要があります。

異なる型で同じパターンを定義する場合は、templateを使用する必要があります。

<br>

