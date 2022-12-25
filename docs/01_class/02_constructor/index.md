# コンストラクタ

## コンストラクタとは

コンストラクタとは、インスタンスを生成する際に呼び出されるメソッドのことです。

<br>

## コンストラクタの定義

コンストラクタは、クラス名と同じ名前のメソッドを定義することで定義できます。

```cpp
#include <cstdio>

class MyClass
{
public:
    MyClass()
    {
        data_a = 0;
        data_b = 1.0;
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
    my_class.print();
}
```

`MyClass` のコンストラクタは、`MyClass` と同じ名前のメソッドです。

必ず、`MyClass` のコンストラクタは、`MyClass` のインスタンスを生成する際に呼び出されます。

そのため、`my_class`に続いて`my_class_1`というインスタンスを生成すると、`MyClass` のコンストラクタがそれぞれ呼び出されます。

<br>

## コンストラクタの引数

コンストラクタには、引数を渡すことができます。

```cpp
#include <cstdio>

class MyClass
{
public:
    MyClass(int a, double b)
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
    MyClass my_class(0, 1.0);
    my_class.print();
}
```

`MyClass` のコンストラクタには、`int` 型の変数 `a` と `double` 型の変数 `b` を引数として渡しています。

`MyClass` のコンストラクタは、`MyClass` のインスタンスを生成する際に、`int` 型の変数 `a` と `double` 型の変数 `b` を受け取ります。

<br>
