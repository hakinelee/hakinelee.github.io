## 入门

### 注释

**作用：**在代码中加一些说明和解释，方便自己和其他程序员阅读代码。
**两种格式：**

1. **单行注释：**`// 描述信息`

· 通常在一行代码的上方，或者一条语句的末尾，**对该行代码说明**。

2. **多行注释：**`/* 描述信息 */`

· 通常在一行代码的上方，**对该段代码做整体说明**。
> 提示：编译器在编译代码时，会忽略注释的内容。

### 变量

**作用：**给一段指定的**内存空间**起名，方便操作这段内存。
**语法：**`数据类型 变量名 = 初始值；`
示例：
> 每一段内存都会有一个地址编号，这段地址编号通常使用一个十六进制的数字来代表它，如0x0000。

```cpp
# include <iostream>
using namespace std;

int main () {
    int a = 10;
    cout << "a = " << a << endl;
    system ("pause");
    return 0;
}
```

### 常量

**作用：**用于记录程序中不可更改的数据。
C++定义常量的两种方式：

1. `#define` **宏常量**：`# define 常量名 常量值`

- **通常在文件上方定义**，表示一个常量。

2. `const` **修饰的变量**：`const 数据类型 常量名 = 常量值`

- **通常在变量定义前加关键字 const，**修饰该变量为常量，不可更改。

示例：

```cpp
# include <iostream>
using namespace std;
 
//#define 宏常量
#define Day 7
int main (){
    cout<<"一周总共有："<<Day<<"天"<<endl;

    //const修饰的变量
    const int month = 12;
    cout<<"一年总共有："<<month<<"月"<<endl; 
    system("pause");
    return 0;
}
```

### 关键字

**作用：**关键字是C++中预先保留的单词（标识符）。
> 在定义变量或者常量的时候，不要用关键字

C++关键字如下：

| asm | do | if | return | typedef |
| --- | --- | --- | --- | --- |
| auto | double | inline | short | typeid |
| bool | dynamic_cast | int | signed | typename |
| break | else | long | sizeof | union |
| case | enum | mutable | static | unsigned |
| catch | explicit | namespace | static_cast | using |
| char | export | new | struct | virtual |
| class | extern | operator | switch | void |
| const | false | private | template | volatile |
| const_cast | float | protected | this | wchar_t |
| continue | for | public | throw | while |
| default | friend | register | true | |
| delete | goto | reinterpret_cast | try |  |

### 标识符命名规则

**作用：**C++规定给标识符（变量、常量）命名时，有一套自己的规则。
**·**标识符不能是关键字；
**·**标识符只能由**数字、字母、下划线**组成；
**·**首字符必须是**字母或下划线**；
**·**大小写敏感；

> 建议：给标识符命名时，争取做到见名知意的效果，方便自己和他人的阅读。

### 输入/输出

输入：`cin >> 变量;`
输出：`cout << 变量;`

示例：

```cpp
int main(){
    //整型输入
    int a = 0;
    cout << "请输入整型变量：" << endl;
    cin >> a;
    cout << a << endl;

    //浮点型输入
    double d = 0;
    cout << "请输入浮点型变量：" << endl;
    cin >> d;
    cout << d << endl;

    //字符型输入
    char ch = 0;
    cout << "请输入字符型变量：" << endl;
    cin >> ch;
    cout << ch << endl;

    //字符串型输入
    string str;
    cout << "请输入字符串型变量：" << endl;
    cin >> str;
    cout << str << endl;

    //布尔类型输入
    bool flag = true;
    cout << "请输入布尔型变量：" << endl;
    cin >> flag;
    cout << flag << endl;
    system("pause");
    return 0;
}
```

## 数据类型
>
> C++规定在创建一个变量或者常量时，必须要指出相应的数据类型，否则无法给变量分配内存。

| 类型 | 关键字 |
| --- | --- |
| 布尔型 | bool |
| 字符型 | char |
| 整型 | int |
| 浮点型 | float |
| 双浮点型 | double |
| 无类型 | void |
| 宽字符型 | wchar_t |

### 整型

**作用：**整型变量表示的是**数据类型**的数据。(整数)
C++中能够表示整型的类型有以下几种方式，**区别在于所占内存空间不同：**

