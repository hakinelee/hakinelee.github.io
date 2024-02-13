## 数组
所谓数组，就是一个集合，里面存放了**相同类型**的数据元素。
**特点：**

1. 数组中的每个数据元素都是**相同的数据类型**；
2. 数组是由**连续的内存位置**组成的；
3. 数组中下标是从 0 开始索引。
### 一维数组
#### 一维数组定义方式

1. `数据类型 数组名[数组长度];`
2. `数据类型 数组名[数组长度] = {值1, 值2, ...};`
3. `数据类型 数组名[] = {值1, 值2, ...};`

示例：
```cpp
int main() {
    // 定义方式1：数据类型 数组名[元素个数];
    int score[10];

    // 利用下标赋值
    score[0] = 100;
    score[1] = 99;
    // 利用下标输出
    cout << score[0] << endl;	// 100
    cout << score[1] << endl;	// 99

    // 定义方式2：数据类型 数组名[元素个数] =  {值1，值2 ，值3 ...};
    // 如果{}内不足10个数据，剩余数据用0补全
    int score2[10] = {100, 90, 80, 70, 60, 50, 40, 30, 20, 10};

    // 逐个输出
    // cout << score2[0] << endl;
    // 一个一个输出太麻烦，因此可以利用循环进行输出
    for(int i = 0; i < 10; i++) {
        cout << score2[i] << endl;
    }

    // 定义方式3：数据类型 数组名[] =  {值1, 值2, 值3, ...};
    int score3[] = {100, 90, 80, 70, 60, 50, 40, 30, 20, 10};
    for(int i = 0; i < 10; i++) {
        cout << score3[i] << endl;
    }
    system("pause");
    return 0;
}
```
> 总结：数组名的命名规范与变量名命名规范一致，不要和变量重名。

#### 一维数组数组名的**用途**

1. 可以统计整个数组在内存中的长度 `sizeof(arr)`
2. 可以获取数组在内存中的首地址 `int arr`

示例：
```cpp
int main() {
    // 1、可以获取整个数组占用内存空间大小
    int arr[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    cout << "整个数组所占内存空间为：" << sizeof(arr) << endl;
    cout << "每个元素所占内存空间为：" << sizeof(arr[0]) << endl;
    cout << "数组的元素个数为：" << sizeof(arr) / sizeof(arr[0]) << endl;

    // 2、可以通过数组名获取到数组首地址
    cout << "数组首地址为：" << (int)arr << endl;
    cout << "数组中第一个元素地址为：" << (int)&arr[0] << endl;
    cout << "数组中第二个元素地址为：" << (int)&arr[1] << endl;

    // arr = 100; 错误，数组名是常量，因此不可以赋值
    system("pause");
    return 0;
}
```
#### 冒泡排序
**作用：** 最常用的排序算法，对数组内元素进行排序。

1. 比较相邻的元素。如果第一个比第二个大，就交换他们两个；
2. 对每一对相邻元素做同样的工作，执行完毕后，找到第一个最大值；
3. 重复以上的步骤，每次比较次数-1，直到不需要比较。

示例： 将数组`{4, 2, 8, 0, 5, 7, 1, 3, 9}`进行升序排序
```cpp
int main() {
    int arr[9] = {4, 2, 8, 0, 5, 7, 1, 3, 9};
    for(int i = 0; i < 9 - 1; i++) {
        for(int j = 0; j < 9 - 1 - i; j++) {
            if(arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    for(int i = 0; i < 9; i++) {
        cout << arr[i] << endl;
    }  
    system("pause");
    return 0;
}
```
### 二维数组
二维数组就是在一维数组上，多加一个维度。
#### 二维数组定义方式

1. `数据类型 数组名[行数][列数];`
2. `数据类型 数组名[行数][列数] = {{数据1, 数据2}, {数据3, 数据4}};`
3. `数据类型 数组名[行数][列数] = {数据1，数据2, 数据3, 数据4};`
4. `数据类型 数组名[][列数] = {数据1, 数据2, 数据3, 数据4};`
> 建议：以上4种定义方式，利用第二种更加直观，提高代码的可读性。

