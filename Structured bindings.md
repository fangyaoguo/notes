Structured bindings 是 C++17 中的一个特性，它允许你将结构体或元组中的成员变量分别绑定到不同的变量上，从而更方便地访问结构体或元组的成员。

下面是一个示例，演示了如何使用 structured bindings：

```cpp
#include <iostream>
#include <tuple>
using namespace std;

struct Point {
    int x;
    int y;
};

int main() {
    Point p = {3, 4};

    // 使用 structured bindings 将结构体成员变量绑定到不同的变量上
    auto [x, y] = p;

    cout << "x: " << x << ", y: " << y << endl;

    return 0;
}
```

在上面的示例中，`Point` 结构体有两个成员变量 `x` 和 `y`，我们可以使用 structured bindings 将它们分别绑定到 `x` 和 `y` 变量上，然后输出它们的值。

这样，structured bindings 提供了一种更简洁、更直观的方式来访问结构体或元组中的成员。