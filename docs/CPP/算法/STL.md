---
title: STL
createTime: 2025/07/08 17:03:15
permalink: /article/1f3y96ra/
---
# 常见STL容器用法
### [vector](#vector) | [stack](#stack) | [queue](#queue) | [priority_queue](#priority_queue) | [deque](#deque) | [set](#set) | [multiset](#multiset)  | [map](#map) | [bitset](#bitset)
###### C++标准库文档：<a href="https://zh.cppreference.com/w/%E9%A6%96%E9%A1%B5" target="_blank">cppreference</a>
---

**迭代器函数：**
迭代器函数只要是可以通过迭代器访问内部元素的stl容器都可以使用，通常需要`<algorithm>`头文件
<details>

1. **advance**
   - **功能**：使迭代器向前或向后移动指定的距离。
   - **参数**：迭代器（引用传递）和要移动的距离。
   - **用法**：`advance(it, n);` 其中`it`是迭代器，`n`是距离（可以是负数，表示向后移动）。
   - **注意**：对于随机访问迭代器，可以直接使用`it += n;`，但`advance`函数提供了更通用的解决方案，适用于所有类型的迭代器。

2. **distance**
   - **功能**：计算两个迭代器之间的距离，即它们之间元素的个数。
   - **参数**：两个迭代器（first和last）。
   - **返回值**：两个迭代器之间的距离。
   - **用法**：`auto dist = distance(first, last);`

3. **begin和end**
   - **功能**：`begin`函数返回指向容器第一个元素的迭代器，`end`函数返回指向容器最后一个元素之后位置的迭代器（即“尾后迭代器”）。
   - **参数**：容器对象。
   - **用法**：`auto it = begin(container);` 和 `auto last = end(container);`

4. **prev**
   - **功能**：返回给定迭代器的前n个位置的迭代器。
   - **参数**：迭代器和一个可选的距离n（默认为1）。
   - **注意**：这个函数需要双向迭代器或更高级别的迭代器。
   - **用法**：`auto prevIt = prev(it, n);`

5. **next**
   - **功能**：返回给定迭代器的后n个位置的迭代器。
   - **参数**：迭代器和一个可选的距离n（默认为1）。
   - **注意**：这个函数需要前向迭代器或更高级别的迭代器。
   - **用法**：`auto nextIt = next(it, n);`

6. **find**
   - **功能**：在指定范围内查找给定值的第一个出现位置。
   - **参数**：两个迭代器（表示范围）和一个要查找的值。
   - **返回值**：如果找到，则返回指向该元素的迭代器；否则返回尾后迭代器。
   - **用法**：`auto it = find(first, last, value);`

7. **find_if**
   - **功能**：在指定范围内查找满足特定条件的第一个元素。
   - **参数**：两个迭代器（表示范围）和一个谓词（一个返回布尔值的函数或可调用对象）。
   - **返回值**：如果找到，则返回指向该元素的迭代器；否则返回尾后迭代器。
   - **用法**：`auto it = find_if(first, last, predicate);`

8. **insert**
   - **功能**：在容器的指定位置插入一个或多个元素。
   - **注意**：虽然`insert`不是直接作用于迭代器的函数，但它通常与迭代器一起使用来指定插入位置。
   - **用法**：`container.insert(it, value);` 或 `container.insert(it, first, last);`

9. **erase**
   - **功能**：从容器中删除一个或多个元素。
   - **注意**：`erase`函数接受一个或两个迭代器作为参数，指定要删除的元素范围。
   - **用法**：`container.erase(it);` 或 `container.erase(first, last);`

10. **unique**
    - **功能**：移除容器中相邻的重复元素（只保留第一个）。
    - **注意**：这个函数实际上修改了容器的内容，并通过迭代器范围来操作。但它通常与排序算法结合使用，以确保重复的元素相邻。
    - **用法**：`container.erase(unique(container.begin(), container.end()), container.end());`（注意，`unique`函数只重排元素并返回一个迭代器，实际删除操作需要与`erase`结合进行）

