应该这样写：

```cpp
int (*func())[20]
{
    static int b[20];
    return &b;
}
```

这个时候，可以这样理解：函数名就相当于一个变量(包括函数名里面的括号在内的一个变量)。

当然：C++11的标准允许我们这样写：

```cpp
auto func()->int(*)[]
{
    static int arr[];
        return &arr;
}
```

这样我们就可以在其他函数比如主函数里面修改或者捣鼓里面的值啦。

但是，一般不会定义太多static类型的数据，所以往往都是在堆区定义数据并返回指针：

```cpp
int* func(){
    int* arr=new int[10];
    return arr;
}
```

如果你知道 `decltype` 的话，在全局区定义的数据类型被用上，那多是一件美事：

```cpp
std::string arr[20];

decltype(arr) *func()
{
    return &arr;
}
```

对了，在比如主函数调用是这样调用的喔：

```cpp
int main(){
    std::string (*p)[20] =func(); //这个要好好理解喔！
    for(int i=0;i<20;i++)
    {
        std::cout<<(**p)++<<" ";
    }
        std::cout<<std::endl;

}
```