| 数据类型 | 占用空间 | 取值范围 |
| --- | --- | --- |
| short(短整型) | 2字节 | $-2^{15}$~$2^{15}-1$ |
| int(整型) | 4字节 | $-2^{31}$~$2^{31}-1$ |
| long(长整型) | Windows为4字节，Linux为4字节（32位），8字节（64位） | $-2^{31} $~$2^{31}-1$ |
| long long(长长整型) | 8字节 | $-2^{63}$~$2^{63}-1$ |

> 1字节==8位二进制

### sizeof关键字

**作用：**利用sizeof关键字可以统计数据类型所占内存大小。
**语法：**`sizeof( 数据类型 / 变量)`
**示例：**

```cpp
int main() {
    cout << "short类型所占内存空间为：" << sizeof(short) << endl; // 2
    cout << "int  类型所占内存空间为：" << sizeof(int) << endl;  // 4
    cout << "long 类型所占内存空间为：" << sizeof(long) << endl;
    cout << "long long 类型所占内存空间为："<<sizeof(long long)<<endl;
    system("pause");
    return 0;
}
```

> 整形结论：`short`<`int`<=`long`<=`long long`

### 实型（浮点型）

**作用：**用于**表示小数**。
浮点型变量分为两种：

1. 单精度`float`：`float f1 = 3.14f;`
2. 双精度`double`：`double f2 = 3.14;`

两者的区别在于表示的有效数字范围不同。

| 数据类型 | 占用空间 | 有效数字范围 |
| --- | --- | --- |
| `float` | 4字节 | 7 位有效数字 |
| `double` | 8字节 | 15~16 位有效数字 |

示例：

```cpp
int mian() {
    float f1 = 3.14f;
    double d1 = 3.14; // PS：默认情况下，输出一个小数，只显示6位有效数字

    cout << f1 << endl;
    cout << d1 << endl;
    cout << "float sizeof = " << sizeof(f1) << endl;
    cout << "double sizeof = " << sizeof(d1) << endl;
 
    // 科学计数法
    float f2 = 3e2;  // 3*10^2
    cout << "f2 = " << f2 << endl;

    float f3 = 3e-2; // 3*10^-2=3*0.1^2
    cout << "f3 = " << f3 << endl;
    system("pause");
    return 0;
}
```

### 字符型

**作用：**字符型变量用于显示单个字符。
**语法：**`char ch = 'a';`
> 字符型变量用`单引号`，只能有`一个字符`

- C 和 C++ 中字符型变量只占用`一个字节`
- 字符型变量并不是把字符本身放到内存中存储，而是`将对应的ASCII编码放入到存储单元`

示例：

```cpp
int main() {
    char ch = 'a';
    cout << ch << endl;
    cout << sizeof(char) << endl;

    cout << (int)ch << endl;  // 查看字符a对应的ASCII码
    ch = 97;  // 可以直接用ASCII给字符型变量赋值
    cout << ch << endl;
    ch = 98;
    cout << ch << endl;
    system("pause");
    return 0;
}
```

ASCII 码表格：

