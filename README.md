## Задание 1

Вам поручили перейти на систему автоматизированной сборки CMake. Исходные файлы находятся в директории formatter_lib. В этой директории находятся файлы для статической библиотеки formatter. Создайте CMakeList.txt в директории formatter_lib, с помощью которого можно будет собирать статическую библиотеку formatter.

```sh
cmake_minimum_required(VERSION 3.5)

project(formatter)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

file(GLOB SOURCES "*.cpp")

add_library(formatter STATIC formatter.cpp)

target_include_directories(formatter PUBLIC formatter_lib)
```

## Задание 2

У компании "Formatter Inc." есть перспективная библиотека, которая является расширением предыдущей библиотеки. Т.к. вы уже овладели навыком созданием CMakeList.txt для статической библиотеки formatter, ваш руководитель поручает заняться созданием CMakeList.txt для библиотеки formatter_ex, которая в свою очередь использует библиотеку formatter.

```sh
cmake_minimum_required(VERSION 3.5)
project(formatter_ex)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(formatter_ex STATIC formatter_ex.cpp)

target_include_directories(formatter_ex PUBLIC 
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib
)
target_link_libraries(formatter_ex PUBLIC formatter)
```



Задание 3

Конечно же ваша компания предоставляет примеры использования своих библиотек. Чтобы продемонстрировать как работать с библиотекой formatter_ex, вам необходимо создать два CMakeList.txt для двух простых приложений:

    hello_world, которое использует библиотеку formatter_ex;
    solver, приложение которое испольует статические библиотеки formatter_ex и solver_lib.

```sh
// hello_world
cmake_minimum_required(VERSION 3.5)
project(hello_world)

set(CMAKE_CXX_STANDARD 11)

set(CMAKE_CXX_STANDARD_REQUIRED ON)


add_executable(hello_world ${CMAKE_CURRENT_SOURCE_DIR}/hello_world.cpp)

target_include_directories(hello_world PUBLIC 
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib
)
target_link_libraries(hello_world PRIVATE formatter_ex)
```


```sh
//solver_lib
cmake_minimum_required(VERSION 3.4)
project(solver VERSION 1.0.0)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


add_library(solver STATIC solver.cpp)
target_include_directories(solver PUBLIC solver_lib)
```

```
//solver

cmake_minimum_required(VERSION 3.5)
project(solver)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(equation ${CMAKE_CURRENT_SOURCE_DIR}/equation.cpp)

target_include_directories(equation PUBLIC 
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex
    ${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib
)
target_link_libraries(equation PUBLIC formatter_ex solver)
```

## Test CMake

```sh
_build/hello_world_application/hello_world && echo
```
-------------------------
hello, world!
-------------------------

```sh
_build/solver_application/equation && echo

1
2
3
```
-------------------------
error: discriminant < 0



