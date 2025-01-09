## 初识C语言


### 1. C语言简介

> C语言是一门通用计算机编程语言，广泛应用于底层开发。C语言的设计目标是提供一种能以简易的方式编译、处理低级存储器、产生少量的机器码以及不需要任何运行环境支持便能运行的编程语言。

> 尽管C语言提供了许多低级处理的功能，但仍然保持着良好跨平台的特性，以一个标准规格写出的C语言程序可在许多电脑平台上进行编译，甚至包含一些嵌入式处理器（单片机或称MCU）以及超级电脑等作业平台。

> 二十世纪八十年代，为了避免各开发厂商用的C语言语法产生差异，由美国国家标准局为C语言制定了一套完整的美国国家标准语法，称为ANSI C，作为C语言最初的标准。 [1] 目前 2011 年 12 月 8 日，国际标准化组织（ISO）和国际电工委员会（IEC）发布的 C标准 是C语言的第三个官方标准，也是C语言的最新标准，该标准更好的支持了汉字函数名和汉字标识符，一定程度上实现了汉字编程。

> C语言是一门面向过程的计算机编程语言，与C++，Java等面向对象的编程语言有所不同。

> 其编译器主要有Clang、 GCC 、WIN-TC、SUBLIME、 MSVC 、Turbo C等。



### 2. C语言程序结构

C 程序主要包括以下部分：

- 预处理器指令
- 函数
- 变量
- 语句 & 表达式
- 注释

```c
#include <stdio.h>

int main() {
    printf("hello, world\n");
    printf("haha\n");
    return 0;
}
// 解释：
// main函数是程序的入口
// 一个工程中main函数有且仅有一个
```



### 3. 数据类型

```c
- 基本数据类型
	-char 		// 字符型
	-short 		// 短整型
	-int 		// 整形
	-long 		// 长整型
	-long long 	// 更长的整形
	-float 		// 单精度浮点数
	-double 	// 双精度浮点数
- 枚举类型
- void类型
- 派生类型
// C语言有没有字符串类型？
```

```c
// 每种类型的大小是多少？
#include <stdio.h>
int main() {
    printf("%d\n", sizeof(char));			// 1
    printf("%d\n", sizeof(short));			// 2
    printf("%d\n", sizeof(int));			// 4
    printf("%d\n", sizeof(long));			// 4
    printf("%d\n", sizeof(long long));		// 8
    printf("%zu\n", sizeof(float));			// 4
    printf("%zu\n", sizeof(double));		// 8
	printf("%zu\n", sizeof(long double));	// 16
	return 0 ;
}
```
> C语言规定：`sizeof(long)  >=   sizeof(int)`



**计算机中的单位**

```
bit  -- 比特位
byte -- 字节
kb / mb / gb / tb / pb

// 1个bit位能存储1位二进制数字
1byte == 8bit
1kb == 1024byte
1mb == 1024kb
同理...
```



| 类型           | 存储大小    | 值范围                                                       |
| -------------- | ----------- | ------------------------------------------------------------ |
| char           | 1 字节      | -128 到 127 或 0 到 255                                      |
| int            | 2 或 4 字节 | `-32,768` 到 `32,767` 或 `-2,147,483,648` 到 `2,147,483,647` |
| short          | 2 字节      | -32,768 到 32,767                                            |
| long           | 4 字节      | -2,147,483,648 到 2,147,483,647                              |

| 类型        | 存储大小 | 值范围                 | 精度        |
| ----------- | -------- | ---------------------- | ----------- |
| float       | 4 字节   | 1.2E-38 到 3.4E+38     | 6 位有效位  |
| double      | 8 字节   | 2.3E-308 到 1.7E+308   | 15 位有效位 |
| long double | 16 字节  | 3.4E-4932 到 1.1E+4932 | 19 位有效位 |



### 4. 变量、常量、作用域


变量其实只不过是程序**可操作的存储区的名称**。C 语言中每个变量都有特定的类型，类型决定了变量存储的大小和布局，该范围内的值都可以存储在内存中，运算符可应用于变量上。

变量的名称可以由 **字母** 、 **数字** 和 **下划线字符** 组成。它必须以字母或下划线开头，并且大小写敏感的。

#### 4.1 定义变量的方法

```c
int age = 150;
float weight = 45.5f;
char ch = 'w';
```

#### 4.2 变量的分类

