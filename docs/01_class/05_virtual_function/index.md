# 仮想関数

仮想関数（virtual function）は、基底クラスで定義された関数を、派生クラスで再定義することです。

仮想関数を使用するには、基底クラスで仮想関数を定義する必要があります。

仮想関数を定義するには、仮想関数を定義する前に「virtual」というキーワードを使用します。

例えば、次のように基底クラスで仮想関数を定義することができます


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

    // 仮想関数の定義
    virtual void greet()
    {
        printf("Hello, I'm %s. I'm %d years old.\n", name, age);
    }
};

```

仮想関数を使用することで、基底クラスで定義された関数を、派生クラスで再定義することができます。

派生クラスで仮想関数を再定義する場合、「override」というキーワードを使用することで、明示的に仮想関数を再定義することができます。

これにより、基底クラスのインタフェースを維持しつつ、派生クラスで独自の振る舞いを実装することができます。

Burgerであれば、そもそも名前と年齢を言う必要がないので、greet()を再定義することで、名前と年齢を言わないようにすることにしましょう。


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
    Human human(20, 180, "Taro");
    human.greet();

    Burger burger(20, 180, "Taro");
    burger.greet();
}
```

実行結果

```bash
Hello, I'm Taro. I'm 20 years old.
Hello, how are you?
```

<br>
