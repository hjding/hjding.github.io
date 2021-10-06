# cmake


### 把所有cmake缓存集中到build目录，便于删除

```
mkdir build
cd build
cmake ..
make
```

命令不区分大小写，参数和变量区分大小写

### CMake注释

单行注释：#注释内容
多行注释：可以使用括号来实现多行注释：
#[[多行注释
多行注释
多行注释]]

### CMake变量

CMake中所有的变量都是string类型，可以使用set() 和 unset() 命令来声明或者移除一个变量
变量的引用：${变量名}
#声明变量 set(变量名 变量值)
set(var 123)
#引用变量 message命令打印
message("var = ${var}")

### CMake列表（lists）

列表也是字符串，可以把列表看做是一个特殊的变量，这个变量有多个值。
语法格式：
set(列表名 值1 值2 ... 值n)
或
set(列表名 “值1;值2;...值n”)
列表的引用：
${列表名}
#声明列表 set set(列表名 值1 值2 ... 值n) 或 set(列表名 “值1;值2;...值n”)
set(list_var 1 2 3 4 5)
#或者
set(list_var "1;2;3;4;5")
#打印列表
message("list_var = ${list_var}")

### CMake流程控制

#### 【操作符】

一元：EXIST, COMMAND, DEFINED
二元：EQUAL, LESS, LESS_EQUAL, GRATER, GRATER_EQUAL, STR... VERSION... MATCHES
逻辑：NOT, AND, OR

#### 【布尔常量值】

true: 1, ON, YES, TRUE, Y, 非0的值
false: 0, OFF, NO, FALSE, N, IGNORE, NOTFOUND, 空字符串, 以NOTFOUND结尾的字符串

#### 【条件命令】

```cmake
if (表达式)
COMMAND(ARGS...)
elseif(表达式)
COMMAND(ARGS...)
else(表达式)
COMMAND(ARGS...)
endif(表达式)
```



#### 【循环命令】

```cmake
while(表达式)
COMMAND(ARGS...)
endwhile(表达式)
```


break() 命令可以跳出整个循环， continue() 可以跳出当前循环。

#### 【循环遍历】

> foreach(循环变量 参数1 参数2... 参数N)
>
> COMMAND(ARGS...)
>
> endforeach(循环变量)
>
> 每次迭代设置循环遍历为参数。
>
> foreach也支持 break() 和 continue() 命令跳出循环。

RANGE 4 表示0到4

```cmake
foreach(item RANGE 4)
message("item = ${item}")
endforeach(item)
```

循环范围从 start 到 stop， 循环增量为step

```cmake
foreach(循环变量 RANGE start stop step)
COMMAND(ARGS...)
endforeach(循环变量)

foreach支持对列表的循环

foreach(循环遍历 IN LISTS 列表)
COMMAND(ARGS...)
endforeach(循环变量)
```

#### CMake自定义函数命令

```cmake
function(<name>[arg1 [arg3 [arg3...]]])
COMMAND(ARGS...)
endfunction(<name>)
函数命令调用格式
name(参数列表)
```



#### CMake自定义宏命令

```cmake
macro(<name>[arg1 [arg3 [arg3...]]])
COMMAND(ARGS...)
endmacro(<name>)
宏定义调用格式
name(实参列表)
函数命令有自己的作用域，宏的作用域和调用者的作用域是一样的。
```



#### CMake中变量的作用域

全局层：cache变量，在整个项目范围可见，一般在set定义变量式，指定CACHE参数就能定义cache变量。
目录层：在当前目录CMakeLists.txt中定义，以及在该文件包含的其他Cmake源文件中定义的变量。
函数层：在命令函数中定义的变量，属于函数作用域内的变量。



```cmake
##myprint
#指定CMake编译最低要求版本
CMAKE_MINIMUM_REQUIRED(VERSION 3.11)

#给项目命名
PROJECT(MYPRINT)

#收集c/c++文件并赋值给变量SRC_LIST_CPP ${PROJECT_SOURCE_DIR}代表区当前项目录
FILE(GLOB SRC_LIST_CPP ${PROJECT_SOURCE_DIR}/src/*.cpp)
FILE(GLOB SRC_LIST_C ${PROJECT_SOURCE_DIR}/src/*.c)

#指定头文件目录
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/include)

#指定生成库文件的目录
SET(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#去变量SRC_LIST_CPP 与SRC_LIST_C 指定生成libmyprint 动态库 默认生成静态库 SHARED指定生成库类型为动态库
ADD_LIBRARY(myprint SHARED ${SRC_LIST_CPP} ${SRC_LIST_C})



##hello
#指定CMake编译最低要求版本
CMAKE_MINIMUM_REQUIRED(VERSION 3.11)

#指定项目名称
PROJECT(HELLO)

#将hello.cpp 赋值给SOURCE 变量
SET(SOURCE ${PROJECT_SOURCE_DIR}/src/hello.cpp)

#指定头文件目录
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/../test/include)

#指定链接库文件目录
LINK_DIRECTORIES(${PROJECT_SOURCE_DIR}/../test/lib)

#指定hello 链接库myprint
TARGET_LINK_LIBRARIES(hello myprint)

#将hello.cpp生成可执行文件hello 
ADD_EXECUTABLE(hello ${SOURCE})
```