- 局部变量
- 全局变量

```c
#include <stdio.h>

int global = 2019;		// 全局变量
int main() {
	int local = 2018;	// 局部变量
	// 下面定义的global会不会有问题？
	int global = 2020;	// 局部变量
	printf("global = %d\n", global);
	return 0;
}
```

总结：

> 当局部变量和全局变量同名的时候，局部变量优先使用。

> 函数的参数，形式参数，被当作该函数内的局部变量，如果与全局变量同名它们会优先使用。

> 当局部变量被定义时，系统不会对其初始化，自行对其初始化。定义全局变量时，系统会自动对其初始化。



#### 4.3 作用域和生命周期

任何一种编程中，**作用域（scope）**是程序中定义的变量所存在的区域，超过该区域变量就不能被访问。C 语言中有三个地方可以声明变量：

1. 在函数或块内部的**局部**变量；
2. 在所有函数外部的**全局**变量；
3. 在**形式**参数的函数参数定义中。

> 局部变量的作用域是变量所在的局部范围。全局变量的作用域是整个工程。

- **全局变量与局部变量在内存中的区别**：
  - 全局变量保存在内存的**全局存储区**中，占用静态的存储单元；
  - 局部变量保存在**栈**中，只有在所在函数被调用时才动态地为变量分配存储单元。
- **生命周期：**变量的生命周期指的是变量的创建到变量的销毁之间的一个时间段。
  1. 局部变量的生命周期是：进入作用域生命周期开始，出作用域生命周期结束。
  - 全局变量的生命周期是：整个程序的生命周期。



#### 4.4 常量

C语言中常量的分类：字面常量、const修饰的常变量、#define定义的标识符常量、枚举常量。

在 C 语言中，有两种简单的定义常量的方式：

1. 使用 **#define** 预处理器： #define 可以在程序中定义一个常量，它在编译时会被替换为其对应的值。

	> ```c
	> // #define 常量名 常量值
	> #define PI 3.14159
	> ```

1. 使用 **const** 关键字：const 关键字用于声明一个只读变量，即该变量的值不能在程序运行时修改。

   > ```c
   > // const 数据类型 常量名 = 常量值;
   > const int MAX = 100;
   > ```

```c
#include <stdio.h>

// 举例
enum Sex {
	MALE,
	FEMALE,
	SECRET
};

// 括号中的MALE, FEMALE, SECRET是枚举常量
int main() {
	// 字面常量演示
	// 3.14;	// 字面常量
 	// 1000;	// 字面常量
    // const 修饰的常变量
    const float pi = 3.14f; 	// 这里的pai是const修饰的常变量
    // pi = 5.14;		// 是不能直接修改的！
    // #define的标识符常量 演示
	#define MAX 100
	printf("max = %d\n", MAX);
    // 枚举常量演示
    printf("%d\n", MALE);
    printf("%d\n", FEMALE);
    printf("%d\n", SECRET);
    // 注：枚举常量的默认是从 0 开始，依次向下递增 1 的
	return 0;
}
```
> 注：`pi`被称为const修饰的常变量，const修饰的常变量在C语言中只是在语法层面限制了变量`pi`不能直接被改变，但是`pi` 本质上还是一个变量的，所以叫常变量。
>



**define 与 const 区别**

通常情况下，建议使用 const 关键字来定义常量，因为它具有类型检查和作用域的优势，而 #define 仅进行简单的文本替换，可能会导致一些意外的问题。

区别：

- 替换机制：`#define` 是进行简单的文本替换，而 `const` 是声明一个具有类型的常量。`#define` 定义的常量在编译时会被直接替换为其对应的值，而 `const` 定义的常量在程序运行时会分配内存，并且具有类型信息。
- 类型检查：`#define` 不进行类型检查，因为它只是进行简单的文本替换。而 `const` 定义的常量具有类型信息，编译器可以对其进行类型检查。这可以帮助捕获一些潜在的类型错误。
- 作用域：`#define` 定义的常量没有作用域限制，它在定义之后的整个代码中都有效。而 `const` 定义的常量具有块级作用域，只在其定义所在的作用域内有效。




#### 4.5 枚举常量

枚举类型通常用于为程序中的一组**相关的常量**取名字，以便于程序的可读性和维护性。

```c
enum 枚举名 { 枚举元素1, 枚举元素2, …… };
```



### 5. 字符串+转义字符+注释