11. **lower_bound**
    - **功能**：查找第一个不小于（即大于或等于）给定值的元素。返回一个迭代器，指向该元素；如果未找到这样的元素，则返回指向范围末尾的迭代器（即尾后迭代器）。
    - **注意**：lower_bound 要求给定的范围必须是已排序的。
    - **用法**：`auto it = std::lower_bound(vec.begin(), vec.end(), target);`

12. **upper_bound**
    - **功能**：查找第一个大于给定值的元素。同样返回一个迭代器，指向该元素；如果未找到这样的元素（即所有元素都不大于给定值），则返回指向范围末尾的迭代器。
    - **注意**：upper_bound 要求给定的范围必须是已排序的。
    - **用法**：`auto ub = std::upper_bound(vec.begin(), vec.end(), target);`

13. **binary_search**
    - **功能**：检查给定值是否存在于已排序的范围内。
    - **注意**：如果存在，则返回true；否则返回false。
    - **用法**：`bool found = std::binary_search(vec.begin(), vec.end(), target);`

需要注意的是，这些函数的可用性和行为可能会根据容器的类型和迭代器的类型而有所不同。

</details>

## <a id = "vector">[vector](#常见stl容器用法)</a>
#### 特点
#### 函数
void resize( size_type new_size );  
void resize( size_type new_size, const value_type& val );   // 使用指定值填充新增的元素  

#### 示例
## <a id = "stack">[stack](#常见stl容器用法)</a>
#### 特点
由deque实现，后进先出（LIFO, Last In First Out）
#### 函数
push(const value_type& val): 将元素压入栈顶。
pop(): 弹出栈顶元素。如果栈为空，则此操作未定义（通常会导致运行时误）。
top(): 返回栈顶元素的引用。如果栈为空，则此操作未定义。
empty() const: 检查栈是否为空。
size() const: 返回栈中元素的数量。
#### 示例
```c++
#include <iostream>
#include <stack>

int main()
{
    std::stack<int> s;

    s.push(1);
    s.push(2);
    s.push(3);

    std::cout << s.top() << std::endl; // 3

    s.pop(); // 弹出顶部元素

    std::cout << s.top() << std::endl; // 2

    if (s.empty())
        std::cout << "Stack is empty." << std::endl;
    else
        std::cout << "Stack size: " << s.size() << std::endl; // 输出: 2

    return 0;
}
```

## <a id = "queue">[queue](#常见stl容器用法)</a>
#### 特点
由deque实现，先进先出（FIFO, First In First Out）
#### 函数
push(const value_type& val): 在队列尾部添加一个元素。
pop(): 移除队列头部的元素。如果队列为空，则此操作未定义。
front(): 返回队列头部元素的引用。如果队列为空，则此操作未定义。
back(): 返回队列尾部元素的引用。如果队列为空，则此操作未定义。
empty() const: 检查队列是否为空。
size() const: 返回队列中元素的数量。
#### 示例
```c++
#include <iostream>
#include <queue>

int main()
{
    std::queue<int> q;

    q.push(1);
    q.push(2);
    q.push(3);

    std::cout << q.front() << std::endl; // 查看头部元素 1
    std::cout << q.back() << std::endl;  // 查看尾部元素 3

    q.pop(); // 出队元素

    std::cout << q.front() << std::endl; // 查看头部元素 2

    if (q.empty())
        std::cout << "Queue is empty." << std::endl;
    else
        std::cout << "Queue size:" << q.size() << std::endl; // 2

    return 0;
}
```
## <a id = "priority_queue">[priority_queue](#常见stl容器用法)</a>
#### 特点
堆(heap)为底层，默认大根堆，从高到低排序，读取最大元素效率高
#### 函数
函数和 stack 一样
#### 示例
```cpp
#include <iostream>  
#include <queue>  
#include <vector>  

int main() {  

    std::priority_queue<int> pq;  
    // 插入元素  
    pq.push(3);  
    pq.push(1);  
    pq.push(4);  
    pq.push(1);  
    pq.push(5);  
    // 访问最高优先级元素  
    std::cout << "Top element: " << pq.top() << std::endl; // 输出: 5  
    // 删除最高优先级元素  
    pq.pop();  
    // 遍历队列（注意：不能直接遍历，这里仅作为示例说明）  
    while (!pq.empty()) {  
        std::cout << pq.top() << " ";  
        pq.pop();  
    }  
    // 注意：在实际使用中，不应该在循环中输出并删除所有元素，因为这将导致队列为空。  

    // 获取队列状态  
    std::cout << "Size: " << pq.size() << std::endl; // 输出: 0，因为队列已空  
    std::cout << "Is empty? " << (pq.empty() ? "Yes" : "No") << std::endl; // 输出: Yes  
    return 0;  
}
```
#### priority_queue 实现小根堆
```cpp
struct cmp
{
    bool operator()(const int& a, const int& b) {return a > b;}
};

priority_queue<int, vector<int>, cmp> pq;
```
```cpp
priority_queue<int, vector<int>, greater<int>> pq;
```
## <a id = "deque">[deque](#常见stl容器用法)</a>
#### 特点
deque是一种双开口的连续空间的数据结构，它允许在两端进行高效的插入和删除操作
#### 函数
构造函数

