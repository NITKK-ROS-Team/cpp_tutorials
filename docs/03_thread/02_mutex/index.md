# mutex

mutexは、複数のスレッドが同時にアクセスすると問題が起こる変数に対して、排他制御を行うための機構です。

mutexでロックされた変数は、アンロックされるまで触ることができなくなります。

## 例

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <vector>

std::mutex mtx;
std::vector<int> v;

// グローバル変数vに対して、値の代入を行う
void input_data(int i)
{
    // std::lock_guard<std::mutex> lock(mtx); // ここのコメントを外すと、mutexが使用される
    std::cout << ".";
    v.push_back(i);

}

int main()
{
    std::vector<std::thread> threads;

    // スレッドをvector（配列に近いもの）で10個作成する
    for (int i = 0; i < 10; ++i)
    {
        threads.push_back(std::thread(input_data, i));
    }
    // スレッドを生成
    for (auto& t : threads)
    {
        t.join();
    }

    // 結果の出力
    std::cout << std::endl;
    for (auto i : v)
    {
        std::cout << i << std::endl;
    }
}
```

**結果：mutex未使用**

結果は実行するたびに変わります。

`double free or corruption (fasttop)`が発生することがあります。

これは、同時にアクセスされた変数に対して、排他制御が行われていないためです。

```bash
double free or corruption (fasttop)
Aborted (core dumped)
```

**結果：mutex使用**

結果は実行するたびに変わります。（順番を保証することはできません）

排他制御が行われているため、`double free or corruption (fasttop)`は発生しません。

```bash
..........
1
2
3
4
5
6
7
8
9
10
```

## 参考

https://cpprefjp.github.io/reference/mutex/mutex.html