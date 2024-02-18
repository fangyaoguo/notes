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
`lower_bound` 和 `upper_bound` 都是 C++ 标准模板库（STL）中的算法，用于在有序序列中进行二分查找。它们的主要区别在于：

1. **返回值：**
   - `lower_bound` 返回的是在序列中第一个不小于指定值的元素的位置（迭代器）。
   - `upper_bound` 返回的是在序列中第一个大于指定值的元素的位置（迭代器）。

2. **定位元素：**
   - `lower_bound` 定位的是不小于指定值的第一个元素，包括相等的情况。
   - `upper_bound` 定位的是大于指定值的第一个元素。

在代码中，你可以看到使用 `lower_bound` 来找到第一个不小于 `target` 的位置：

```cpp
auto bound = lower_bound(sums.begin(), sums.end(), target);
```

如果你希望找到大于某个值的第一个元素的位置，你可以使用 `upper_bound`：

```cpp
auto bound = upper_bound(sums.begin(), sums.end(), target);
```

总的来说，两者都是在有序序列中进行二分查找的工具，只是定位的元素条件略有不同。
## distince
`std::distance` 是 C++ 标准库中的一个算法，用于计算两个迭代器之间的距离。它的定义如下：

```cpp
template<class InputIt>
typename std::iterator_traits<InputIt>::difference_type
distance(InputIt first, InputIt last);
```

其中，`InputIt` 是迭代器的类型，`first` 是起始迭代器，`last` 是结束迭代器。返回值是两个迭代器之间的距离，以 `difference_type` 类型表示。

在使用时，`std::distance` 可以用于计算两个迭代器之间的元素个数。例如：

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    
    auto first = vec.begin();
    auto last = vec.end();

    std::ptrdiff_t dist = std::distance(first, last);

    std::cout << "Distance: " << dist << std::endl;

    return 0;
}
```

在你的代码中，`std::distance(nums.begin() + i - 1, Iterator)` 用于计算从 `nums.begin() + i - 1` 到 `Iterator` 之间的元素个数，即两个迭代器之间的距离。在这里，这个距离表示了子数组的长度。

由于 `std::distance` 返回 `std::ptrdiff_t` 类型，而你想将其转换为 `int` 类型，需要小心处理可能的溢出问题，以避免运行时错误。在前面的代码修改中，使用了 `std::min` 函数来确保距离不会溢出 `INT_MAX`。
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
myVector.insert(myVector.begin()+2,2)//向索引为2的地方插入2
```