示例：
```cpp
int main() {
    // 方式1：数组类型 数组名[行数][列数]
    int arr[2][3];
    arr[0][0] = 1;
    arr[0][1] = 2;
    arr[0][2] = 3;
    arr[1][0] = 4;
    arr[1][1] = 5;
    arr[1][2] = 6;

    for(int i = 0; i < 2; i++) {
        for(int j = 0; j < 3; j++) {
            cout << arr[i][j] << " ";
        }
        cout << endl;
    }

    // 方式2：数据类型 数组名[行数][列数] = {{数据1, 数据2}, {数据3, 数据4}};
    int arr2[2][3] =
    {
        {1,2,3},
        {4,5,6}
    };

    // 方式3：数据类型 数组名[行数][列数] = {数据1, 数据2, 数据3, 数据4};
    int arr3[2][3] = {1, 2, 3, 4, 5, 6}; 

    // 方式4：数据类型 数组名[][列数] = {数据1, 数据2, 数据3, 数据4};
    int arr4[][3] = {1, 2, 3, 4, 5, 6};
    system("pause");
    return 0;
}
```
> 总结：在定义二维数组时，如果初始化了数据，可以省略行数。

#### 二维数组数组名的**用途**

- 查看二维数组所占内存空间`sizeof(arr)`
- 获取二维数组首地址`arr`

示例：
```cpp
int main() {
    // 二维数组数组名
    int arr[2][3] =
    {
    	{1, 2, 3},
    	{4, 5, 6}
	};

    cout << "二维数组大小：" << sizeof(arr) << endl;
    cout << "二维数组一行大小：" << sizeof(arr[0]) << endl;
    cout << "二维数组元素大小：" << sizeof(arr[0][0]) << endl;
    cout << "二维数组行数：" << sizeof(arr) / sizeof(arr[0]) << endl;
    cout << "二维数组列数：" << sizeof(arr[0]) / sizeof(arr[0][0]) << endl;

    // 地址
    cout << "二维数组首地址：" << arr << endl;
    cout << "二维数组第一行地址：" << arr[0] << endl;
    cout << "二维数组第二行地址：" << arr[1] << endl;
    cout << "二维数组第一个元素地址：" << &arr[0][0] << endl;
    cout << "二维数组第二个元素地址：" << &arr[0][1] << endl;
    system("pause");
    return 0;
}
```
## 函数
### 概述
**作用：**将一段经常使用的代码封装起来，减少重复代码。
一个较大的程序，一般分为若干个程序块，每个模块实现特定的功能。
### 函数的定义
函数的定义一般主要有5个步骤：

- 1、返回值类型
- 2、函数名
- 3、参数表列
- 4、函数体语句
- 5、return 表达式

**语法：**
```cpp
返回值类型 函数名(参数列表) {
    函数体语句
    return 表达式
}
```

- 返回值类型 ：一个函数可以返回一个值；
- 函数名：给函数起个名称；
- 参数列表：使用该函数时，传入的数据；
- 函数体语句：花括号内的代码，函数内需要执行的语句；
- return 表达式： 和返回值类型挂钩，函数执行完后，返回相应的数据。

示例：定义一个加法函数，实现两个数相加
```cpp
//函数定义
int add(int num1, int num2) {
    int sum = num1 + num2;
    return sum;
}
```
### 函数的调用
**功能：**使用定义好的函数
**语法：**`函数名（参数）`
示例：
```cpp
//函数定义
int add(int num1, int num2) { // 定义中的num1, num2称为形式参数，简称形参
    int sum = num1 + num2;
    return sum;
}

int main() {
    int a = 10, b = 10;
    // 调用add函数
    int sum = add(a, b);     // 调用时的a，b称为实际参数，简称实参
    cout << "sum = " << sum << endl;

    a = 100;
    b = 100;
    sum = add(a, b);
    cout << "sum = " << sum << endl;
    system("pause");
    return 0;
}
```
> 总结：函数定义里小括号内称为形参，函数调用时传入的参数称为实参。

### 值传递

