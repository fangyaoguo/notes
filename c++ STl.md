# 什么是STL
STL（Standard Template Library）是C++标准库的一部分，提供了一组通用的模板类和函数，用于实现常见的数据结构和算法。STL 的设计目标是提供一种高效、灵活、可复用的编程工具，使得开发人员能够更容易地编写高质量、高性能的代码。

STL 主要包括以下几个组件：

1. **容器（Containers）**：提供了一系列通用的数据结构，如向量（vector）、链表（list）、队列（queue）、栈（stack）、集合（set）、映射（map）等。这些容器可以存储不同类型的数据，并提供了许多操作和算法。

2. **迭代器（Iterators）**：允许以一种统一的方式对容器中的元素进行访问。迭代器可以被看作是一种指针，用于遍历容器中的元素。

3. **算法（Algorithms）**：提供了一系列常见的算法，如排序、搜索、拷贝等。这些算法可以应用于不同类型的容器，使得开发人员无需为不同的数据结构编写重复的算法代码。

4. **函数对象（Function Objects）**：允许将函数作为参数传递给算法，使得算法更加灵活。函数对象是类对象，实现了函数调用操作符 `operator()`。

5. **迭代器适配器（Iterator Adapters）**：提供了一些用于改变迭代器行为的工具，如反向迭代器、插入迭代器等。

使用STL，开发人员可以通过组合这些通用的模块，快速构建复杂的数据结构和实现各种算法，而无需从头开始编写大量的代码。STL的广泛应用使得C++成为一种强大的编程语言，适用于各种应用领域。
# 算法
### 二分查找算法
`upper_bound` 是 C++ 标准库中的一个算法，它用于在已排序的区间（通常是一个容器，比如向量或数组）中找到第一个大于某个值的元素的迭代器。在这个代码中，`upper_bound` 的目的是找到已排序的 `potions` 中第一个大于阈值 `t` 的元素。

函数原型如下：

```cpp
template<class ForwardIt, class T>
ForwardIt upper_bound(ForwardIt first, ForwardIt last, const T& value);
```

- `first` 和 `last` 表示要搜索的区间，这个区间应该是已排序的。
- `value` 是要进行比较的值。
- 返回的是一个迭代器，指向区间中第一个大于 `value` 的元素。

在上述代码中，`upper_bound` 的使用如下：

```cpp
upper_bound(potions.begin(), potions.end(), t)
```

这将在已排序的 `potions` 容器中找到第一个大于 `t` 的元素的迭代器。然后，通过计算这个迭代器与 `potions.begin()` 之间的距离，即 `upper_bound(potions.begin(), potions.end(), t) - potions.begin()`，可以得到小于等于 `t` 的元素的数量。

最终，`potions.size() - ...` 就是大于 `t` 的元素的数量，也就是成功的配对数量。
### 排序算法
`std::sort` 是 C++ 标准库中的排序算法，用于对容器中的元素进行排序。这个算法采用迭代器作为参数，并按升序（默认情况下）或指定的比较函数对元素进行排序。

函数原型如下：

```cpp
template <class RandomIt>
void sort(RandomIt first, RandomIt last);

template <class RandomIt, class Compare>
void sort(RandomIt first, RandomIt last, Compare comp);
```

- `first` 和 `last` 分别是表示待排序范围的迭代器，`first` 指向排序范围的起始位置，`last` 指向排序范围的末尾位置（不包括末尾元素）。
- `comp` 是一个可选的参数，用于指定排序时的比较函数，默认为使用 `<` 运算符进行比较。

例如，对一个整数向量进行排序可以这样使用：

```cpp
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> numbers = {5, 2, 9, 1, 5, 6};
    
    // 使用默认的升序比较函数
    std::sort(numbers.begin(), numbers.end());

    // 现在 numbers 中的元素已经按升序排列
    return 0;
}
```

如果需要按降序排序，可以使用自定义的比较函数：

```cpp
#include <algorithm>
#include <vector>

bool descending(int a, int b) {
    return a > b;
}

int main() {
    std::vector<int> numbers = {5, 2, 9, 1, 5, 6};

    // 使用自定义的比较函数
    std::sort(numbers.begin(), numbers.end(), descending);

    // 现在 numbers 中的元素已经按降序排列
    return 0;
}
```

`std::sort` 是一个高效的排序算法，通常采用的是快速排序或者归并排序的变体。排序之后，容器中的元素将按照指定的顺序排列，使得对数据进行查找等操作更加高效。


# 容器
### 介绍
C++ 标准模板库（STL）提供了多种容器，每种容器都有其独特的特性和适用场景。以下是 C++ STL 中的主要容器：

1. **序列容器（Sequence Containers）**：
   - **vector**：动态数组，支持快速随机访问。
   - **list**：双向链表，支持快速插入和删除。
   - **deque**：双端队列，支持快速在两端进行插入和删除。
   - **array**：静态数组，大小固定，支持快速随机访问。

2. **关联容器（Associative Containers）**：
   - **set**：有序的唯一元素集合。
   - **multiset**：有序的可重复元素集合。
   - **map**：有序的键-值对集合。
   - **multimap**：有序的键可重复的键-值对集合。

3. **无序关联容器（Unordered Associative Containers）**：
   - **unordered_set**：无序的唯一元素集合。
   - **unordered_multiset**：无序的可重复元素集合。
   - **unordered_map**：无序的键-值对集合。
   - **unordered_multimap**：无序的键可重复的键-值对集合。

4. **容器适配器（Container Adapters）**：
   - **stack**：基于 deque 或 vector 实现的堆栈。
   - **queue**：基于 deque 或 list 实现的队列。
   - **priority_queue**：基于 vector 实现的优先级队列。