#### 5.1 字符串

```c
"hello bit.\n"
```

这种由双引号（Double Quote）引起来的一串字符称为字符串字面值（String Literal），或者简称字符串。

**注：**字符串的结束标志是一个`\0`的转义字符。在计算字符串长度的时候`\0`是结束标志，不算作字符串内容。

```c
#include <stdio.h>
// 下面代码，打印结果是什么？为什么？（突出'\0'的重要性）
int main()
{
    char arr1[] = "bit";
    char arr2[] = {'b', 'i', 't'};
    char arr3[] = {'b', 'i', 't'， '\0'};
    printf("%s\n", arr1);
    printf("%s\n", arr2);
    printf("%s\n", arr3);
    return 0;
}
```



#### 5.2 转义字符

加入我们要在屏幕上打印一个目录：`c:\code\test.c`

我们该如何写代码？

实际上程序运行的结果是这样的：

```c
#include <stdio.h>
int main() {
	printf("c:\code\test.c\n");
	return 0;
}
```
这里就不得不提一下转义字符了。转义字符顾名思义就是转变意思。

下面看一些转义字符。

| 转义字符 |                        释义                        |
| :------: | :------------------------------------------------: |
|   `\?`   | 在书写连续多个问号时使用，防止他们被解析成三字母词 |
|   `\'`   |                 用于表示字符常量'                  |
|   `\“`   |           用于表示一个字符串内部的双引号           |
|   `\\`   | 用于表示一个反斜杠，防止它被解释为一个转义序列符。 |
|   `\a`   |                   警告字符，蜂鸣                   |
|`\b`| 退格符|
|`\f`| 进纸符|
|`\n`| 换行|
|`\r`| 回车|
|`\t`| 水平制表符|
|`\v`| 垂直制表符|
|`\ddd`| ddd表示1~3个八进制的数字。 如：`\130 X |
|`\xdd`| dd表示 2 个十六进制数字。 如： \x30 0|

```C
#include <stdio.h>
int main() {
    // 问题 1 ：在屏幕上打印一个单引号'，怎么做？
    // 问题 2 ：在屏幕上打印一个字符串，字符串的内容是一个双引号“，怎么做？
    printf("%c\n", '\'');
    printf("%s\n", "\"");
    return 0;
}
```
 笔试题：

```c
// 程序输出什么？
#include <stdio.h>
int main() {
    printf("%d\n", strlen("abcdef"));
    // \62被解析成一个转义字符
    printf("%d\n", strlen("c:\test\628\test.c"));
    return 0;
}
```

#### 5.3 注释

1. 代码中有不需要的代码可以直接删除，也可以注释掉
2. 代码中有些代码比较难懂，可以加一下注释文字

比如：

```c
#include <stdio.h>
int Add(int x, int y) {
	return x+y;
}
/* C语言风格注释
int Sub(int x, int y) {
	return x-y;
}
*/
int main() {
	// C++注释风格
	// int a = 10;
	// 调用Add函数，完成加法
	printf("%d\n", Add( 1 , 2 ));
	return 0;
}
```

注释有两种风格：

- C语言风格的注释 `/*xxxxxx*/`
  - 缺陷：不能嵌套注释
- C++风格的注释 `//xxxxxxxx`
  - 可以注释一行也可以注释多行





### 6. 选择语句

如果你好好学习，校招时拿一个好offer，走上人生巅峰。

如果你不学习，毕业等于失业，回家卖红薯。

这就是选择！

```c
#include <stdio.h>
int main() {
    int coding = 0;
    printf("你会去敲代码吗？（选择1 or 0）:>");
    scanf("%d", &coding);
    if(coding == 1) {
    	prinf("坚持，你会有好offer\n");
    }
    else {
    	printf("放弃，回家卖红薯\n");
    }
    return 0;
}
```




### 7. 循环语句

C语言中如何实现循环呢？

- while语句-讲解
- for语句
- do ... while语句

```c
// while循环的实例
#include <stdio.h>
int main() {
    printf("加入比特\n");
    int line = 0 ;
    while(line <= 20000) {
    	line++;
    	printf("我要继续努力敲代码\n");
    }
    if(line > 20000)
    	printf("好offer\n");
    return 0;
}
```



### 8. 函数

函数的特点就是简化代码，代码复用。