```cpp
std::deque<int> d; // 创建一个空的int类型deque
std::deque<int> d(10); // 创建一个包含10个元素的deque，每个元素初始化为int的默认值（0）
std::deque<int> d(10, 42); // 创建一个包含10个元素的deque，每个元素初始化为42
std::deque<int> d(anotherDeque); // 使用另一个deque来初始化
std::deque<int> d(anotherDeque.begin(), anotherDeque.end()); // 使用迭代器范围来初始化
```

插入元素

```cpp
d.push_front(value); // 在deque的开始处插入一个元素
d.push_back(value); // 在deque的结尾处插入一个元素
d.insert(iter, value); // 在迭代器iter指向的位置前插入一个元素
d.insert(iter, n, value); // 在迭代器iter指向的位置前插入n个值为value的元素
d.insert(iter, begin, end); // 在迭代器iter指向的位置前插入另一个范围[begin, end)内的元素
```

删除元素

```cpp
d.pop_front(); // 删除deque开始处的元素
d.pop_back(); // 删除deque结尾处的元素
d.erase(iter); // 删除迭代器iter指向的元素
d.erase(begin, end); // 删除范围[begin, end)内的元素
d.clear(); // 删除deque中的所有元素
```

访问元素

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

容量和大小

```cpp
bool empty() const; // 检查deque是否为空
size_t size() const; // 返回deque中的元素数量
size_t max_size() const; // 返回deque可能包含的最大元素数量
```

修改大小

```cpp
void resize(size_t newSize); // 改变deque的大小，如果newSize大于当前大小，则新元素初始化为默认值
void resize(size_t newSize, const value_type& val); // 改变deque的大小，并用val初始化新元素
```

迭代器

```cpp
iterator begin(); // 返回指向deque开始处的迭代器
const_iterator begin() const; // 返回指向deque开始处的常量迭代器
iterator end(); // 返回指向deque结尾处下一个位置的迭代器
const_iterator end() const; // 返回指向deque结尾处下一个位置的常量迭代器
```

此外，`std::deque`还支持其他一些函数，如`assign`用于分配新的元素值，`swap`用于交换两个`deque`的内容等。