| **ASCII**值 | **控制字符** | **ASCII**值 | **字符** | **ASCII**值 | **字符** | **ASCII**值 | **字符** |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | NUT | 32 | (space) | 64 | @ | 96 | 、 |
| 1 | SOH | 33 | ! | 65 | A | 97 | a |
| 2 | STX | 34 | " | 66 | B | 98 | b |
| 3 | ETX | 35 | # | 67 | C | 99 | c |
| 4 | EOT | 36 | $ | 68 | D | 100 | d |
| 5 | ENQ | 37 | % | 69 | E | 101 | e |
| 6 | ACK | 38 | & | 70 | F | 102 | f |
| 7 | BEL | 39 | , | 71 | G | 103 | g |
| 8 | BS | 40 | ( | 72 | H | 104 | h |
| 9 | HT | 41 | ) | 73 | I | 105 | i |
| 10 | LF | 42 | * | 74 | J | 106 | j |
| 11 | VT | 43 | + | 75 | K | 107 | k |
| 12 | FF | 44 | , | 76 | L | 108 | l |
| 13 | CR | 45 | - | 77 | M | 109 | m |
| 14 | SO | 46 | . | 78 | N | 110 | n |
| 15 | SI | 47 | / | 79 | O | 111 | o |
| 16 | DLE | 48 | 0 | 80 | P | 112 | p |
| 17 | DCI | 49 | 1 | 81 | Q | 113 | q |
| 18 | DC2 | 50 | 2 | 82 | R | 114 | r |
| 19 | DC3 | 51 | 3 | 83 | S | 115 | s |
| 20 | DC4 | 52 | 4 | 84 | T | 116 | t |
| 21 | NAK | 53 | 5 | 85 | U | 117 | u |
| 22 | SYN | 54 | 6 | 86 | V | 118 | v |
| 23 | TB | 55 | 7 | 87 | W | 119 | w |
| 24 | CAN | 56 | 8 | 88 | X | 120 | x |
| 25 | EM | 57 | 9 | 89 | Y | 121 | y |
| 26 | SUB | 58 | : | 90 | Z | 122 | z |
| 27 | ESC | 59 | ; | 91 | [ | 123 | { |
| 28 | FS | 60 | < | 92 | / | 124 | &#124; |
| 29 | GS | 61 | = | 93 | ] | 125 | } |
| 30 | RS | 62 | > | 94 | ^ | 126 | ` |
| 31 | US | 63 | ? | 95 | _ | 127 | DEL |

ASCII 码大致由以下两部分组成：

- ASCII 非打印控制字符： ASCII 表上的数字 **0-31** 分配给了控制字符，用于控制像打印机等一些外围设备。
- ASCII 打印字符：数字 **32-126** 分配给了能在键盘上找到的字符，当查看或打印文档时就会出现。

### 转义字符

**作用：**用于表示一些不能显示出来的 ASCII 字符
现阶段我们常用的转义字符有：`\n \\ \t`

| **转义字符** | **含义** | **ASCII**码值（十进制） |
| --- | --- | --- |
| \\a | 警报 | 007 |
| \\b | 退格(BS) ，将当前位置移到前一列 | 008 |
| \\f | 换页(FF)，将当前位置移到下页开头 | 012 |
| **\\n** | **换行(LF) ，将当前位置移到下一行开头** | **010** |
| \\r | 回车(CR) ，将当前位置移到本行开头 | 013 |
| **\\t** | **水平制表(HT) （跳到下一个TAB位置）** | **009** |
| \\v | 垂直制表(VT) | 011 |
| **\\\\** | **代表一个反斜线字符""** | **092** |
| ' | 代表一个单引号（撇号）字符 | 039 |
| " | 代表一个双引号字符 | 034 |
| ? | 代表一个问号 | 063 |
| \\0 | 数字0 | 000 |
| \\ddd | 8进制转义字符，d范围0~7 | 3位8进制 |
| \\xhh | 16进制转义字符，h范围0~9, a~f, A~F | 3位16进制 |

示例：

```cpp
int main() {
    cout << "\\" << endl;
    cout << "\tHello" << endl;
    cout << "\n" << endl;
    system("pause");
    return 0;
}
```

### 字符串型

**作用**：用于表示一串字符。
**两种风格**

1. **C 风格字符串**： `char 变量名[] = "字符串值"`

示例：

```cpp
int main() {
    char str1[] = "hello world";
    cout << str1 << endl;
    system("pause");
    return 0;
}
```

> 注意：C风格的字符串要用双引号括起来

2. **C++ 风格字符串**：  `string 变量名 = "字符串值"`

示例：

```cpp
int main() {
    string str = "hello world";
    cout << str << endl;
    system("pause");
    return 0;
}
```

> 注意：C++ 风格字符串，需要加入头文件`#include<string>`

### 布尔类型 bool

**作用：**布尔数据类型代表真或假的值
bool类型只有两个值：

- true  --- 真（本质是1）
- false --- 假（本质是0）

**bool类型占1个字节大小**
示例：

```cpp
int main() {
    bool flag = true;
    cout << flag << endl; // 1
    flag = false;
    cout << flag << endl; // 0
    cout << "size of bool = " << sizeof(bool) << endl;  // 1
    system("pause");
    return 0;
}
```

## 运算符

### 算术运算符

**作用**：用于处理四则运算。

| **运算符** | **术语** | **示例** | **结果** |
| --- | --- | --- | --- |
| + | 正号 | +3 | 3 |
| - | 负号 | -3 | -3 |
| + | 加 | 10 + 5 | 15 |
| - | 减 | 10 - 5 | 5 |
| * | 乘 | 10 * 5 | 50 |
| / | 除 | 10 / 5 | 2 |
| % | 取模(取余) | 10 % 3 | 1 |
| ++ | 前置递增 | a=2; b=++a; | a=3; b=3; |
| ++ | 后置递增 | a=2; b=a++; | a=3; b=2; |
| -- | 前置递减 | a=2; b=--a; | a=1; b=1; |
| -- | 后置递减 | a=2; b=a--; | a=1; b=2; |

