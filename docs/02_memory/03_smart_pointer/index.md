# スマートポインタ

スマートポインタは、ポインタのメモリ管理を自動化するための仕組みです。

先ほどのプログラムであれば、まだシンプルなので、どのコードが発端でエラーになっているかがわかりますが、実際のプログラムでは、どのコードが発端でエラーになっているかがわかりにくくなります。

さらに厄介なのは、動的メモリというのは確保する量が可変するため、「たまにエラーになる」という再現に困るエラーが出現する可能性があるのです、

<br>

スマートポインタは「所有権」を割り当てて動的メモリを管理することで、このような問題を解決します。

スマートポインタはC++11から導入された機能で、`memory`ヘッダに含まれています。

<br>

## std::unique_ptr

`std::unique_ptr`は、ポインタの所有権を割り当てるためのスマートポインタです。

"unique"という名前の通り、所有権は一つだけです。

```cpp
#include <cstdio>
#include <memory>

int main() {
    std::unique_ptr<int> p(new int(42));
    printf("@%p: %d\n", p.get(), *p);

    return 0;
}

```

スマートポインタにdeleteは要りません。勝手に解放してくれます。

2.1のプログラムをスマートポインタのunique_ptrを使って書き直すと以下のようになります。

```cpp
#include <cstdio>
#include <memory>

void func(std::unique_ptr<int> p) {
    printf("@%p: %d\n", p.get(), *p);
    // 3を代入
    *p = 3;
    // ここで解放される
}

int main() {
    std::unique_ptr<int> p(new int(42));
    printf("@%p: %d\n", p.get(), *p);
    func(std::move(p));
    // ここで解放される
    printf("@%p: %d\n", p.get(), *p); // ここでエラー
    return 0;
}
```

unique_ptrは、所有権を共有することはできず、`std::move`を使って所有権を移動する必要があります。

std::moveによって移動した後は、移動元の所有権がなくなり、アクセスができなくなります。

移動先でしか使用できないため、これまでのメモリ管理の中では安全と言えるでしょう。

<br>

### 実行結果

所有権が移動してしまい、`func()`の終了時点で解放されてしまうため、`main()`の中で`p`を使おうとするとエラーになります。

```bash
@0x557f4929deb0: 42
@0x557f4929deb0: 42
Segmentation fault (core dumped)
```

<br>

## std::shared_ptr

`std::shared_ptr`は、ポインタの所有権を共有するためのスマートポインタです。

"shared"という名前の通り、所有権は複数の所有を認めています。

```cpp
#include <cstdio>
#include <memory>

void func(std::shared_ptr<int> p) {
    printf("@%p: %d\n", p.get(), *p);
    // 3を代入
    *p = 3;
    // ここで解放される
}

int main() {
    std::shared_ptr<int> p(new int(42));
    printf("@%p: %d\n", p.get(), *p);
    func(p);
    // ここで解放される
    printf("@%p: %d\n", p.get(), *p); // OK!
    return 0;
}
```

<br>

### 実行結果

`func()`の終了時点で解放されることはなく、`main()`の中で`p`を使うことができます。

ただし、`p`の所有権を共有しているため、`p`の所有権を持つ変数がなくなるまで、解放されません。

```bash
@0x562742cdceb0: 42
@0x562742cdceb0: 42
@0x562742cdceb0: 3
```

これまでの生ポインタと同じような挙動になります。

<br>

shard_ptrは内部で所有者数をカウントアップ・ダウンしており、0になった時点で解放されます。

p.reset()を使うと、所有権を明示的に解放することができます。

```cpp
#include <cstdio>
#include <memory>

void func(std::shared_ptr<int> p) {
    printf("@%p: %d\n", p.get(), *p);
    // 3を代入
    *p = 3;
}

int main() {
    std::shared_ptr<int> p(new int(42));
    printf("@%p: %d\n", p.get(), *p);
    func(p);
    // 明示的に解放する
    p.reset();
    printf("@%p: %d\n", p.get(), *p); // ここでエラー

    return 0;
}
```

<br>

## weak_ptr

`std::weak_ptr`は、所有権を持たないスマートポインタです。

先ほどの「shared_ptrは所有権を共有するため、所有権を持つ変数がなくなるまで解放されない」という特徴が悪さをして、循環参照が発生してしまうことがあります。

循環参照とは、オブジェクトAがオブジェクトBを参照し、オブジェクトBがオブジェクトAを参照し続けることで、オブジェクトAとオブジェクトBが解放されなくなることです。

これはメモリリークにつながります。

<br>

まずは正常終了する例から。片方だけだとすぐに終了してくれます。

```cpp
#include <cstdio>
#include <memory>

class ClassA
{
public:
    std::shared_ptr<ClassA> ptr;

    ClassA(){ printf("Start\n"); }
    ~ClassA() { printf("End\n"); }
};


int main()
{
    {
        std::shared_ptr<ClassA> ptr1 = std::make_shared<ClassA>();
        std::shared_ptr<ClassA> ptr2 = std::make_shared<ClassA>();

        ptr1->ptr = ptr2;
        // ptr2->ptr = ptr1;
    }
    getchar();

    return 0;
}
```

<br>

### 実行結果

```bash
Start
Start
End
End
```

<br>

次は、先ほどの`ptr2->ptr = ptr1;`のコメントアウトを外して実行してみます。

```cpp
...

int main()
{
    {
        std::shared_ptr<ClassA> ptr1 = std::make_shared<ClassA>();
        std::shared_ptr<ClassA> ptr2 = std::make_shared<ClassA>();

        ptr1->ptr = ptr2;
        ptr2->ptr = ptr1;
    }
    getchar();

    return 0;
}
```

<br>

### 実行結果

```bash
Start
Start
```

このようにいつまでもリソースを解放することはありません。

ループがなければこれでも問題ないのですが、ループがあると永遠にメモリを消費し続けます。

<br>

### 解決策

`std::weak_ptr`を使うことで、循環参照を防ぐことができます。

```cpp
#include <cstdio>
#include <memory>

class ClassA
{
public:
    std::weak_ptr<ClassA> ptr;

    ClassA(){ printf("Start\n"); }
    ~ClassA() { printf("End\n"); }
};

int main()
{
    {
        std::shared_ptr<ClassA> ptr1 = std::make_shared<ClassA>();
        std::shared_ptr<ClassA> ptr2 = std::make_shared<ClassA>();

        ptr1->ptr = ptr2;
        ptr2->ptr = ptr1;
    }
    getchar();

    return 0;
}
```

<br>

### 実行結果

インスタンスが互いに所有することはないので、循環参照は防げました。

ただし、所有権がないため、`ptr.lock()`を使って所有権を取得する必要があります。


```bash
Start
Start
End
End
```

<br>

### 参考URL

https://programming.pc-note.net/cpp/smartpointer3.html

<br>