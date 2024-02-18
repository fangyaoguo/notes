## 前言

[字符串操作](https://so.csdn.net/so/search?q=%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%93%8D%E4%BD%9C&spm=1001.2101.3001.7020)是各种算法题中的常客，很多数据常常以字符串形式给出，其中有的需要自己转化成整数，而一些整型数据有时转换成字符串处理起来更加方便，比如判断一个整数是否是回文数，所以字符串和整数的转换是一些问题处理的基础步骤，`C++` 在处理这类问题时并不像 `Python` 那样方便，但是也有许多方法能够实现，为了今后查找方便，整理如下。

## int 转 string

### 通过 std::to_string() 函数转换

```cpp
#include <iostream>

int main()
{
    int num = 123;
    std::cout << std::to_string(num);
    return 0;
}
```

这种方式在 C++11 中才能使用，编译时记得加上 `--std=c++11` 的选项

### 通过 ostringstream 转换

```cpp
#include <iostream>
#include <sstream>

int main()
{
    int num = 123;
    std::ostringstream ss;
    ss << num;
    std::cout << ss.str();
    return 0;
}
```

这是一种通过字符流的方式将整数转换成字符串，这种方式在C++11之前也可以使用

### 通过 sprintf 转换

```cpp
#include <stdio.h>

int main()
{
    int num = 123;
    char buffer[256];
    sprintf(buffer, "%d", num);

    printf("%s", buffer);
    return 0;
}
```

这是一种C语言中的转换方式，`sprintf` 也可以换成更安全的 `snprintf` 函数

## string 转 int

### 通过 istringstream 转换

```cpp
#include <iostream>
#include <sstream>

int main()
{
    std::string str = "668";
    int num = 0;

    std::istringstream ss(str);
    ss >> num;

    std::cout << num;
    return 0;
}
```

使用 `istringstream` 可以从字符流中读取整数，与 `ostringstream` 是一种相反的操作

### 使用 sscanf 来转化

```cpp
#include <iostream>
#include <stdio.h>

int main()
{
    std::string str = "668";
    int num = 0;

    sscanf(str.c_str(), "%d", &num);
    std::cout << num;
    return 0;
}
```

注意 `sscanf` 函数的第一个参数类型是 `const char *`，`string`类型的参数需要转换一下

### 使用 atoi 转换

```cpp
#include <iostream>
#include <stdlib.h>

int main()
{
    std::string str = "668";
    std::cout << atoi(str.c_str());
    return 0;
}
```

`atoi` 函数的头文件是 `stdlib.h`，同样是一个C语言中的函数

## 总结

- `itoa` 不是c语言标准函数，在跨平台的整数转字符串的代码中不要使用这个函数
- `atoi` 是一个标准函数，需要将它和 `itoa` 区别开来，这一点很容易记混的
- 如果是在C++环境中进行转换，推荐使用 `stringstream` 字符流的形式和 `to_string` 函数