# **隐式调用****DLL

静态加载DLL需要提供.h.dll文件，假设需要加载的DLL文件名为MyDll.dll，静态加载DLL步骤如下：

（1）将MyDll.dll拷到目标工程(需调用MyDll.dll的工程)的Debug目录下；

（3）将MyDll.h(包含输出函数的定义)拷到目标工程(需调用MyDll.dll的工程)目录下；

（5）在目标工程Head Files加入MyDll.h文件；
 (4)  在cmake项目中链接库
（6）在目标工程(*.cpp,需要调用MyDll.dll中的接口)中包含头文件，即#include “MyDll.h”，然后在该*.cpp中可直接调用MyDll.h中的接口。
# 显式调用
DLL不需要依赖.h和.lib文件，仅需要将.dll文件拷贝到应用程序所在目录下。

动态加载需主要用到LoadLibrary（加载DLL）、GetProcAddress（获得DLL中API函数的地址）、FreeLibrary（释放DLL）这几个系统函数。

LoadLibrary() 函数作用是将指定的可执行模块映射到调用进程的地址空间，如果调用成功， LoadLibrary() 函数将返回所加载的那个模块的句柄。当获取到动态链接库模块的句柄后，接下来就要想办法获取DLL导出函数的地址，这可以通过调用 GetProcAddress() 函数来实现。当DLL文件中的函数不再使用或程序结束时，需要使用FreeLibrary（）函数对其进行释放。具体使用示例如下：

加载DLL：
```cpp
#include <windows.h>

HINSTANCE hDllInst = LoadLibrary(“MyDll.dll”);
```
1、声明头文件<windows.h>，说明我想用windows32方法来加载和卸载DLL
2、然后用typedef定义一个指针函数类型.typedef void(*fun) //这个指针类型，要和你调用的函数类型和参数保持一致

3、定一个句柄实例，用来取DLL的实例地址。HINSTANCE hdll；

格式为hdll=LoadLibrary（“DLL地址”）；你封装的ｄｌｌ路径名称

要配置-属性-常规里面把默认字符集“unicode”改成支持多字符扩展。

4、取的地址要判断，定义一个函数指针，用来获取你要用的函数地址。

然后通过Win32 API 函数GetProcAdress来获取函数的地址，参数是DLL的句柄和你要调用的函数名：比如：FUN=(fun)GetProcAdress(hdll,"Ｍｙ＿ａｄｄ");

要判断要函数指针是否为空，如果没取到要求的函数，那么要释放句柄。

6、然后通过函数指针来调用函数。

7、调用结束后，就释放句柄FreeLibrary(hdll);
1. **静态加载与动态加载区别**

（1）加载时间：静态加载发生在程序运行之前，故如果缺少dll文件，程序运行不起来。动态加载发生在程序运行过程中（由编程者决定何时加载），不会因为缺少dll，导致整个程序运行不起来。如果程序体积较大，功能较为复杂，静态加载会导致程序启动时间长。而动态加载可将较大的程序分开加载的，程序运行时只需要将主程序载入内存，程序启动快。

（2）依赖文件：静态加载需要.lib和.dll文件，动态加载只需要.dll文件。

（3）占用内存： 静态加载占用内存较大。静态加载可 以在需要的时候用LoadLibrary进行加载，在不需要的时候用FreeLibrary进行卸载，这样可以不必占用内存。

（4）使用情况：静态加载使用简单方便。动态加载使用复杂一些，需要显示获取函数地址。