- 所谓值传递，就是函数调用时实参将数值传入给形参。
- 值传递时，如果形参发生，并不会影响实参。

示例：
```cpp
void swap(int num1, int num2) {
    cout << "交换前：" << endl;
    cout << "num1 = " << num1 << endl;	// 10
    cout << "num2 = " << num2 << endl;	// 20

    int temp = num1;
    num1 = num2;
    num2 = temp;

    cout << "交换后：" << endl;
    cout << "num1 = " << num1 << endl;	// 20
    cout << "num2 = " << num2 << endl;	// 10
    // return ; 当函数声明时候，不需要返回值，可以不写return
}
int main() {
    int a = 10, b = 20;
    swap(a, b);
    cout << "main中的 a = " << a << endl;	// 10
    cout << "main中的 b = " << b << endl;	// 20
    system("pause");
    return 0;
}
```
> 总结： 值传递时，形参是修饰不了实参的。

### 函数的常见样式
常见的函数样式有 4 种：

1. 无参无返；
2. 有参无返；
3. 无参有返；
4. 有参有返。

示例：
```cpp
// 1、无参无返
void test01() {
    // void a = 10; 	// 无类型不可以创建变量,原因无法分配内存
    cout << "this is test01" << endl;
    // test01(); 函数调用
}

// 2、有参无返
void test02(int a) {
    cout << "this is test02" << endl;
    cout << "a = " << a << endl;
}

// 3、无参有返
int test03() {
    cout << "this is test03 " << endl;
    return 10;
}

// 4、有参有返
int test04(int a, int b) {
    cout << "this is test04 " << endl;
    int sum = a + b;
    return sum;
}
```
### 函数的声明
**作用：** 告诉编译器函数名称及如何调用函数。函数的实际主体可以单独定义。

- 函数的**声明可以多次**，但是函数的**定义只能有一次**

示例：
```cpp
//声明可以多次，定义只能一次
//声明
int max(int a, int b);
int max(int a, int b);
//定义
int max(int a, int b) {
    return a > b ? a : b;
}

int main() {
    int a = 100;
    int b = 200;
    cout << max(a, b) << endl;
    system("pause");
    return 0;
}
```
### 函数的分文件编写
**作用：**让代码结构更加清晰。
函数分文件编写一般有4个步骤：

1. 创建后缀名为`.h`的头文件；
2. 创建后缀名为`.cpp`的源文件；
3. 在头文件中写函数的声明；
4. 在源文件中写函数的定义。

示例：
```cpp
//swap.h文件
#include<iostream>
using namespace std;

//实现两个数字交换的函数声明
void swap(int a, int b);
```
```cpp
//swap.cpp文件
#include "swap.h"

void swap(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
    cout << "a = " << a << endl;
    cout << "b = " << b << endl;
}
```
```cpp
//main函数文件
#include "swap.h"
int main() {
    int a = 100, b = 200;
    swap(a, b);
    system("pause");
    return 0;
}
```
## 结构体
### 基本概念
结构体属于用户自定义的数据类型，允许用户存储不同的数据类型。
### 定义和使用
**语法：**`struct 结构体名 {结构体成员列表};`
通过结构体创建变量的方式有三种：

- `struct 结构体名 变量名`
- `struct 结构体名 变量名 = {成员1值, 成员2值, ...}`
- `定义结构体时顺便创建变量`

**示例：**
```cpp
//结构体定义
struct student {
	//成员列表
	string name;  //姓名
	int age;      //年龄
	int score;    //分数
}stu3; //结构体变量创建方式3 

int main() {
    //结构体变量创建方式1
    struct student stu1; //struct 关键字可以省略

    stu1.name = "张三";
    stu1.age = 18;
    stu1.score = 100;	
    cout<<"姓名："<<stu1.name<<" 年龄："<<stu1.age<<" 分数："<<stu1.score<<endl;

    //结构体变量创建方式2
    struct student stu2 = { "李四",19,60 };
    cout<<"姓名："<<stu2.name<<" 年龄："<<stu2.age<<" 分数："<<stu2.score<<endl;

    stu3.name = "王五";
    stu3.age = 18;
    stu3.score = 80;
    cout<<"姓名："<<stu3.name<<" 年龄："<<stu3.age<<" 分数："<<stu3.score<<endl;
    system("pause");
    return 0;
}
```
> 总结1：定义结构体时的关键字是struct，不可省略