##### 删除元素：
```cpp
std::vector<int> myVector = {1, 2, 3, 4, 5};

myVector.pop_back();   // 删除末尾元素
myVector.erase(myVector.begin()+2)//删除索引为2的元素
.clear()//delete all
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
### 使用
1.去重
2.存在性问题
3.存图
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
## queue
以下是`std::queue`的一些常用成员函数和特性：

1. **push()：** 将元素加入队列的尾部。
    
    cppCopy code
    
    `std::queue<int> myQueue; myQueue.push(10); myQueue.push(20);`
    
2. **pop()：** 移除队列头部的元素。
    
    cppCopy code
    
    `myQueue.pop();`
    
3. **front()：** 返回队列头部的元素，但不会移除它。
    
    cppCopy code
    
    `int frontElement = myQueue.front();`
    
4. **back()：** 返回队列尾部的元素，但不会移除它。
    
    cppCopy code
    
    `int backElement = myQueue.back();`
    
5. **empty()：** 检查队列是否为空。
    
    cppCopy code
    
    `if (myQueue.empty()) {     // 队列为空 }`
    
6. **size()：** 返回队列中元素的数量。
    
    cppCopy code
    
    `int queueSize = myQueue.size();`
    

STL队列的使用示例：

cppCopy code

`#include <iostream> #include <queue>  int main() {     std::queue<int> myQueue;      myQueue.push(10);     myQueue.push(20);     myQueue.push(30);      while (!myQueue.empty()) {         std::cout << myQueue.front() << " ";         myQueue.pop();     }      return 0; }`

在这个示例中，元素10首先被加入队列，然后是20和30。在循环中，队列头部的元素被打印并移除，直到队列为空。输出将是：`10 20 30`。
## stack
在STL中，栈是由模板类`std::stack`表示的。这个模板类提供了一组成员函数，使得栈的使用变得非常方便。以下是`std::stack`的一些重要成员函数和特性：

1. **push()：** 将元素压入栈顶。
    
    cppCopy code
    
    `std::stack<int> myStack; myStack.push(10); myStack.push(20);`
    
2. **pop()：** 从栈顶弹出一个元素。
    
    cppCopy code
    
    `myStack.pop();`
    
3. **top()：** 返回栈顶元素的引用，但不会将其从栈中移除。
    
    cppCopy code
    
    `int topElement = myStack.top();`
    
4. **empty()：** 检查栈是否为空。
    
    cppCopy code
    
    `if (myStack.empty()) {     // 栈为空 }`
    
5. **size()：** 返回栈中元素的数量。
    
    cppCopy code
    
    `int stackSize = myStack.size();`
    

STL栈的使用示例：

cppCopy code

`#include <iostream> #include <stack>  int main() {     std::stack<int> myStack;      myStack.push(10);     myStack.push(20);     myStack.push(30);      while (!myStack.empty()) {         std::cout << myStack.top() << " ";         myStack.pop();     }      return 0; }`

在这个示例中，元素30首先被压入栈，然后20，最后10。在循环中，栈顶元素被打印并弹出，直到栈为空。输出将是：`30 20 10`。
## map
TL（Standard Template Library）中的`std::map`是一种关联容器，实现了键值对的存储和检索。它基于红黑树（Red-Black Tree）实现，因此它的查找、插入和删除操作的平均时间复杂度是对数级别的，使得它非常高效。`std::map`中的键和值可以是任意类型，但键必须是可比较的。

以下是`std::map`的一些常用成员函数和特性：

1. **insert()：** 将键值对插入`std::map`。
    
    cppCopy code
    
    `std::map<int, std::string> myMap; myMap.insert(std::make_pair(1, "One")); myMap.insert(std::make_pair(2, "Two"));`
    
2. **emplace()：** 在C++11及更高版本中，使用`emplace`可以更高效地插入元素。
    
    cppCopy code
    
    `myMap.emplace(3, "Three");`
    
3. **find()：** 查找指定键的元素，返回指向该元素的迭代器，如果没有找到，则返回`end()`。
    
    cppCopy code
    
    `auto it = myMap.find(2); if (it != myMap.end()) {     // 找到了     std::cout << "Value for key 2: " << it->second << std::endl; } else {     // 没找到     std::cout << "Key 2 not found." << std::endl; }`
    
4. **erase()：** 删除指定键的元素。
    
    cppCopy code
    
    `myMap.erase(1);`
    
5. **empty()：** 检查`std::map`是否为空。
    
    cppCopy code
    
    `if (myMap.empty()) {     // map为空 }`
    
6. **size()：** 返回`std::map`中键值对的数量。
    
    cppCopy code
    
    `int mapSize = myMap.size();`
    
7. **operator[]：** 访问指定键的值，如果键不存在，则插入一个具有默认值的新元素。
    
    cppCopy code
    
    `std::cout << "Value for key 3: " << myMap[3] << std::endl;`
    

`std::map`中的元素按键的升序排列。如果需要按降序排列，可以使用`std::map`的逆迭代器或者考虑使用`std::map`的近亲`std::unordered_map`（基于哈希表实现）。  
## unordered_map
STL（Standard Template Library）中的`std::unordered_map`是C++中的一个关联容器，实现了无序（哈希）映射。它提供了一种快速查找和插入键-值对的方法。`std::unordered_map`使用哈希表来实现，具有平均O(1)的时间复杂度，但不保证元素的顺序。

以下是`std::unordered_map`的一些重要特性和成员函数：

1. **插入元素：**
    
    cppCopy code
    
    `#include <unordered_map>  std::unordered_map<int, std::string> myMap; myMap.insert({1, "one"}); myMap[2] = "two";`
    
2. **访问元素：**
    
    cppCopy code
    
    `std::string value = myMap[1]; // 返回键为1的值`
    
3. **查找元素：**
    
    cppCopy code
    
    `auto it = myMap.find(2); if (it != myMap.end()) {     // 找到了键为2的元素 }`
    
4. **删除元素：**
    
    cppCopy code
    
    `myMap.erase(1); // 删除键为1的元素`
    
5. **遍历元素：**
    
    cppCopy code
    
    `for (const auto& pair : myMap) {     std::cout << pair.first << ": " << pair.second << std::endl; }`
    
6. **大小和空判断：**
    
    cppCopy code
    
    `if (myMap.empty()) {     // unordered_map为空 } std::size_t size = myMap.size(); // 返回元素的数量`
    
7. **桶操作：**
    
    cppCopy code
    
    `std::size_t numBuckets = myMap.bucket_count(); // 返回桶的数量`
    
8. **哈希策略：**
    
    cppCopy code
    
    `myMap.hash_function(); // 返回哈希函数对象`
    

`std::unordered_map`允许存储键和值的任何类型，只要这些类型支持哈希操作和比较操作。对于自定义类型，可以通过提供自定义的哈希函数和相等性比较函数来支持`std::unordered_map`的使用。
## string
以下是`std::string`类的一些常用操作，包括构造、访问、修改、比较、查找和其他操作：

1. **构造和初始化：**
    
    cppCopy code
    
    std::string();                // 空字符串   
    std::string(const char*);     // 通过C风格字符串初始化   
    std::string(const std::string&); // 通过另一个字符串初始化   
    std::string(size_t, char);    // 重复n次的字符初始化   
    std::string(const char*, size_t); // 初始化为C风格字符串的前n个字符`
    
2. **赋值和拼接：**
    
    std::string& operator=(const std::string&); // 赋值  
     std::string& operator=(const char*);        // 赋值给C风格字符串   
     std::string& operator+=(const std::string&); // 拼接   
     std::string& operator+=(const char*);        // 拼接C风格字符串`
    
3. **访问字符：**
    
    
    char& operator[](size_t);     // 访问字符  
     char& at(size_t);              // 访问字符，带边界检查   
     char& front();                 // 获取第一个字符   
     char& back();                  // 获取最后一个字符`
    
4. **字符串迭代器：**
    
 
    
    iterator begin();              // 返回指向第一个字符的迭代器  
     iterator end();                // 返回指向尾部的迭代器`
    
5. **修改字符串：**
    

    
    void append(const std::string&); // 追加字符串   
    void append(const char*);        // 追加C风格字符串   
    void erase(size_t pos, size_t len); // 删除子字符串   
    void clear();                   // 清空字符串`
    
6. **比较字符串：**
    
    
    bool operator == (const std::string&) const;   // 相等比较 bool      
     operator!=(const std::string&) const; // 不等比较
      bool operator<(const std::string&) const;  // 小于比较
    
7. **查找和替换：**
    

    
    size_t find(const std::string&);   // 查找子字符串 void  如果找不到就返回string::npos  
     replace(size_t pos, size_t len, const std::string&); // 替换子字符串
8. **字符串长度和空检查：**
    

    
    size_t length() const;            // 返回字符串长度   
    bool empty() const;               // 检查字符串是否为空`
    
9. **转换为C风格字符串：**
    
 
    
    `const char* c_str() const;        // 转换为const char*`
    
10. **子字符串提取：**
    
    `std::string substr(size_t pos, size_t len); // 提取子字符串`
    11. 颠倒字符串
    `reserve(s.begin(),s.end())`
    

这里列举的只是一些常用的`std::string`操作，实际上`std::string`提供了更多的成员函数和操作符，以满足不同的字符串处理需求。详细的信息可以查阅C++的文档。
## valarray
`std::valarray` 是 C++ 标准库中提供的一个用于处理数值数组的类模板。它位于 `<valarray>` 头文件中，并提供了一组用于执行数学运算的成员函数和运算符重载。`valarray` 主要设计用于进行数值计算，提供了一些性能优化，以便在一些情况下可以更高效地执行操作。

以下是一些 `std::valarray` 的主要特性和用法：

1. **数学运算：** `valarray` 提供了许多数学运算的成员函数，例如加法、减法、乘法、除法等。这些运算符重载使得可以直观地对数组进行操作。

    ```cpp
    #include <valarray>
    #include <iostream>

    int main() {
        std::valarray<int> array1 = {1, 2, 3, 4, 5};
        std::valarray<int> array2 = {10, 20, 30, 40, 50};

        std::valarray<int> result = array1 + array2;

        for (const auto& element : result) {
            std::cout << element << " ";
        }

        return 0;
    }
    ```

2. **数学函数：** `valarray` 提供了一些常见的数学函数，如 `sin`、`cos`、`exp` 等，以便对数组的每个元素进行逐一计算。

    ```cpp
    #include <valarray>
    #include <iostream>
    #include <cmath>

    int main() {
        std::valarray<double> angles = {0.0, 1.0, 2.0, 3.0, 4.0};
        std::valarray<double> sine_values = std::sin(angles);

        for (const auto& value : sine_values) {
            std::cout << value << " ";
        }

        return 0;
    }
    ```

3. **切片操作：** `valarray` 支持类似 Python NumPy 的切片操作，允许你对数组的子集执行操作。

    ```cpp
    #include <valarray>
    #include <iostream>

    int main() {
        std::valarray<int> array = {1, 2, 3, 4, 5};

        // 对数组的前三个元素进行平方操作
        std::valarray<int> result = array[std::slice(0, 3, 1)] * array[std::slice(0, 3, 1)];

        for (const auto& element : result) {
            std::cout << element << " ";
        }

        return 0;
    }
    ```

4. **性能优化：** `valarray` 的设计旨在允许对数组执行一些优化，以提高数值计算的性能。这可能涉及到硬件优化、并行计算等方面的考虑。

请注意，虽然 `std::valarray` 提供了一些方便的数值计算功能，但在实际应用中，由于缺乏一些高级特性，一些开发者更喜欢使用其他库，如 Eigen 或 Boost 数组库，以满足更复杂的数学计算需求。