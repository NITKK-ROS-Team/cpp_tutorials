# vector

vectorは、要素の追加や削除が可能な配列です。

<br>

## vectorのメンバ関数

vectorのメンバ関数は、以下の通りです。

- `at(int index)`: 指定したインデックスの要素を返します。範囲外のインデックスを指定した場合、`std::out_of_range`例外を投げます。（`[]`でもアクセス可能です。）
- `front()`: 先頭の要素を返します。
- `back()`: 末尾の要素を返します。
- `push_back(T value)`: 末尾に要素を追加します。
- `pop_back()`: 末尾の要素を削除します。
- `insert(iterator it, T value)`: 指定したイテレータの位置に要素を挿入します。
- `erase(iterator it)`: 指定したイテレータの位置の要素を削除します。
- `clear()`: 全ての要素を削除します。
- `size()`: 要素の数を返します。
- `empty()`: 要素が空かどうかを返します。
- `swap(vector& v)`: 2つのvectorをスワップします。

<br>


## vectorの使用

vectorの使用例は、以下の通りです。

挙動を予想してみましょう。

```cpp
#include <vector>
#include <iostream>

int main()
{
    std::vector<int> v;
    
    // 要素の追加
    for (int i = 0; i < 5; i++)
    {
        v.push_back(i);
    }

    for (int i = 0; i < v.size(); i++)
    {
        std::cout << "v[" << i << "] = " << v[i] << std::endl;
    }

    // 末尾の削除
    v.pop_back();
    // 特定の要素を削除
    v.erase(v.begin() + 2);

    std::cout << "----------------" << std::endl;
    for (int i = 0; i < v.size(); i++)
    {
        std::cout << "v[" << i << "] = " << v[i] << std::endl;
    }

    // 先頭と末尾のスワップ
    std::swap(v.front(), v.back());

    std::cout << "----------------" << std::endl;
    for (int i = 0; i < v.size(); i++)
    {
        std::cout << "v[" << i << "] = " << v.at(i) << std::endl;
    }
}
```

出力

```bash
v[0] = 0
v[1] = 1
v[2] = 2
v[3] = 3
v[4] = 4
----------------
v[0] = 0
v[1] = 1
v[2] = 3
----------------
v[0] = 3
v[1] = 1
v[2] = 0
```

<br>

## 参考

https://cpprefjp.github.io/reference/vector/vector.html