示例1：

```cpp
//加减乘除
int main() {
    int a1 = 10;
    int b1 = 3;

    cout << a1 + b1 << endl;
    cout << a1 - b1 << endl;
    cout << a1 * b1 << endl;
    cout << a1 / b1 << endl;  //两个整数相除结果依然是整数

    int a2 = 10;
    int b2 = 20;
    cout << a2 / b2 << endl; 

    int a3 = 10;
    int b3 = 0;
    //cout << a3 / b3 << endl; //报错，除数不可以为0

    //两个小数可以相除
    double d1 = 0.5;
    double d2 = 0.25;
    cout << d1 / d2 << endl;
    system("pause");
    return 0;
}
```

> 总结：在除法运算中，除数不能为 0

示例2：

```cpp
//取模
int main() {
    int a1 = 10;
    int b1 = 3;
    cout << 10 % 3 << endl;

    int a2 = 10;
    int b2 = 20;
    cout << a2 % b2 << endl;

    int a3 = 10;
    int b3 = 0;
    //cout << a3 % b3 << endl; //取模运算时，除数也不能为0

    //两个小数不可以取模
    double d1 = 3.14;
    double d2 = 1.1;
    //cout << d1 % d2 << endl;
    system("pause");
    return 0;
}
```

> 总结：只有整型变量可以进行取模运算

示例3：

```cpp
//递增
int main() {
    //后置递增
    int a = 10;
    a++; //等价于a = a + 1
    cout << a << endl; // 11

    //前置递增
    int b = 10;
    ++b;
    cout << b << endl; // 11

    //区别
    //前置递增先对变量进行++，再计算表达式
    int a2 = 10;
    int b2 = ++a2 * 10;
    cout << b2 << endl;

    //后置递增先计算表达式，后对变量进行++
    int a3 = 10;
    int b3 = a3++ * 10;
    cout << b3 << endl;
    system("pause");
    return 0;
}
```

> 总结：前置递增先对变量进行++，再计算表达式，后置递增相反

### 赋值运算符

**作用：**用于将表达式的值赋给变量。

| **运算符** | **术语** | **示例** | **结果** |
| --- | --- | --- | --- |
| = | 赋值 | a=2; b=3; | a=2; b=3; |
| += | 加等于 | a=0; a+=2; | a=2; |
| -= | 减等于 | a=5; a-=3; | a=2; |
| *= | 乘等于 | a=2; a*=2; | a=4; |
| /= | 除等于 | a=4; a/=2; | a=2; |
| %= | 模等于 | a=3; a%2; | a=1; |

**示例：**

```cpp
int main() {
    // 赋值运算符
    // =
    int a = 10;
    a = 100;
    cout << "a = " << a << endl;

    // +=
    a = 10;
    a += 2; // a = a + 2;
    cout << "a = " << a << endl;

    // -=
    a = 10;
    a -= 2; // a = a - 2
    cout << "a = " << a << endl;

    // *=
    a = 10;
    a *= 2; // a = a * 2
    cout << "a = " << a << endl;

    // /=
    a = 10;
    a /= 2;  // a = a / 2;
    cout << "a = " << a << endl;

    // %=
    a = 10;
    a %= 2;  // a = a % 2;
    cout << "a = " << a << endl;
    system("pause");
    return 0;
}
```

### 比较运算符

**作用：**用于表达式的比较，并返回一个真值或假值。

| **运算符** | **术语** | **示例** | **结果** |
| --- | --- | --- | --- |
| == | 相等于 | 4 == 3 | 0 |
| != | 不等于 | 4 != 3 | 1 |
| < | 小于 | 4 < 3 | 0 |
| > | 大于 | 4 > 3 | 1 |
| <= | 小于等于 | 4 <= 3 | 0 |
| >= | 大于等于 | 4 >= 1 | 1 |

示例：

```cpp
int main() {
    int a = 10;
    int b = 20;
    cout << (a == b) << endl; // 0 
    cout << (a != b) << endl; // 1
    cout << (a > b) << endl;  // 0
    cout << (a < b) << endl;  // 1
    cout << (a >= b) << endl; // 0
    cout << (a <= b) << endl; // 1
    system("pause");
    return 0;
}
```

> 注意：C 和 C++ 语言的比较运算中，“真”用数字“1”来表示，“假”用数字“0”来表示

