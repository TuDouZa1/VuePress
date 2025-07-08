---
title: SDL
createTime: 2025/07/08 17:03:15
permalink: /article/vckora2m/
---
# SDL

> SDL（Simple DirectMedia Layer）是一套[开放源代码](https://baike.baidu.com/item/开放源代码/114160?fromModule=lemma_inlink)的[跨平台](https://baike.baidu.com/item/跨平台/8558902?fromModule=lemma_inlink)多媒体开发库，使用[C语言](https://baike.baidu.com/item/C语言/105958?fromModule=lemma_inlink)写成。SDL提供了数种控制图像、声音、输出入的函数，让开发者只要用相同或是相似的代码就可以开发出跨多个平台（[Linux](https://baike.baidu.com/item/Linux/27050?fromModule=lemma_inlink)、Windows、[Mac OS X](https://baike.baidu.com/item/Mac OS X/470629?fromModule=lemma_inlink)等）的应用软件。现SDL多用于开发游戏、模拟器、[媒体播放器](https://baike.baidu.com/item/媒体播放器/777835?fromModule=lemma_inlink)等多媒体应用领域。
>
> SDL在[GNU](https://baike.baidu.com/item/GNU/671972?fromModule=lemma_inlink) LGPL 2（一个国际上的开源组织）下发布，这个版本允许你将SDL以[动态链接库](https://baike.baidu.com/item/动态链接库/100352?fromModule=lemma_inlink)（dynamic link library）的形式免费地用于商业游戏软件的开发。

## 环境配置

> 均使用VS Code为例子

### 配置cpp和cmake等

下载VS Build Tools，勾选C++桌面开发即可(MSVC)

### 配置SDL

下载SDL库
[Releases · libsdl-org/SDL](https://github.com/libsdl-org/SDL/releases)
[Releases · libsdl-org/SDL_ttf](https://github.com/libsdl-org/SDL_ttf/releases)
[Releases · libsdl-org/SDL_mixer](https://github.com/libsdl-org/SDL_mixer/releases)
[Releases · libsdl-org/SDL_image](https://github.com/libsdl-org/SDL_image/releases)
全部解压提取 `cmake` `include` `lib` 合并到一块就行了
SDL还要手动在 `PATH` 里添加两个环境变量：SDL的根目录，`SDL\lib\x64` 

### 配置CMake

**初始使用配置**

1. 安装C/C++,CMake插件
2. `ctrl+shift+p` 选择“扫描工具包”然后选择“快速入门”，输入项目名称然后勾选文件就行
3. 设置输入 `cmake status bar` 将状态栏选项设置为 `visible`
4. 在下方状态栏点击“更改活动的工具包”选择 `arm64` 
5. 设置输入 `cmake output` 找到 `Cmake: Output Log Encoding` 设置为 `utf-8` 解决乱码问题

**配置CMakeLists.txt**

```cmake
# 标题
cmake_minimum_required(VERSION 3.5.0)
project(SDLShooter VERSION 0.1.0 LANGUAGES C CXX)

# 设置C++标准
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)

# 设置编译选项
if (MSVC)
    add_compile_options(/W4)
else()
    add_compile_options(-Wall -Wextra -Wpedantic -Werror)
endif()

# 设置输出目录
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_DEBUG ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_RELEASE ${CMAKE_BINARY_DIR}/lib)

# 设置输出文件名
set(TARGET ${PROJECT_NAME}-${CMAKE_SYSTEM_NAME})

# 查找并载入CMake预设
find_package(SDL2 REQUIRED)

# 添加可执行文件
add_executable(${TARGET} main.cpp)

# 链接库
target_link_libraries(${TARGET}
                        ${SDL2_LIBRARY}
                        )
```

**跨平台**

```cmake
if (WIN32)
    include_directories("C:/Library/SDL2/include")
    link_directories("C:/Library/SDL2/1ib/x64")
elseif (APPLE)
    include_directories(/usr/local/include/SDL2)
    link_directories(/usr/local/lib)
elseif (UNIX)
    include_directories(/usr/include/SDL2)
    link_directories(/usr/1ib/x86_64-1inux-gnu)
endif()
```

## SDL基本框架

```cpp
#include <iostream>
#include <SDL.h>

int main(int argc, char* argv[]) {
    std::cout << "Hello, world!" << std::endl;
    // SDL初始化
    if (SDL_Init(SDL_INIT_EVERYTHING)!= 0) {
        std::cout << "SDL_Init Error: " << SDL_GetError() << std::endl;
        return 1;
    }
    // 创建窗口
    SDL_Window *window = SDL_CreateWindow("SDLShooter", 100, 100, 800, 600, SDL_WINDOW_SHOWN);
    // 创建渲染器
    SDL_Renderer *renderer = SDL_CreateRenderer(window, -1, SDL_RENDERER_ACCELERATED);

    // todo

    // 清理并退出
    SDL_DestroyRenderer(renderer);
    SDL_DestroyWindow(window);
    SDL_Quit();

    return 0;
}
```

