# WSL

Links:

* [Add WSL](https://www.jetbrains.com/help/clion/how-to-use-wsl-development-environment-in-clion.html#wsl-tooclhain)

Создайте новый проект, зайдите в File -> Settings -> Build,Execution,Deployment -> Cmake. Изначально там будет только один профиль Debug. Когда вы нажмете + добавится профиль Release, который пригодится в дальнейшем. Добавьте еще один профиль, назовите его ASAN. В Cmake Options запишите

```shell
-DCMAKE_BUILD_TYPE=ASAN
```

Отредактируйте ваш CmakeLists.txt. Он будет выглядеть примерно так:

```shell
cmake_minimum_required(VERSION 3.12)
project(my_project)

set(CMAKE_CXX_STANDARD 17)

set(CMAKE_CXX_FLAGS_ASAN "-g -fsanitize=address,undefined -fno-sanitize-recover=all"
        CACHE STRING "Compiler flags in asan build"
        FORCE)

add_executable(my_project main.cpp)
```

Теперь вы легко можете переключаться между разными видами сборок: Debug для пошагового дебага, Release для тестирования производительности, ASAN для запуска с санитайзерами.