```c
#include <stdio.h>
int main() {
    int num1 = 0;
    int num2 = 0;
    int sum = 0;
    printf("输入两个操作数:>");
    scanf("%d %d", &num1, &num2);
    sum = num1 + num2;
    printf("sum = %d\n", sum);
    return 0;
}
# 上述代码，写成函数如下：
#include <stdio.h>
int Add(int x, int y) {
	int z = x + y;
	return z;
}
int main() {
    int num1 = 0;
    int num2 = 0;
    int sum = 0;
    printf("输入两个操作数:>");
    scanf("%d %d", &num1, &num2);
    sum = Add(num1, num2);
    printf("sum = %d\n", sum);
    return 0;
}
```



### 9. 数组

要存储1-10的数字，怎么存储？

C语言中给了数组的定义：一组相同类型元素的集合

##### 9.1 数组定义

```c
int arr[10] = {1 , 2 , 3 , 4 , 5 , 6 , 7 , 8 , 9 , 10};		// 定义一个整形数组，最多放 10 个元素
```

##### 9.2 数组的下标

C语言规定：数组的每个元素都有一个下标，下标是从 0 开始的。

数组可以通过下标来访问的。

比如：

```c
int arr[10] = {0};
// 如果数组 10 个元素，下标的范围是0-9
```

##### 9.3 数组的使用

```c
#include <stdio.h>
int main()
{
    int i = 0;
    int arr[10] = {1 , 2 , 3 , 4 , 5 , 6 , 7 , 8 , 9 , 10};
    for(i = 0; i < 10 ; i++)
    {
    	printf("%d ", arr[i]);
    }
    printf("\n");
    return 0 ;
}
```



### 10. 操作符

- 算术操作符

```
+ - * / %
```
- 移位操作符

```
>> <<
```
- 位操作符

```
& ^ |
```
- 赋值操作符

```
= += -= *= /= &= ^= |= >>= <<=
```
- 单目操作符

```
! 	逻辑反操作
- 	负值
+ 	正值
& 	取地址
sizeof 	操作数的类型长度（以字节为单位）
~ 	对一个数的二进制按位取反
-- 	前置、后置	--
++ 	前置、后置	++
- 	间接访问操作符(解引用操作符)
(类型) 	强制类型转换
```

- 关系操作符

```
>
>=
<
<=
!= 用于测试“不相等”
== 用于测试“相等”
```

- 逻辑操作符

```
&& 逻辑与
|| 逻辑或
```

- 条件操作符

```
exp1? exp2 : exp
```

- 逗号表达式

```
exp1, exp2, exp3, ...expN
```

- 下标引用、函数调用和结构成员

```
[] (). ->
```



### 11. 常见关键字

```C
auto break case char const continue default do double else enum
extern float for goto if int long register return short signed
sizeof static struct switch typedef union unsigned void volatile while
```
注：关键字，先介绍下面几个，后期遇到讲解。


##### 11.1 关键字 typedef

> typedef 顾名思义是类型定义，这里应该理解为类型重命名。

比如：

```c
#include <stdio.h>
// 将unsigned int 重命名为uint_32, 所以uint_32也是一个类型名
typedef unsigned int uint_32;
int main()
{
    // 观察num1和num2,这两个变量的类型是一样的
    unsigned int num1 = 0;
    uint_32 num2 = 0;
    return 0;
}
```

##### 11.2 关键字static

> 在C语言中：`static` 是用来修饰变量和函数的。
>
> - 修饰局部变量，称为静态局部变量
> - 修饰全局变量，称为静态全局变量
> - 修饰函数，称为静态函数

**11.2.1 修饰局部变量**

``` c
//代码 1
#include <stdio.h>
void test() {
    int i = 0;
    i++;
    printf("%d ", i);
}
int main() {
    int i = 0;
    for(i = 0; i < 10; i++) {
    	test();
    }
    return 0;
}
//代码 2
#include <stdio.h>
void test() {
    // static修饰局部变量
    static int i = 0;
    i++;
    printf("%d ", i);
}
int main() {
    int i = 0;
    for(i = 0; i < 10; i++) {
    	test();
    }
    return 0;
}
```

对比代码 1 和代码 2 的效果理解static修饰局部变量的意义。

结论：

- `static` 修饰局部变量改变了变量的生命周期
- 让静态局部变量出了作用域依然存在，到程序结束，生命周期才结束。

**11.2.2 修饰全局变量**

