# Thread

スレッドとは、コンピュータによる並列処理を指します。

逐次実行では時間がかかってしまうタスクに対して並列化を行うことで効率的にCPUリソースを使用することができるようになります。

数学・理科・英語の3教科の宿題があなたに与えられていると仮定して、逐次処理が順番に解くとすれば、並列処理であれば定時毎に解く宿題を変更していきます。

<br>

## 簡単なスレッド

まずは、簡単なスレッドを示します。

以下のプログラムでは、`std::thread`クラスを使用して、`hello`関数を別スレッドで実行しています。

`hello`関数は、1秒間スリープしてから`Hello, world!`と出力して変数`a`をインクリメントしています。

mainでは全てのスレッドを`detach`した後に、変数`a`が5になるまで待機しています。

スレッドでは、`join`を使用すると、スレッドが終了するまで待機することができます。

`detach`を使用すると、終了待ちをせずにスレッドを実行します。

```cpp
#include <iostream>
#include <thread>
#include <chrono>

int a = 0;
void hello()
{
    // sleep 1
    std::this_thread::sleep_for(std::chrono::seconds(1));
    std::cout << "Hello, world!" << std::endl;
    a++;
}

int main()
{
    for (int i = 0; i < 5; i++) {
        std::thread t(hello);

        // t.join();
        t.detach();
    }
    // wait for all done
    while (a < 5) {
        std::this_thread::sleep_for(std::chrono::seconds(1));
    }
}
```

コンパイルには、`-pthread`オプションを付けてください。

`g++ main.cpp -pthread`

<br>

1秒後に`Hello, world!`が5回出力されます。

<br>