### 逻辑运算符

**作用：**用于根据表达式的值返回真值或假值。

| **运算符** | **术语** | **示例** | **结果** |
| --- | --- | --- | --- |
| ! | 非 | !a | 如果 a为假，则 !a 为真；如果 a 为真，则 !a 为假。 |
| && | 与 | a && b | 如果 a 和 b 都为真，则结果为真，否则为假。 |
| &#124;&#124; | 或 | a &#124;&#124; b | 如果 a 和 b 有一个为真，则结果为真，二者都为假时，结果为假。 |

示例1：逻辑非

```cpp
// 逻辑运算符  --- 非
int main() {
    int a = 10;
    cout << !a << endl; // 0
    cout << !!a << endl; // 1
    system("pause");
    return 0;
}
```

> 总结： 真变假，假变真

示例2：逻辑与

```cpp
// 逻辑运算符  --- 与
int main() {
    int a = 10;
    int b = 10;
    cout << (a && b) << endl; // 1

    a = 10;
    b = 0;
    cout << (a && b) << endl; // 0 

    a = 0;
    b = 0;
    cout << (a && b) << endl; // 0
    system("pause");
    return 0;
}
```

> 总结：逻辑与运算符总结：同真为真，其余为假

示例3：逻辑或

```cpp
// 逻辑运算符  --- 或
int main() {
    int a = 10;
    int b = 10;
    cout << (a || b) << endl;// 1

    a = 10;
    b = 0;
    cout << (a || b) << endl;// 1 

    a = 0;
    b = 0;
    cout << (a || b) << endl;// 0
    system("pause");
    return 0;
}
```

> 逻辑或运算符总结：同假为假，其余为真

## 程序流程结构

C/C++ 支持最基本的三种程序运行结构：

- 顺序结构：程序按顺序执行，不发生跳转；
- 选择结构：依据条件是否满足，有选择的执行相应功能；
- 循环结构：依据条件是否满足，循环多次执行某段代码。

### 选择结构

#### if 语句

**作用：**执行满足条件的语句。
if 语句的三种形式：

1. 单行格式 if 语句：

```cpp
if (条件) { 
    条件满足执行的语句 
}
```

> 注意：if 条件表达式后不要加分号

2. 多行格式 if 语句：

```cpp
if(条件) { 
    条件满足执行的语句 
}
else { 
    条件不满足执行的语句 
};
```

3. 多条件的 if 语句：

```cpp
if(条件1) { 
    条件1满足执行的语句 
}
else if(条件2) {
    条件2满足执行的语句
}... 
else { 
    都不满足执行的语句
}
```

> 嵌套 if 语句：在 if 语句中，可以嵌套使用 if 语句，达到更精确的条件判断

#### 三目运算符

**作用：** 通过三目运算符实现简单的判断。
**语法：**`表达式1 ? 表达式2 ：表达式3`
**解释：**

- 如果表达式1的值为真，执行表达式2，并返回表达式2的结果；
- 如果表达式1的值为假，执行表达式3，并返回表达式3的结果。

**示例：**

```cpp
int main() {
    int a = 10;
    int b = 20;
    int c = 0;
    c = a > b ? a : b;
    cout << "c = " << c << endl;

    // C++中三目运算符返回的是变量,可以继续赋值
    (a > b ? a : b) = 100;

    cout << "a = " << a << endl;
    cout << "b = " << b << endl;
    cout << "c = " << c << endl;
    system("pause");
    return 0;
}
```

> 总结：和 if 语句比较，三目运算符优点是短小整洁，缺点是如果用嵌套，结构不清晰

#### switch 语句

**作用：**执行多条件分支语句。
**语法：**

```cpp
switch (表达式) {
    case 结果1：
        执行语句; 
        break;
    case 结果2：
        执行语句; 
        break;
    ...
    default: 
        执行语句; 
        break;
}
```

**示例：**

```cpp
int main() {
    //请给电影评分 
    // 10 ~ 9   经典   
    // 8 ~ 7    非常好
    // 6 ~ 5    一般
    // 5分以下  烂片
    int score = 0;
    cout << "请给电影打分" << endl;
    cin >> score;
    switch (score) {
     case 10:
        case 9:
            cout << "经典" << endl;
            break;
        case 8:
            cout << "非常好" << endl;
            break;
        case 7:
        case 6:
            cout << "一般" << endl;
            break;
        default:
            cout << "烂片" << endl;
            break;
    }
    system("pause");
    return 0;
}
```

