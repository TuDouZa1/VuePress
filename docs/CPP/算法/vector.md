---
title: vector
createTime: 2025/07/08 17:03:15
permalink: /article/qjryveo3/
---

# VECTOR

C++ 中的 `std::vector` 是一个动态数组，它可以自动管理其大小。以下是一些 `std::vector` 的基本操作及其示例：

1. **包含头文件**

首先，你需要包含 `<vector>` 头文件来使用 `std::vector`。


```cpp
#include <vector>
```
2. **创建 vector**


```cpp
std::vector<int> vec;  // 创建一个空的 int 类型的 vector
std::vector<std::string> strVec;  // 创建一个空的 string 类型的 vector
```
3. **添加元素**


* 使用 `push_back`：


```cpp
vec.push_back(10);
vec.push_back(20);
```
* 使用 `emplace_back`（C++11 起）：


```cpp
vec.emplace_back(30);
```
* 使用 `insert`：


```cpp
vec.insert(vec.begin(),40);  // 在 vector 的开始位置插入40
```
4. **访问元素**


* 使用下标运算符：


```cpp
int firstElement = vec[0];  //访问第一个元素
```
* 使用 `at` 方法（更安全，如果索引出范围会抛出异常）：


```cpp
int firstElement = vec.at(0);
```
* 使用迭代器：


```cpp
for(std::vector<int>::iterator it =vec.begin(); it != vec.end();++it) {
    std::cout << *it << std::endl;
}
```
5. **修改元素**


```cpp
vec[0] = 50;  // 修改第一个元素为 50
```
6. **删除元素**


* 使用 `pop_back` 删除最后一个元素：


```c++
vec.pop_back();
```
* 使用 `erase` 删除指定位置的元素：


```c++
vec.erase(vec.begin());  // 除第一个元素
```
* 使用 `erase` 删除一个范围内的元素：


```c++
vec.erase(vec.begin() + 1, vecend() - 1);  // 删除第二个到倒数第个元素
```
7. **获取 vector 的大小**


```c++
size_t size = vec.size();  // 获取 vector 的大小
```
8. **判断 vector 是否为空**


```c++
bool isEmpty = vec.empty();  // 如果 vector 为空则返回 true，否则返回 false
```
9. **清空 vector**


```cpp
vec.clear();  // 清空 vector
```
10. **其他操作**
* 使用 `resize` 改变 vector 的大小：
```cpp
vec.resize(10);  // 改变 vector 的大小为 10
```
* 使用 `swap` 交换两个 vector 的内容：
```cpp
std::vector<int> anotherVec = {1, 2, 3};
vec.swap(anotherVec);  // 交换 vec 和 anotherVec 的内容
```

这些只是 `std::vector` 的一些基本操作。实际上，`std::vector` 提供了更多的功能和操作，如 `reserve`、`capacity` 等，用于更细粒度的管理内存。使用 `std::vector` 可以让你在 C++ 中更方便地处理动态数组。