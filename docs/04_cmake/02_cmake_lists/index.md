# CMakeLists.txt


```cmake
cmake_minimum_required(VERSION 3.10)
project(hello_world)

set(CMAKE_CXX_STANDARD 17)

set(SRC
    main.cpp
)

add_executable(hello_world ${SRC})
```

