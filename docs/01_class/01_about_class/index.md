# クラス (Class)

## クラスとは

クラスとは、オブジェクトを作成するための設計図のようなものです。

クラスを使うことで、同じようなオブジェクトを複数作成することができます。

## クラスの定義

クラスは、`class`キーワードを使って定義します。

```cpp
#include <cstdio>

class MyClass
{
public:
    int data_a;
    double data_b;
};

int main()
{
    MyClass my_class;
    my_class.data_a = 0;
    my_class.data_b = 1.0;
    printf("data_a = %d\n", my_class.data_a);
    printf("data_b = %f\n", my_class.data_b);
    return 0;
}
```

`class MyClass` でクラスを定義しています。

- `MyClass` はクラスの名前です。
- `data_a` と `data_b` はクラスのメンバ変数です。
    - `public` はアクセス修飾子です。 クラスの外部からアクセスできることを示しています。
- `data_a` と `data_b` はそれぞれ、`int` 型と `double` 型の変数です。

## 複製

クラスを使うと、同じようなオブジェクトを複製することができます。

```cpp
#include <cstdio>

class MyClass
{
public:
    int data_a;
    double data_b;
};

int main()
{
    MyClass my_class_a;
    my_class_a.data_a = 0;
    my_class_a.data_b = 1.0;
    printf("data_a = %d\n", my_class_a.data_a);
    printf("data_b = %f\n", my_class_a.data_b);

    MyClass my_class_b;
    my_class_b.data_a = 2;
    my_class_b.data_b = 3.0;
    printf("data_a = %d\n", my_class_b.data_a);
    printf("data_b = %f\n", my_class_b.data_b);

    return 0;
}
```

`my_class_a` と `my_class_b` は、`MyClass` というクラスから作成されたオブジェクトで、形は全く同じです。

`MyClass`自体はクッキーの型のようなもので、`my_class_a` と `my_class_b` はクッキーの型から作られたクッキーのようなものです。

<br>

## メンバ関数

クラスには、メンバ変数だけでなく、メンバ関数も定義できます。

メソッドとも呼ばれます。

```cpp
#include <cstdio>

class MyClass
{
public:
    void init(int a, double b)
    {
        data_a = a;
        data_b = b;
    }

    void print()
    {
        printf("data_a = %d\n", data_a);
        printf("data_b = %f\n", data_b);
    }
private:
    int data_a;
    double data_b;
};

int main()
{
    MyClass my_class;
    my_class.init(0, 1.0);
    my_class.print();
    return 0;
}
```

MyClassの中に、`init` と `print` というメンバ関数を定義しています。

- `init` は、`data_a` と `data_b` に値を代入するメンバ関数です。
- `print` は、`data_a` と `data_b` の値を表示するメンバ関数です。

`init` と `print` は、`MyClass` のメンバ関数なので、`my_class` から呼び出すことができます。

<br>

また、ここでは、`data_a` と `data_b` を `private` にしています。

これにより、`data_a` と `data_b` は `MyClass` の外部からアクセスできなくなります。

試しに、`main` の中で `my_class.data_a = 0;` というコードを追加してみてください。

コンパイルエラーが発生するはずです。

```cpp
...
    my_class.init(0, 1.0);
    my_class.print();
    my_class.data_a = 0; // コンパイルエラー
    return 0;
}
```

Classはライブラリとして外部からインクルード可能にするため、メンバ変数は基本的に `private` にして関数を使ってアクセスすると、可読性が高くなります。

<br>
