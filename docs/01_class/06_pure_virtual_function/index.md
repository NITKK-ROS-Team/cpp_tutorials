# 純粋仮想関数

純粋仮想関数は、クラスの中で宣言された仮想関数のうち、関数の実装がないものです。純粋仮想関数を含むクラスは、純粋仮想関数を実装するまでインスタンス化できません。

## 純粋仮想関数の宣言

純粋仮想関数は、関数の宣言の後に `= 0` を付けることで宣言できます。

```cpp
#include <cstdio>

class Human {
public:
    int age;
    int tone;
    char name[256];

    Human(int age, int tone, const char* name) {
        this->age = age;
        this->tone = tone;
        strcpy(this->name, name);
    }

    // 純粋仮想関数の定義
    virtual void greet() = 0;
};
```

## 純粋仮想関数の実装

純粋仮想関数を実装するには、純粋仮想関数を含むクラスを継承したクラスで、純粋仮想関数を実装する必要があります。

> 注意：何も実装しない場合でも、関数の実装を記述する必要があります。

```cpp
class Burger : public Human {
public:
    Burger(int age, int tone, const char* name) : Human(age, tone, name) {}

    void greet() override
    {
        printf("Hello, how are you?");
    }
};

int main()
{
    // Human human(20, 180, "John"); <-- Error

    // OK -------------------------
    Burger burger(20, 180, "Burger");
    burger.greet();
}
```

<br>
