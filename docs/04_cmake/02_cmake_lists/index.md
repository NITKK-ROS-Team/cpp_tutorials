# CMakeLists.txt

CMakeLists.txtの基本的な書き方について、用途別に紹介します。

## messageを表示

メッセージの表示には、`message()`を使います。

主に環境変数の確認に使用します。

メッセージの表示には、次のモードがあります。

| モード | 説明 | 挙動 | 成功？ |
| --- | --- | --- | --- |
| なし | 通常のメッセージ | 通常のメッセージとして表示 | ○ |
| STATUS | ステータスメッセージ | `--` で始まるメッセージとして表示 | ○ |
| WARNING | 警告メッセージ | `CMake Warning` で始まるメッセージとして表示 | ○ |
| ERROR | エラーメッセージ | `CMake Error` で始まるメッセージとして表示、ただし、ビルドは継続される | × |
| FATAL_ERROR | 致命的なエラーメッセージ | `CMake Error` で始まるメッセージとして表示し、処理を中断 | × |

```cmake
cmake_minimum_required(VERSION 3.0)
project(hoge)

message("HOGEHOGE")
message(STATUS "HOGEHOGE-STATUS")
message(WARNING "HOGEHOGE-WARNING")
message(ERROR "HOGEHOGE-ERROR")
message(FATAL_ERROR "HOGEHOGE-FATAL_ERROR")
```


```bash
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
HOGEHOGE
-- HOGEHOGE-STATUS
CMake Warning at CMakeLists.txt:6 (message):
  HOGEHOGE-WARNING


ERRORHOGEHOGE-ERROR
CMake Error at CMakeLists.txt:8 (message):
  HOGEHOGE-FATAL_ERROR


-- Configuring incomplete, errors occurred!
See also "***/build/CMakeFiles/CMakeOutput.log"
```

<br>

## 変数の定義・参照

変数の定義には、`set()`を使います。変数の参照には、`${変数名}`を使います。

<br>

`set()`の第一引数に変数名、第二引数に値を指定します。

通常は上書きされますが、第二引数に対して`${変数名} 追加の情報`で変数に追加できます。

これは、プログラムのコンパイルオプションや同時に複数ファイルをターゲットにする際に使えます。

<br>

以下の例では、次のステップを踏んでいます。

- 変数`HOGE`に`hoge1`を代入
- 変数`HOGE`を表示
- 変数`HOGE`に`hoge2`を追加
- 変数`HOGE`を表示 (HOGEには`hoge1 hoge2`が入っている)
- 変数`HOGE`に`hoge3`を代入
- 変数`HOGE`を表示 (HOGEには`hoge3`のみが入っている)


```cmake
cmake_minimum_required(VERSION 3.0)
project(hoge)

set(HOGE "hoge1")
message(${HOGE})
set(HOGE ${HOGE} "hoge2")
message(${HOGE})
set(HOGE "hoge3")
message(${HOGE})
```

```bash
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
hoge1
hoge1 hoge2
hoge3
-- Configuring done
-- Generating done
-- Build files have been written to: ...
```

<br>

## ターゲットの定義

ターゲットの定義には、`add_executable()`を使います。

`add_executable()`の第一引数にターゲット名、第二引数にソースファイルを指定します。

ソースファイルは複数可能です。また、ヘッダーファイルは指定しなくても大丈夫です。(明示的にincludeされている場合)

<br>

以下の例では、次のステップを踏んでいます。

- ターゲット`hoge`を定義
- ターゲット`hoge`を表示
- ターゲット`hoge`にソースファイル`hoge.cpp`を追加

```cmake
cmake_minimum_required(VERSION 3.0)
project(hoge)

set(HOGE "hoge")
message(${HOGE})
add_executable(${HOGE} ${HOGE}.cpp)
```

```bash
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
hoge
-- Configuring done
-- Generating done
-- Build files have been written to: ...
```

コンパイルの実行後は、`hoge`という実行ファイルが生成されているはずです。

ソースファイルが見つからない・コンパイルエラーが出る場合は失敗します。

