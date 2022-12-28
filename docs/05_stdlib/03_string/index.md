# string

`std::string`は、文字列を扱うためのクラスです。

iostreamと同様にC++でよく使用されています。

<br>

## 文字列の生成

```cpp
#include <iostream>
#include <string>

int main()
{
    std::string data = "Hello, world!";
    std::cout << data << std::endl;
}
```

<br>

## 文字列の長さ

```cpp
#include <iostream>
#include <string>

int main()
{
    std::string data = "Hello, world!";
    std::cout << data.size() << std::endl;
}
```

<br>

## 文字列の比較

```cpp
#include <iostream>
#include <string>

int main()
{
    std::string data1 = "Hello, world!";
    std::string data2 = "Hello, world!";
    std::string data3 = "Hello, world!!";
    std::cout << (data1 == data2) << std::endl;
    if (data1 == data2) {
        std::cout << "data1 == data2" << std::endl;
    }
    if (data1 == data3) {
        std::cout << "data1 == data3" << std::endl;
    }
}
```

<br>

## 文字列の連結（文字列・非文字列）


```cpp
#include <iostream>
#include <string>

int main()
{
    std::string data = "Hello, world!";
    std::cout << data + "!! " << std::endl;

    // add 1
    data += std::to_string(10) + "!!";
    std::cout << data << std::endl;
}
```

<br>

## 通常の文字列(char*)への変換

```cpp
#include <iostream>
#include <cstdio>
#include <string>

int main()
{
    std::string data = "Hello, world!";
    printf("%s\n", data.c_str());
}
```

<br>