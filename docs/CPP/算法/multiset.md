---
title: multiset
createTime: 2025/07/08 17:03:15
permalink: /article/0t3bm2s7/
---

# multiset

在C++的标准模板库（STL）中，`multiset`是一个关联容器，它包含可以重复的键值。`multiset`中的元素总是按照特定的排序标准（默认为升序）进行排序。

`multiset`底层通常使用红黑树（或类似的平衡搜索树）来实现，从而确保了对数时间复杂度的插入、删除和查找操作。

以下是一些`multiset`的基本用法：

1. **包含头文件**：


```cpp
#include <iostream>
#include <set>
```
2. **声明一个multiset**：


```cpp
std::multiset<int> ms;
```
3. **插入元素**：


```cpp
ms.insert(10);
ms.insert(20);
ms.insert(10);  // 注意：multiset允许重复元素
```
4. **查找元素**：


```cpp
if (ms.find(10) != ms.end()) {
    std::cout << "Found 10 in the multiset." << std::endl;
}
```
5. **删除元素**：


```cpp
ms.erase(ms.find(10));  // 删除一个10
// 或者删除所有10
while (ms.find(10) != ms.end()) {
    ms.erase(ms.find(10));
}
```
6. **遍历元素**：


```cpp
for (int val : ms) {
    std::cout << val << " ";
}
std::cout << std::endl;
```
7. **检查multiset是否为空**：


```cpp
if (ms.empty()) {
    std::cout << "The multiset is empty." << std::endl;
}
```
8. **获取multiset的大小**：


```cpp
std::cout << "Size of the multiset: " << ms.size() << std::endl;
```

`multiset`是一个非常有用的容器，当你需要存储可以重复的排序元素时，它是一个很好的选择。