```c
// 代码 1
// add.c
int g_val = 2018 ;
// test.c
int main() {
	printf("%d\n", g_val);
	return 0;
}

// 代码 2
// add.c
static int g_val = 2018;
// test.c
int main() {
	printf("%d\n", g_val);
	return 0;
}
```

代码 1 正常，代码 2 在编译的时候会出现连接性错误。

结论：

> 一个全局变量被static修饰，使得这个全局变量只能在本源文件内使用，不能在其他源文件内使用。

**11.2.3 修饰函数**

```c
// 代码 1
// add.c
int Add(int x, int y) {
	return c + y;
}
// test.c
int main() {
	printf("%d\n", Add( 2 , 3 ));
	return 0;
}
```
```c
// 代码 2
// add.c
static int Add(int x, int y) {
	return c + y;
}
// test.c
int main() {
	printf("%d\n", Add( 2 , 3 ));
	return 0;
}
```

代码 1 正常，代码 2 在编译的时候会出现连接性错误.

结论：

> 一个函数被static修饰，使得这个函数只能在本源文件内使用，不能在其他源文件内使用。

剩余关键字后续课程中陆续会讲解。



### 12. #define 定义常量和宏

```c
// define定义标识符常量
#define MAX 1000
// define定义宏
#define ADD(x, y) ((x)+(y))

#include <stdio.h>
int main() {
	int sum = ADD( 2 , 3 );
	printf("sum = %d\n", sum);
    sum = 10 *ADD( 2 , 3 );
	printf("sum = %d\n", sum);
    return 0;
}
```



### 13. 指针

**13.1 内存**

内存是电脑上特别重要的存储器，计算机中程序的运行都是在内存中进行的 。

所以为了有效的使用内存，就把内存划分成一个个小的内存单元，每个内存单元的大小是 **1 个字节** 。

为了能够有效的访问到内存的每个单元，就给内存单元进行了编号，这些编号被称为该 **内存单元的地址** 。




变量是创建内存中的（在内存中分配空间的），每个内存单元都有地址，所以变量也是有地址的。

取出变量地址如下：

```c
#include <stdio.h>
int main() {
    int num = 10;
    &num;	// 取出num的地址
    // 注：这里num的 4 个字节，每个字节都有地址，取出的是第一个字节的地址（较小的地址）
    printf("%p\n", &num);	// 打印地址，%p是以地址的形式打印
    return 0;
}
```


那地址如何存储，需要定义指针变量。

```c
int num = 10;
int *p;		// p为一个整形指针变量
p = &num;
```



指针的使用实例：

```c
#include <stdio.h>
int main() {
	int num = 10;
	int *p = &num;
	*p = 20;
	return 0;
} 
```
以整形指针举例，可以推广到其他类型，如：

```c
#include <stdio.h>
int main() {
    char ch = 'w';
    char* pc = &ch;
    *pc = 'q';
    printf("%c\n", ch);
    return 0;
}
```



##### 13.2 指针变量的大小

```c
#include <stdio.h>
// 指针变量的大小取决于地址的大小
// 32位平台下地址是 32 个bit位（即 4 个字节）
// 64位平台下地址是 64 个bit位（即 8 个字节）
int main() {
    printf("%d\n", sizeof(char *));
    printf("%d\n", sizeof(short *));
    printf("%d\n", sizeof(int *));
    printf("%d\n", sizeof(double *));
    return 0;
}
```
**结论** ：指针大小在 32 位平台是 4 个字节， 64 位平台是 8 个字节。



### 14. 结构体

结构体是C语言中特别重要的知识点，结构体使得C语言有能力描述复杂类型。

比如描述学生，学生包含：`名字+年龄+性别+学号` 这几项信息。

这里只能使用结构体来描述了。

例如：

```c
struct Stu {
    char name[20];	// 名字
    int age;  		// 年龄
    char sex[5];  	// 性别
    char id[15]；   // 学号
};
```

结构体的初始化：

```c
// 打印结构体信息
struct Stu s = {"张三"， 20 ， "男"， "20180101"};

// .为结构成员访问操作符
printf("name = %s age = %d sex = %s id = %s\n", s.name, s.age, s.sex, s.id);

// ->操作符
struct Stu *ps = &s;

printf("name = %s age = %d sex = %s id = %s\n", ps->name, ps->age, ps->sex, ps->id);
```

---

本章完。