5. **其他容器**：
   - **bitset**：固定大小的位集合。
   - **valarray**：数值数组，用于进行数值计算。

这些容器提供了不同的接口和性能特性，开发人员可以根据具体的需求选择合适的容器类型。容器之间可以相互转换，因此可以根据实际情况选择最适合问题的数据结构。

## vector
`std::vector` 是 C++ 标准模板库中的动态数组容器，提供了动态大小、连续存储的数组，并支持在数组末尾进行快速的插入和删除操作。以下是关于 `std::vector` 的基本用法：

#### 包含头文件
在使用 `std::vector` 之前，需要包含 `<vector>` 头文件：

```cpp
#include <vector>
```

#### 声明和初始化
可以使用以下几种方式声明和初始化 `std::vector`：

##### 1. 使用默认构造函数：
```cpp
std::vector<int> myVector;
```

##### 2. 指定初始大小并初始化所有元素：
```cpp
std::vector<int> myVector(5, 0); // 创建一个包含5个元素，每个元素都初始化为0的 vector
```

##### 3. 使用初始化列表：
```cpp
std::vector<int> myVector = {1, 2, 3, 4, 5};
```

#### 访问元素
可以使用下标运算符 `[]` 或者 `at()` 函数访问元素：

```cpp
std::vector<int> myVector = {10, 20, 30, 40, 50};

int firstElement = myVector[0];      // 访问第一个元素
int secondElement = myVector.at(1);  // 访问第二个元素
```

#### 插入和删除元素
##### 插入元素：
```cpp
std::vector<int> myVector = {1, 2, 3};

myVector.push_back(4);  // 在末尾插入元素
```

##### 删除元素：
```cpp
std::vector<int> myVector = {1, 2, 3, 4, 5};

myVector.pop_back();   // 删除末尾元素
```

#### 获取容器大小
可以使用 `size()` 函数获取容器的大小：

```cpp
std::vector<int> myVector = {1, 2, 3, 4, 5};

std::cout << "Size of vector: " << myVector.size() << std::endl;
```

#### 遍历容器
可以使用迭代器或者范围-based for 循环遍历 `std::vector`：

##### 使用迭代器：
```cpp
std::vector<int> myVector = {1, 2, 3, 4, 5};

for (std::vector<int>::iterator it = myVector.begin(); it != myVector.end(); ++it) {
    std::cout << *it << " ";
}
```

##### 使用范围-based for 循环：
```cpp
std::vector<int> myVector = {1, 2, 3, 4, 5};

for (int element : myVector) {
    std::cout << element << " ";
}
```

`std::vector` 提供了丰富的操作，使得它成为处理动态数组的强大工具。在编写 C++ 代码时，根据需求选择合适的容器是很重要的，而 `std::vector` 是一个常用的选择，特别是当需要动态调整数组大小时。
## list
`std::list` 是 C++ 标准模板库中的双向链表容器，它提供了在两端进行快速插入和删除操作的能力。以下是关于 `std::list` 的基本用法：

### 包含头文件
在使用 `std::list` 之前，需要包含 `<list>` 头文件：

```cpp
#include <list>
```

### 声明和初始化
可以使用以下几种方式声明和初始化 `std::list`：

#### 1. 使用默认构造函数：
```cpp
std::list<int> myList;
```

#### 2. 指定初始大小并初始化所有元素：
```cpp
std::list<int> myList(5, 0); // 创建一个包含5个元素，每个元素都初始化为0的 list
```

#### 3. 使用初始化列表：
```cpp
std::list<int> myList = {1, 2, 3, 4, 5};
```

### 访问元素
由于 `std::list` 是双向链表，它不支持使用下标直接访问元素。可以使用迭代器或者 `std::advance` 函数来访问元素。

#### 使用迭代器：
```cpp
std::list<int> myList = {10, 20, 30, 40, 50};

for (std::list<int>::iterator it = myList.begin(); it != myList.end(); ++it) {
    std::cout << *it << " ";
}
```

#### 使用 `std::advance` 函数：
```cpp
std::list<int> myList = {10, 20, 30, 40, 50};
std::list<int>::iterator it = myList.begin();

std::advance(it, 2); // 将迭代器移动到第三个元素
std::cout << *it << std::endl; // 输出第三个元素的值
```

### 插入和删除元素
#### 插入元素：
```cpp
std::list<int> myList = {1, 2, 3};

myList.push_back(4);    // 在末尾插入元素
myList.push_front(0);   // 在开头插入元素
```

#### 删除元素：
```cpp
std::list<int> myList = {1, 2, 3, 4, 5};

myList.pop_back();    // 删除末尾元素
myList.pop_front();   // 删除开头元素
```

### 获取容器大小
可以使用 `size()` 函数获取容器的大小：

```cpp
std::list<int> myList = {1, 2, 3, 4, 5};

std::cout << "Size of list: " << myList.size() << std::endl;
```

### 遍历容器
可以使用迭代器或者范围-based for 循环遍历 `std::list`：

#### 使用迭代器：
```cpp
std::list<int> myList = {1, 2, 3, 4, 5};

for (std::list<int>::iterator it = myList.begin(); it != myList.end(); ++it) {
    std::cout << *it << " ";
}
```

#### 使用范围-based for 循环：
```cpp
std::list<int> myList = {1, 2, 3, 4, 5};

for (int element : myList) {
    std::cout << element << " ";
}
```

`std::list` 在某些场景中比 `std::vector` 更适用，特别是当需要在容器中间或开头频繁插入或删除元素时。使用 `std::list` 可以避免在数组中插入或删除元素时涉及的元素移动操作。****