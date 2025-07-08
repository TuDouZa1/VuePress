---
title: deque
createTime: 2025/07/08 17:03:15
permalink: /article/eqz7aun9/
---
# deque

---

### deque 介绍

在C++中，`std::deque`（双端队列）是一个模板类，它提供了在序列的开始和结尾进行高效插入和删除操作的功能。

### 构造函数

```cpp
std::deque<int> d; // 创建一个空的int类型deque
std::deque<int> d(10); // 创建一个包含10个元素的deque，每个元素初始化为int的默认值（0）
std::deque<int> d(10, 42); // 创建一个包含10个元素的deque，每个元素初始化为42
std::deque<int> d(anotherDeque); // 使用另一个deque来初始化
std::deque<int> d(anotherDeque.begin(), anotherDeque.end()); // 使用迭代器范围来初始化
```

### 插入元素

```cpp
d.push_front(value); // 在deque的开始处插入一个元素
d.push_back(value); // 在deque的结尾处插入一个元素
d.insert(iter, value); // 在迭代器iter指向的位置前插入一个元素
d.insert(iter, n, value); // 在迭代器iter指向的位置前插入n个值为value的元素
d.insert(iter, begin, end); // 在迭代器iter指向的位置前插入另一个范围[begin, end)内的元素
```

### 删除元素

```cpp
d.pop_front(); // 删除deque开始处的元素
d.pop_back(); // 删除deque结尾处的元素
d.erase(iter); // 删除迭代器iter指向的元素
d.erase(begin, end); // 删除范围[begin, end)内的元素
d.clear(); // 删除deque中的所有元素
```

### 访问元素

```cpp
int& front(); // 返回对deque开始处元素的引用
const int& front() const; // 返回对deque开始处元素的常量引用
int& back(); // 返回对deque结尾处元素的引用
const int& back() const; // 返回对deque结尾处元素的常量引用
int& operator[](size_t index); // 通过索引访问元素
const int& operator[](size_t index) const; // 通过索引访问元素（常量版本）
int& at(size_t index); // 通过索引访问元素，如果index越界则抛出std::out_of_range异常
const int& at(size_t index) const; // 通过索引访问元素（常量版本），如果index越界则抛出std::out_of_range异常
```

### 容量和大小

```cpp
bool empty() const; // 检查deque是否为空
size_t size() const; // 返回deque中的元素数量
size_t max_size() const; // 返回deque可能包含的最大元素数量
```

### 修改大小

```cpp
void resize(size_t newSize); // 改变deque的大小，如果newSize大于当前大小，则新元素初始化为默认值
void resize(size_t newSize, const value_type& val); // 改变deque的大小，并用val初始化新元素
```

### 迭代器

```cpp
iterator begin(); // 返回指向deque开始处的迭代器
const_iterator begin() const; // 返回指向deque开始处的常量迭代器
iterator end(); // 返回指向deque结尾处下一个位置的迭代器
const_iterator end() const; // 返回指向deque结尾处下一个位置的常量迭代器
```

此外，`std::deque`还支持其他一些函数，如`assign`用于分配新的元素值，`swap`用于交换两个`deque`的内容等。

### 示例

```cpp
#include <iostream>
#include <deque>

int main() {
    std::deque<int> d;

    // 插入元素
    d.push_back(1);
    d.push_front(2);
    d.insert(d.begin() + 1, 3);

    // 访问元素
    std::cout << "Front element: " << d.front() << std::endl;
    std::cout << "Back element: " << d.back() << std::endl;
    std::cout << "Element at index 1: " << d[1] << std::endl;

    // 删除元素
    d.pop_front();
    d.erase(d.begin());

    // 遍历元素
    for (int elem : d) {
        std::cout << elem << " ";
    }
    std::cout << std::endl;

    // 容量和大小
    std::cout << "Size: " << d.size() << std::endl
```