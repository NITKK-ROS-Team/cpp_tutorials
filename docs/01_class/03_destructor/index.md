# デストラクタ

デストラクタはオブジェクトが破棄される時に呼び出されます。

つまり、コンストラクタの逆と言えます。

## デストラクタの定義

デストラクタはコンストラクタの名前に `~` をつけたものです。

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

    ~MyClass()
    {
        printf("MyClass is destroyed.\n");
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

`MyClass` のデストラクタは、`~MyClass` という名前のメソッドです。

`MyClass` のインスタンスが破棄される時に、`MyClass` のデストラクタが呼び出されます。

ここでは、`MyClass is destroyed.` という文字列が出力されます。

デストラクタは、明示的に呼び出すことはできませんが、明示的に破棄することはできます。

<br>

## デストラクタの引数

デストラクタには引数を渡すことはできません。

<br>

## デストラクタのオーバーロード

デストラクタは、引数を渡すことができないため、オーバーロードすることはできません。

<br>

