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
### 二分查找算法 [[二分]]
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

[[运算符重载]]
当使用 `std::sort` 对数组 `p` 进行排序时，排序的规则由结构体中的 `<` 运算符定义。在这里，`<` 运算符是结构体 `book` 中的一个成员函数，它被重载用于确定两个 `book` 对象之间的大小关系。

让我们再次看一下 `book` 结构体中的 `<` 运算符的定义：

```cpp
bool operator < (const book & u) const
{
    if (h == u.h && s == u.s) return w < u.w;
    if (h == u.h) return s < u.s;
    return h < u.h;
}
```

这个运算符定义了 `book` 对象之间的“小于”关系。在排序过程中，`std::sort` 会多次调用这个运算符来比较数组中的元素。这个运算符的逻辑按照以下规则进行：

1. 如果两个书的高度 `h` 和大小 `s` 都相等，那么比较它们的重量 `w`，返回 `w < u.w` 的结果。
2. 如果两个书的高度 `h` 相等，但大小 `s` 不相等，那么比较它们的大小 `s`，返回 `s < u.s` 的结果。
3. 如果两个书的高度 `h` 不相等，直接比较它们的高度 `h`，返回 `h < u.h` 的结果。

这样定义的比较规则会在排序时决定数组中元素的相对顺序。在这个例子中，`std::sort` 将根据这个规则，按照递减的高度、递增的大小、递增的重量的顺序对数组 `p` 进行排序。

### 去重算法
1. 在C++中，`std::unique`是一个算法，用于在容器中去除相邻的重复元素。它并不真正删除重复元素，而是将它们移到容器的末尾，并返回一个指向新的逻辑尾部的迭代器。这样，容器的前部就包含了不重复的元素，而后部包含了重复的元素。

以下是`std::unique`的基本用法：

```cpp
#include <algorithm>
#include <vector>
#include <iostream>

int main() {
    std::vector<int> vec = {1, 2, 2, 3, 4, 4, 5};

    // 使用 std::unique 去除相邻的重复元素
    auto newEnd = std::unique(vec.begin(), vec.end());

    // 删除重复元素后的容器大小不变，但重复元素移到了末尾
    vec.erase(newEnd, vec.end());

    // 输出不重复的元素
    for (const auto& element : vec) {
        std::cout << element << " ";
    }

    return 0;
}
```

在这个例子中，`std::unique`会将相邻的重复元素移动到容器末尾，并返回指向新逻辑尾部的迭代器。然后，可以使用容器的`erase`方法删除重复元素的部分。

需要注意的是，`std::unique`只能去除相邻的重复元素，如果要去除整个容器中的重复元素，通常需要先对容器进行排序（使用`std::sort`），然后再使用`std::unique`。
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
## set
在C++中，`std::set`是一个标准库中提供的集合容器，它是一个有序的容器，其中的元素按照升序排序。`std::set`是基于红黑树（Red-Black Tree）实现的，这使得插入、删除和查找操作的平均时间复杂度为O(log n)。

以下是关于`std::set`的一些重要特性和用法：

1. **有序性：** `std::set`中的元素是有序的，默认按照元素的升序进行排序。这个有序性使得`std::set`很适合需要按照顺序访问元素的场景。

2. **唯一性：** `std::set`中不允许重复的元素。每个元素都是唯一的，如果插入一个已经存在的元素，插入操作将被忽略。

3. **插入和删除：** 插入和删除操作都具有较高的效率，平均时间复杂度为O(log n)。

4. **查找：** 查找操作同样具有较高的效率，平均时间复杂度为O(log n)。

5. **迭代器：** `std::set`提供了正向迭代器，可以用于遍历容器中的元素。