> 注意1：switch 语句中表达式类型只能是**整型或者字符型**
> 注意2：case 里如果没有 break，那么程序会一直向下执行
> 总结：与 if 语句比，对于多条件判断时，switch 的结构清晰，执行效率高，缺点是 switch 不可以判断区间

### 循环结构

#### while 循环语句

**作用：**满足循环条件，执行循环语句
**语法：**

```cpp
while (循环条件) { 
    循环语句 
}
```

**解释：**只要循环条件的结果为真，就执行循环语句
示例：

```cpp
int main() {
    int num = 0;
    while (num < 10) {
        cout << "num = " << num << endl;
        num++;
    }
    system("pause");
    return 0;
}
```

> 注意：在执行循环语句时候，程序必须提供跳出循环的出口，否则出现死循环

#### do...while 循环语句

**作用：** 满足循环条件，执行循环语句
**语法：**

```cpp
do {
    循环语句 
} while(循环条件);
```

**注意：**与while的区别在于`do...while 会先执行一次循环语句`，再判断循环条件
**示例：**

```cpp
int main() {
    int num = 0;
    do {
        cout << num << endl;
        num++;
    } while (num < 10);
    system("pause");
    return 0;
}
```

> 总结：与 while 循环区别在于，do...while 先执行一次循环语句，再判断循环条件

#### for 循环语句

**作用：** 满足循环条件，执行循环语句
**语法：**

```cpp
for (起始表达式; 条件表达式; 末尾循环体) {
    循环语句; 
}
```

示例：

```cpp
int main() {
    for (int i = 0; i < 10; i++) {
        cout << i << endl;
    }
    system("pause");
    return 0;
}
```

**详解：**
> 注意：for 循环中的表达式，要用分号进行分隔。
> 总结：while , do...while, for 都是开发中常用的循环语句，for 循环结构比较清晰，比较常用。

### 跳转语句

#### break 语句

**作用：**用于跳出选择结构或者循环结构。
break 使用的时机：

- 出现在 switch 条件语句中，作用是终止 case 并跳出 switch；
- 出现在循环语句中，作用是跳出当前的循环语句；
- 出现在嵌套循环中，跳出最近的内层循环语句。

示例1：

```cpp
int main() {
    //1、在switch 语句中使用break
    cout << "请选择您挑战副本的难度：" << endl;
    cout << "1、普通" << endl;
    cout << "2、中等" << endl;
    cout << "3、困难" << endl;
    int num = 0;
    cin >> num;
    switch (num) {
        case 1:
            cout << "您选择的是普通难度" << endl;
            break;
        case 2:
            cout << "您选择的是中等难度" << endl;
            break;
        case 3:
            cout << "您选择的是困难难度" << endl;
            break;
    }
    system("pause");
    return 0;
}
```

示例2：

```cpp
int main() {
    //2、在循环语句中用break
    for (int i = 0; i < 10; i++) {
        if (i == 5) {
            break; //跳出循环语句
        }
        cout << i << endl;
    }
    system("pause");
    return 0;
}
```

示例3：

```cpp
int main() {
    //在嵌套循环语句中使用break，退出内层循环
    for (int i = 0; i < 10; i++) {
        for (int j = 0; j < 10; j++) {
            if (j == 5) {
                break;
            }
            cout << "*" << " ";
        }
        cout << endl;
    }
    system("pause");
    return 0;
}
```

#### continue 语句

**作用：**在循环结构中，跳过本次循环中余下尚未执行的语句，继续执行下一次循环。
示例：

```cpp
int main() {
    for(int i = 0; i < 100; i++) {
        if (i % 2 == 0) {
            continue;
        }
        cout << i << endl;
    }
    system("pause");
    return 0;
}
```

> 注意：continue 并没有使整个循环终止，而break会跳出循环

#### goto 语句

**作用：**可以无条件跳转语句
**语法：** `goto 标记;`
**解释：**如果标记的名称存在，执行到 goto 语句时，会跳转到标记的位置
示例：

```cpp
int main() {
    cout << "1" << endl;
    goto FLAG;
    cout << "2" << endl;
    cout << "3" << endl;
    cout << "4" << endl;
    FLAG:
    cout << "5" << endl;
    system("pause");
    return 0;
}
```

> 注意：在程序中不建议使用 goto 语句，以免造成程序流程混乱