<br>

## ターゲットにコンパイルオプションを追加

ターゲットにコンパイルオプションを追加するには、`target_compile_options()`を使います。

`target_compile_options()`の第一引数にターゲット名、第二引数にコンパイルオプションを指定します。

<br>

以下の例では、次のステップを踏んでいます。

- ターゲット`hoge`にコンパイルオプション`-std=c++11`を追加
- 最適化オプション`-O3`を追加

```cmake
cmake_minimum_required(VERSION 3.0)
project(hoge)

set(HOGE "hoge")
add_executable(${HOGE} ${HOGE}.cpp)
target_compile_options(${HOGE} PRIVATE -std=c++11)
target_compile_options(${HOGE} PRIVATE -O3)
```


```bash
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: ...
```

<br>

## ライブラリを生成

ライブラリを生成するには、`add_library()`を使います。

`add_library()`の第一引数にライブラリ名、第二引数にライブラリの種類、第三引数にソースファイルを指定します。

ライブラリの種類は、`STATIC`か`SHARED`を指定します。

- `STATIC`は静的ライブラリを生成します。
- `SHARED`は動的ライブラリを生成します。

静的ライブラリは、実行ファイルにリンクされるため、実行ファイルのサイズが大きくなります。一方、動的ライブラリは、実行ファイルにリンクされず、実行時に読み込まれます。そのため、実行ファイルのサイズは小さくなります。

<br>

以下の例では、次のステップを踏んでいます。

- ターゲット`fuga`を定義
- ターゲット`fuga`にソースファイル`fuga.cpp`を追加
- ライブラリとして`fuga`を生成

<br>

```cmake
cmake_minimum_required(VERSION 3.0)
project(hoge)

set(FUGA "fuga")
add_library(${FUGA} STATIC ${FUGA}.cpp)
```

<br>

## ライブラリをリンク

ライブラリをリンクするには、`target_link_libraries()`を使います。

先ほどのfugaライブラリをリンクするには、以下のようにします。

```cmake
cmake_minimum_required(VERSION 3.0)
project(hoge)

set(FUGA "fuga")
add_library(${FUGA} STATIC ${FUGA}.cpp)

set(HOGE "hoge")
add_executable(${HOGE} ${HOGE}.cpp)
target_link_libraries(${HOGE} ${FUGA})
```

<br>

作成したソースコードを示します。

**fuga.h**

```cpp
#pragma once
#include <cstdio>

void fuga(void);
```

**fuga.cpp**

```cpp
#include "fuga.h"

void fuga(void) {
    printf("Hello World\n");
}
```

**hoge.cpp**

```cpp
#include "fuga.h"

int main(void) {
    fuga();
    return 0;
}
```

<br>

コンパイル結果は以下のようになります。

```bash
$ cmake ..
-- Configuring done
-- Generating done
-- Build files have been written to: ...
$ make
Scanning dependencies of target fuga
[ 25%] Building CXX object CMakeFiles/fuga.dir/fuga.cpp.o
[ 50%] Linking CXX static library libfuga.a
[ 50%] Built target fuga
Scanning dependencies of target hoge
[ 75%] Building CXX object CMakeFiles/hoge.dir/hoge.cpp.o
[100%] Linking CXX executable hoge
[100%] Built target hoge
```

<br>

## インクルードディレクトリを指定

インクルードディレクトリを指定するには、`target_include_directories()`を使います。

たとえば、先ほどの`fuga.h`を新しく同じディレクトリに作成した`include/`ディレクトリに入れた場合、相対パスを変更することが本来の作業になりそうですが、cmake側で変更すると次のようになります。

```cmake
cmake_minimum_required(VERSION 3.0)
project(hoge)

set(FUGA "fuga")
add_library(${FUGA} STATIC ${FUGA}.cpp)
target_include_directories(${FUGA} PUBLIC include)

set(HOGE "hoge")
add_executable(${HOGE} ${HOGE}.cpp)
target_link_libraries(${HOGE} ${FUGA})
```

<br>

## インストール