> 总结2：创建结构体变量时，关键字struct可以省略

> 总结3：结构体变量利用操作符 ''.''  访问成员

### 结构体数组
**作用：**将自定义的结构体放入到数组中方便维护
**语法：**`struct 结构体名 数组名[元素个数] = { {} , {} , ... {} }`
**示例：**
```c
//结构体定义
struct student {
	//成员列表
	string name;  //姓名
	int age;      //年龄
	int score;    //分数
}
int main() {	
	//结构体数组
	struct student arr[3] = {
		{"张三",18,80 },
		{"李四",19,60 },
		{"王五",20,70 }
	};
	for (int i = 0; i < 3; i++) {
		cout<<"姓名："<<arr[i].name<<" 年龄："<<arr[i].age<<" 分数："<<arr[i].score<<endl;
	}
	system("pause");
	return 0;
}
```
### 结构体指针
**作用：**通过指针访问结构体中的成员

- 利用操作符 `->`可以通过结构体指针访问结构体属性

**示例：**
```c
//结构体定义
struct student {
	//成员列表
	string name;  //姓名
	int age;      //年龄
	int score;    //分数
};

int main() {
	struct student stu = { "张三",18,100, };
	struct student * p = &stu;
	p->score = 80; //指针通过 -> 操作符可以访问成员
	cout<<"姓名："<< p->name <<" 年龄："<< p->age <<" 分数："<< p->score <<endl;
	system("pause");
	return 0;
}
```
> 总结：结构体指针可以通过 -> 操作符 来访问结构体中的成员

### 结构体嵌套结构体
**作用：** 结构体中的成员可以是另一个结构体
**例如：**每个老师辅导一个学员，一个老师的结构体中，记录一个学生的结构体
**示例：**
```c
//学生结构体定义
struct student {
	//成员列表
	string name;  //姓名
	int age;      //年龄
	int score;    //分数
};

//教师结构体定义
struct teacher {
    //成员列表
	int id; //职工编号
	string name;  //教师姓名
	int age;   //教师年龄
	struct student stu; //子结构体 学生
};

int main() {
	struct teacher t1;
	t1.id = 10000;
	t1.name = "老王";
	t1.age = 40;
	t1.stu.name = "张三";
	t1.stu.age = 18;
	t1.stu.score = 100;

	cout<<"教师职工编号："<<t1.id<<" 姓名："<<t1.name<<"年龄："<<t1.age<<endl;
	cout<<"学员姓名："<<t1.stu.name<<" 年龄："<<t1.stu.age<<"分数："<<t1.stu.score<<endl;
	system("pause");
	return 0;
}
```
**总结：**在结构体中可以定义另一个结构体作为成员，用来解决实际问题
### 结构体做函数参数
**作用：**将结构体作为参数向函数中传递
传递方式有两种：

- 值传递
- 地址传递

**示例：**
```c
//学生结构体定义
struct student {
	//成员列表
	string name;  //姓名
	int age;      //年龄
	int score;    //分数
};

//值传递
void printStudent(student stu) {
	stu.age = 28;
	cout << "子函数中 姓名："<< stu.name <<"年龄："<<stu.age<<"分数："<<stu.score<<endl;
}

//地址传递
void printStudent2(student *stu) {
	stu->age = 28;
	cout<<"子函数中姓名："<< stu->name <<"年龄:"<< stu->age <<"分数:"<< stu->score <<endl;
}

int main() {
	student stu = { "张三",18,100};
	//值传递
	printStudent(stu);
	cout<<"主函数中姓名："<<stu.name<<"年龄："<<stu.age<<"分数："<<stu.score<<endl;
	cout << endl;
	
    //地址传递
	printStudent2(&stu);
	cout<<"主函数中姓名："<<stu.name<<"年龄："<< stu.age <<"分数："<<stu.score<<endl;
	system("pause");
	return 0;
}
```
> 总结：如果不想修改主函数中的数据，用值传递，反之用地址传递

