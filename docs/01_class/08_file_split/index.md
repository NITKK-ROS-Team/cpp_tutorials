# ファイル分割

Classの実装と実態を分けることができます。ここではヘッダーとソースファイルを分けてみます。

C++でライブラリを作成する際は、ヘッダーとソースファイルを分けることが多いです。

ヘッダーでは定義のみを書いて、ソースファイルでは実装を書くことで役割を明確にできて、コードの可読性が上がります。

また、ソースコードは先にコンパイルしておいて、ヘッダーをインクルードすることで、コンパイル時間を短縮できます。

<br>

## ヘッダー

ヘッダーは、`*.h`または`*.hpp`という拡張子を使います。ここでは`human.hpp`という名前で作成します。


ヘッダーは、`#pragma once`というプリプロセッサを使って、二重インクルードを防ぎます。

これはインクルードガードとも呼ばれます。かつてはヘッダーファイル名を使用して書かれていました。

```cpp
#pragma once

class Human {
public:
    Human();
    virtual void greet();
};
```

<br>

## ソースファイル

ソースファイル側では、ヘッダーをインクルードします。

`human.hpp`をインクルードします。

```cpp
#include "human.hpp"

Human::Human()
{
}

void Human::greet()
{
    printf("Hello\n");
}

int main()
{
    Human human;
    human.greet();
}
```

<br>

## 実行結果

```bash
Hello
```

<br>

## オーバーライドとファイル分割

ファイル分割ができると、同じヘッダーファイルの定義を用いたオーバーライドができます。

オーバーライドについては、[05_virtual_function](../05_virtual_function/index.md)を参照してください。

**burger.hpp**

```cpp
#pragma once
#include "human.hpp"

class Burger : public Human {
public:
    Burger();
    void greet() override;
};
```

```cpp
#include "burger.hpp"

Burger::Burger()
{
}

void Burger::greet()
{
    printf("Hello, how are you?\n");
    print("I'll suggest you a cheese burger!\n");
}

int main()
{
    Burger burger;
    burger.greet();
}
```

<br>