ビルド結果を特定のディレクトリにコピーすることができます。

特に`/usr/local/bin`や`/usr/local/lib`などにコピーすることで、システム全体で使えるようになります。

```cmake
cmake_minimum_required(VERSION 3.0)
project(hoge)

set(FUGA "fuga")
add_library(${FUGA} STATIC ${FUGA}.cpp)
target_include_directories(${FUGA} PUBLIC include)

set(HOGE "hoge")
add_executable(${HOGE} ${HOGE}.cpp)
target_link_libraries(${HOGE} ${FUGA})

install(TARGETS ${HOGE} DESTINATION bin)
install(TARGETS ${FUGA} DESTINATION lib)
```

<br>

installの実行には`sudo make install`を使います。

```bash
sudo make install
[sudo] password for ***: ***
[ 50%] Built target fuga
[100%] Built target hoge
Install the project...
-- Install configuration: ""
-- Installing: /usr/local/bin/hoge
-- Installing: /usr/local/lib/libfuga.a
```

<br>

実行します。

```bash
$ hoge
Hello World
```

<br>

## 他のライブラリを使用する

ここでは、libcurlライブラリを使用してみます。

libcurlは、HTTP通信を行うためのライブラリです。

<br>

以下のプログラムは、googleにpingを送ってその結果を表示するものです。

```cpp
#include <cstdio>
#include <curl/curl.h>

// google ping
int main(void) {
    CURL *curl;
    CURLcode res;

    curl = curl_easy_init();
    if(curl) {
        curl_easy_setopt(curl, CURLOPT_URL, "http://www.google.com/");
        res = curl_easy_perform(curl);
        if(res != CURLE_OK)
            fprintf(stderr, "curl_easy_perform() failed: %s", curl_easy_strerror(res));
        curl_easy_cleanup(curl);
    }
    return 0;
}
```

<br>

cmakeの設定は以下のようになります。

```cmake
cmake_minimum_required(VERSION 3.0)
project(hoge)

find_package(CURL REQUIRED)

set(HOGE "hoge")
add_executable(${HOGE} ${HOGE}.cpp)
target_link_libraries(${HOGE} ${CURL_LIBRARIES})
```

`target_include_directories()`は`/usr/local/include`にインストールされている場合には不要です。

<br>

実行すると、オンラインに接続されているときはhtmlが流れてくると思います。

<br>

## 条件分岐：if

条件分岐は`if()`を使います。

以下の例では、`HOGE`が`hoge1`か`hoge2`かそれ以外かで処理を分岐しています。

```cmake
cmake_minimum_required(VERSION 3.0)
project(hoge)

set(HOGE "hoge2")

if(HOGE STREQUAL "hoge1")
    message(STATUS "HOGE is hoge1")
elseif(HOGE STREQUAL "hoge2")
    message(STATUS "HOGE is hoge2")
else()
    message(STATUS "else")
endif()
```

<br>

## ループ：foreach

`foreach()`を使うと、リストの要素を順番に処理することができます。

- LISTS: 指定されたリストの要素を順番に処理する
- RANGE: 0から指定した数までの数字をリストにする
- ITEMS: 各値をリストにする

ここでは、HOGEにリストを代入して、その要素を順番に表示しています。

また、0から10までの数字を順番に表示していき、5になったらループを抜けるようにしています。

```cmake
cmake_minimum_required(VERSION 3.0)
project(hoge)

set(HOGE "hoge1;hoge2;hoge3")

foreach(ONEHOGE IN LISTS HOGE)
    message(STATUS "HOGE: ${ONEHOGE}")
endforeach()

foreach(NUMBER RANGE 10)
    if (NUMBER EQUAL 5)
        break()
    endif()
    message(STATUS "NUMBER: ${NUMBER}")
endforeach()
```

```bash
-- HOGE: hoge1
-- HOGE: hoge2
-- HOGE: hoge3
-- NUMBER: 0
-- NUMBER: 1
-- NUMBER: 2
-- NUMBER: 3
-- NUMBER: 4
-- Configuring done
-- Generating done
```

<br>