6. **使用示例：**
    ```cpp
    #include <iostream>
    #include <set>

    int main() {
        // 创建一个set
        std::set<int> mySet;

        // 插入元素
        mySet.insert(3);
        mySet.insert(1);
        mySet.insert(4);
        mySet.insert(2);

        // 遍历元素
        for (const auto& element : mySet) {
            std::cout << element << " ";
        }
        // 输出：1 2 3 4

        // 查找元素
        auto it = mySet.find(3);
        if (it != mySet.end()) {
            std::cout << "\nElement found: " << *it << std::endl;
        }

        // 删除元素
        mySet.erase(2);

        // 输出删除元素后的set
        for (const auto& element : mySet) {
            std::cout << element << " ";
        }
        // 输出：1 3 4

        return 0;
    }
    ```
    上述示例演示了如何创建`std::set`，插入、遍历、查找和删除元素。

## priority_queue
`priority_queue`（优先队列）是C++标准模板库（STL）中的一个容器适配器，用于实现具有优先级的队列。它是基于堆（heap）数据结构实现的，通常用于需要按照特定顺序处理元素的场景。

### 特点和用途：
1. **优先级队列：** `priority_queue` 会按照元素的优先级进行排序，每次访问或弹出的都是具有最高优先级的元素。
  
2. **底层实现：** 通常使用堆来实现。默认情况下，`priority_queue` 是一个最大堆（大顶堆），意味着最大的元素总是位于队列的最前面。你也可以通过指定比较函数来创建最小堆。

3. **接口与队列相似：** `priority_queue` 提供了类似于队列（FIFO）的接口，例如 `push()`（入队）、`pop()`（出队）、`top()`（访问队首元素）等。

### 基本操作：

- **构造：** `std::priority_queue<T>` 创建一个类型为 T 的优先队列，默认是最大堆；也可以通过提供比较函数来创建最小堆。

  ```cpp
  #include <queue>
  std::priority_queue<int> max_heap; // 默认是最大堆
  std::priority_queue<int, std::vector<int>, std::greater<int>> min_heap; // 最小堆
  ```

- **插入：** 使用 `push()` 方法将元素插入队列。

  ```cpp
  max_heap.push(10);
  max_heap.push(20);
  ```

- **访问队首元素：** 使用 `top()` 方法获取队首元素。

  ```cpp
  int top_element = max_heap.top(); // 获取最大元素
  ```

- **弹出队首元素：** 使用 `pop()` 方法弹出队首元素。

  ```cpp
  max_heap.pop(); // 移除最大元素
  ```

### 例子：

```cpp
#include <iostream>
#include <queue>

int main() {
    std::priority_queue<int> max_heap;

    max_heap.push(30);
    max_heap.push(10);
    max_heap.push(20);

    std::cout << "Top element: " << max_heap.top() << std::endl; // Output: 30

    max_heap.pop(); // Remove the top element

    std::cout << "Top element after pop: " << max_heap.top() << std::endl; // Output: 20

    return 0;
}
```

这是一个简单的例子，说明了如何使用 `priority_queue` 进行基本操作。需要注意，`priority_queue` 并没有提供迭代器，因此无法直接遍历其中的元素。
### 最小堆 
要创建最小堆，你需要使用 `priority_queue` 的第二和第三个参数来指定底层容器类型和比较函数。

在默认情况下，`priority_queue` 使用 `std::less` 作为比较函数，这将导致创建最大堆。为了创建最小堆，你应该使用 `std::greater` 作为比较函数。以下是一个创建最小堆的示例：

```cpp
#include <iostream>
#include <queue>
#include <vector>

int main() {
    // 使用 std::greater<int> 作为比较函数，创建最小堆
    std::priority_queue<int, std::vector<int>, std::greater<int>> min_heap;

    min_heap.push(30);
    min_heap.push(10);
    min_heap.push(20);

    std::cout << "Top element: " << min_heap.top() << std::endl; // Output: 10

    min_heap.pop(); // 移除最小元素

    std::cout << "Top element after pop: " << min_heap.top() << std::endl; // Output: 20

    return 0;
}
```

在这个例子中，`std::greater<int>` 作为比较函数，确保了最小的元素位于队首。这样，你就创建了一个最小堆。