### 结构体中 const 使用场景
**作用：**用 const 来防止误操作
**示例：**
```c
//学生结构体定义
struct student {
    //成员列表
	string name;  //姓名
	int age;      //年龄
	int score;    //分数
};

//const使用场景
void printStudent(const student *stu) { //加const防止函数体中的误操作
	//stu->age = 100; //操作失败，因为加了const修饰
	cout<<"姓名："<< stu->name <<"年龄："<< stu->age <<"分数："<< stu->score <<endl;
}

int main() {
	student stu = { "张三",18,100 };
	printStudent(&stu);
	system("pause");
	return 0;
}
```
### 结构体案例
#### 案例1
**案例描述：**
学校正在做毕设项目，每名老师带领5个学生，总共有3名老师，需求如下：

1. 设计学生和老师的结构体，其中在老师的结构体中，有老师姓名和一个存放5名学生的数组作为成员；
2. 学生的成员有姓名、考试分数，创建数组存放3名老师，通过函数给每个老师及所带的学生赋值；
3. 最终打印出老师数据以及老师所带的学生数据。

**示例：**
```c
struct Student {
	string name;
	int score;
};
struct Teacher {
	string name;
	Student sArray[5];
};

void allocateSpace(Teacher tArray[] , int len) {
	string tName = "教师";
	string sName = "学生";
	string nameSeed = "ABCDE";
	for (int i = 0; i < len; i++) {
		tArray[i].name = tName + nameSeed[i];
		for (int j = 0; j < 5; j++)	{
			tArray[i].sArray[j].name = sName + nameSeed[j];
			tArray[i].sArray[j].score = rand() % 61 + 40;
		}
	}
}

void printTeachers(Teacher tArray[], int len) {
	for (int i = 0; i < len; i++) {
		cout << tArray[i].name << endl;
		for (int j = 0; j < 5; j++)	{
			cout<<"\t姓名："<<tArray[i].sArray[j].name<<"分数："<<tArray[i].sArray[j].score<<endl;
		}
	}
}

int main() {
	srand((unsigned int)time(NULL)); //随机数种子 头文件 #include <ctime>
	Teacher tArray[3]; //老师数组
	int len = sizeof(tArray) / sizeof(Teacher);
	allocateSpace(tArray, len); //创建数据
	printTeachers(tArray, len); //打印数据
	system("pause");
	return 0;
}
```
#### 案例2
**案例描述：**
设计一个英雄的结构体，包括成员姓名，年龄，性别;创建结构体数组，数组中存放5名英雄。
通过冒泡排序的算法，将数组中的英雄按照年龄进行升序排序，最终打印排序后的结果。
五名英雄信息如下：
```c
{"刘备",23,"男"},
{"关羽",22,"男"},
{"张飞",20,"男"},
{"赵云",21,"男"},
{"貂蝉",19,"女"},
```
**示例：**
```c
//英雄结构体
struct hero {
	string name;
	int age;
	string sex;
};
//冒泡排序
void bubbleSort(hero arr[] , int len) {
	for (int i = 0; i < len - 1; i++) {
		for (int j = 0; j < len - 1 - i; j++) {
			if (arr[j].age > arr[j + 1].age) {
				hero temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
			}
		}
	}
}
//打印数组
void printHeros(hero arr[], int len) {
	for (int i = 0; i < len; i++) {
		cout<<"姓名："<<arr[i].name<<"性别："<<arr[i].sex<<"年龄："<<arr[i].age<<endl;
	}
}

int main() {
	struct hero arr[5] = {
		{"刘备",23,"男"},
		{"关羽",22,"男"},
		{"张飞",20,"男"},
		{"赵云",21,"男"},
		{"貂蝉",19,"女"},
	};
	int len = sizeof(arr) / sizeof(hero); //获取数组元素个数
	bubbleSort(arr, len); //排序
	printHeros(arr, len); //打印
	system("pause");
	return 0;
}
```

