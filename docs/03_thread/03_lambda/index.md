# Lambda

C++では、ラムダ式を使用することができます。

スレッド対象がそれほど複雑でない場合に有用です。

<br>

前章で作成したスレッドの例をラムダ式を使用して書き換えてみましょう。

```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <vector>

std::mutex mtx;
std::vector<int> v;

int main()
{
    std::vector<std::thread> threads;

    // スレッドをvector（配列に近いもの）で10個作成する
    for (int i = 0; i < 10; ++i)
    {
        threads.push_back(
            std::thread(
                // ラムダ式を使用
                [](int i) {
                    std::lock_guard<std::mutex> lock(mtx);
                    std::cout << ".";
                    v.push_back(i);
                }
                , i)
        );
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

単体の作成の場合は、以下のように書くこともできます。

```cpp
auto t = [](int i) {
    std::lock_guard<std::mutex> lock(mtx);
    std::cout << ".";
    v.push_back(i);
};
```

tをそのまま関数として呼び出すことができます。

<br>

## 参考

https://cpprefjp.github.io/lang/cpp11/lambda_expressions.html

<br>