#### 示例

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
## <a id = "set">[set](#常见stl容器用法)</a>
#### 特点
基于红黑树实现的容器，用于存储唯一元素的集合，且这些元素会根据一定的排序规则（默认为升序）自动排序。
#### 函数
insert();  插入
erase();   删除，可以通过值、迭代器或迭代器范围来指定要删除的元素。
find();    查找，返回指向该元素的迭代器。如果不存在，则返回end()迭代器。
count();   查找，对于set来说总是返回0（如果元素不存在）或1
size();大小
empty();
swap();
#### 示例
```cpp
#include <iostream>  
#include <set>  
  
int main() {  
    // 创建一个空的set  
    std::set<int> mySet;  
  
    // 插入元素  
    mySet.insert(10);  
    mySet.insert(20);  
    mySet.insert(15);  
    mySet.insert(10); // 这行代码实际上不会添加任何新元素，因为set中的元素是唯一的  
  
    // 查找元素  
    auto it = mySet.find(15);  
    if (it != mySet.end()) {  
        std::cout << "Found 15 in the set." << std::endl;  
    }  
  
    // 遍历set  
    std::cout << "Elements in the set: ";  
    for (int elem : mySet) {  
        std::cout << elem << " ";  
    }  
    std::cout << std::endl;  
  
    // 删除元素  
    mySet.erase(10); // 删除第一个找到的10（实际上set中只有一个10）  
    if (mySet.erase(100)) { // 尝试删除不存在的元素，这会返回0  
        std::cout << "Deleted 100 (but it wasn't there)." << std::endl;  
    } else {  
        std::cout << "100 was not found in the set." << std::endl;  
    }  
  
    // 获取集合大小和检查是否为空  
    std::cout << "Size of the set: " << mySet.size() << std::endl;  
    if (mySet.empty()) {  
        std::cout << "The set is empty." << std::endl;  
    } else {  
        std::cout << "The set is not empty." << std::endl;  
    }  
  
    // 交换集合内容（这里仅作为演示，实际上并没有另一个set来交换）  
    // 假设我们有一个另一个set  
    std::set<int> anotherSet = {30, 40, 50};  
    // 交换内容  
    mySet.swap(anotherSet);  
  
    // 再次遍历交换后的set  
    std::cout << "After swapping, elements in mySet: ";  
    for (int elem : mySet) {  
        std::cout << elem << " ";  
    }  
    std::cout << std::endl;  
  
    return 0;  
}
```
#### set降序排序
```cpp
struct Compare {  
    bool operator()(int a, int b) const {  
        return a > b;  
    }  
};  
std::set<int, Compare> mySetCompare;
```
## <a id ="multiset">[multiset](#常见stl容器用法)</a>
#### 特点
红黑树实现，包含可以重复的键值。`multiset`中的元素总是按照特定的排序标准（默认为升序）进行排序。
#### 函数
begin(): 返回一个指向容器中第一个元素的迭代器。
end(): 返回一个指向容器中最后一个元素之后位置的迭代器（即“尾后迭代器”）。
rbegin(): 返回一个指向容器中最后一个元素的反向迭代器。
rend(): 返回一个指向容器中第一个元素之前位置的反向迭代器（即“尾前反向迭代器”）。

