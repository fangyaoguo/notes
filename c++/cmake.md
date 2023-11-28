`cmake_minimum_required(VERSION 3.15)`指定使用cmake的最低版本号
`project(name)`设置项目名称
`add_executable(name example.cpp)`用来生成可执行文件，需要指定生成可执行文件的名称和相关源文件。
`cmake -G"MinGW Makefiles" ..`用`..`表示上层目录
`cmake --build .` `--build` 指定编译生成的文件存放目录，其中就包括可执行文件，`.` 表示存放到当前目录。
指定了项目名后，后面可能会有多个地方用到这个项目名，如果更改了这个名字，就要改多个地方，比较麻烦，那么可以使用 `${PROJECT_NAME}` 来表示项目名。
我们也可以用一个变量来表示这多个源文件：```cmake set(SRC_LIST a.cpp b.cpp c.cpp)
```
set(CMAKE_CXX_STANDARD 23) //设置c++标准
set(INC_DIR ./include)  
set(SRC_DIR ./src)  
set(LINK_DIR ./lib)  
  
include_directories(${INC_DIR})  //设置include
  
link_directories(${LINK_DIR})  // 设置lib

target_link_libraries(${PROJECT_NAME} libyaml-cpp.dll) // 链接lib
```