#### 示例
求解滑动窗口
```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        multiset<int> st;
        vector<int> ans;
        for (int i = 0; i < nums.size(); i++) {
            if (i >= k) st.erase(st.find(nums[i - k]));
            st.insert(nums[i]);
            if (i >= k - 1) ans.push_back(*st.rbegin());
        }
        return ans;
    }
};
```
## <a id = "map">[map](#常见stl容器用法)</a>
#### 特点
map是一个关联容器，它存储元素并形成键值对（key-value pairs）的集合，其中每个元素都是一个键值对。map内部通常通过红黑树实现，以支持对数时间复杂度的查找、插入和删除操作。map的键是唯一的，并且自动按键的排序规则（默认为升序）排序。
#### 函数
其余和set基本一样
lower_bound(const key_type& key): 返回一个迭代器，指向第一个不小于key的元素。
upper_bound(const key_type& key): 返回一个迭代器，指向第一个大于key的元素。
equal_range(const key_type& key): 返回一个包含两个迭代器的pair，第一个迭代器指向第一个不小于key的元素，第二个迭代器指向第一个大于key的元素。如果容器中不存在等于key的元素，则两个迭代器相等且都等于upper_bound(key)。
#### 示例
```cpp
#include <iostream>  
#include <map>  
#include <string>  
  
int main() {  
    // 使用默认构造函数创建map  
    std::map<int, std::string> myMap;  
  
    // 插入元素  
    myMap.insert(std::make_pair(1, "one"));  
    myMap[2] = "two"; // 使用[]运算符插入或更新元素  
    myMap.insert({3, "three"}); // C++11及以后支持这种插入方式  
  
    // 查找元素  
    auto it = myMap.find(2);  
    if (it != myMap.end()) {  
        std::cout << "Found key 2 with value " << it->second << std::endl;  
    }  
  
    // 尝试访问不存在的键（使用at()会抛出异常，这里仅作为演示）  
    try {  
        std::string value = myMap.at(4); // 这将抛出std::out_of_range异常  
    } catch (const std::out_of_range& e) {  
        std::cout << "Key 4 not found." << std::endl;  
    }  
  
    // 遍历map  
    std::cout << "Traversing the map:" << std::endl;  
    for (const auto& pair : myMap) {  
        std::cout << "Key: " << pair.first << ", Value: " << pair.second << std::endl;  
    }  
  
    // 删除元素  
    myMap.erase(1); // 通过键删除  
    if (it != myMap.end()) { // 注意：这里it是之前找到的键为2的迭代器，为演示而保留  
        myMap.erase(it); // 通过迭代器删除（但这里不应该用it，因为它已经指向了一个可能已被删除的元素之后的位置）  
    } else {  
        // 正确删除方式：直接使用find找到要删除的元素的迭代器，然后删除  
        it = myMap.find(2); // 假设我们要删除键为2的元素  
        if (it != myMap.end()) {  
            myMap.erase(it);  
        }  
    }  
  
    // 再次遍历map以显示删除后的结果  
    std::cout << "Map after deletion:" << std::endl;  
    for (const auto& pair : myMap) {  
        std::cout << "Key: " << pair.first << ", Value: " << pair.second << std::endl;  
    }  
  
    // 获取集合大小和检查是否为空  
    std::cout << "Size of the map: " << myMap.size() << std::endl;  
    if (myMap.empty()) {  
        std::cout << "The map is empty." << std::endl;  
    } else {  
        std::cout << "The map is not empty." << std::endl;  
    }  
  
    return 0;  
}  
  
// 注意：上面的代码示例中，删除键为2的元素的部分是为了演示如何使用迭代器进行删除，但实际上在删除后立即尝试再次使用那个迭代器（it）是不安全的。  
// 在实际应用中，你应该在删除后立即停止使用该迭代器，或者重新通过find等方法获取有效的迭代器。
```
## <a id = "bitset">[bitset](#常见stl容器用法)</a>
#### 特点
有很多位的二进制数，支持位运算O(n/w机器位数)，不支持加减乘除，从右往左从低到高
#### 函数
count()返回bitset中1位的总数(size_t)
#### 示例
```cpp
#include <bitset>  
#include <iostream>  
  
int main() {  
    // 创建一个有8位的bitset，所有位初始化为0  
    std::bitset<8> myBitset;  
  
    // 设置特定的位  
    myBitset.set(0); // 设置最低位（索引0）为1  
    myBitset.set(2); // 设置索引为2的位为1  
  
    // 翻转特定的位  
    myBitset.flip(1); // 翻转索引为1的位  
  
    // 清除特定的位  
    myBitset.reset(2); // 将索引为2的位重置为0  
  
    // 访问特定的位  
    bool bit = myBitset.test(0); // 检查索引为0的位是否为1  
  
    // 输出bitset  
    std::cout << myBitset << std::endl; // 输出类似 10100000  
  
    // 转换为无符号整数  
    unsigned long value = myBitset.to_ulong(); // 注意：如果bitset表示的数值超出无符号整数的范围，将抛出std::overflow_error  
  
    return 0;  
}
```
