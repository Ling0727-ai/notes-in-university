## 一、 代码结构
```C
#include ...     // 头文件

(#define ...)   // 定义常量或一个宏

(typedef struct{
     
}Name;)     // 结构体

(int \ char \ float) // 声明全局变量

(void \ int \ char) //定义函数 

int main{

}             //主函数运行
```
___
___
## 二、头文件
提前声明一下，所有头文件都以.h结尾，h代表head
- 1. `stdio.h`
	这是最常用的头文件，包含输入输出$scanf,printf,getchar,putchar,fgets(str,size,stdin),puts,$ 、文件操作$FILE *fopen(filename,mode);fprintf;fscanf;fgets;...$ 将元素重新退回`stdin`（输入流）$ungetc(c,stdin)$（在作业7题解中有使用）等基本功能
___
- 2. `stdlib.h`
	C语言中功能最丰富的头文件，虽然大部分情况下我们都用不上。
	功能：

>>1. 动态分配内存
```C
int *arr = (int*)malloc(10*sizeof(int));   //分配10个int的空间，malloc返回指针。
//或者使用calloc动态分配内存
int *arr = (int*)calloc(10,sizeof(int));   //分配10个int的空间，并初始化为0
//也可以用realloc扩容
int arr = (int*)realloc(arr,20*sizeof(int));     //将arr的容量扩到20个int的空间
free(arr)
```
> >2. 排序 `qsort()`，但是大部分题目禁用，所以不多说了 

___
- 3. `math.h`
	这是我们第二常用的头文件，一切除加减乘除与或异或非以外的运算都离不开它。
	
	三角函数：$sin(),cos(),tan(),asin(),acos(),atan()$输入为弧度，输出double类型的浮点数
	绝对值：$abs(int),fabs(float)$
	指数和对数：$exp(),log(),log10(),log2()$，exp(n) = $e^n$,$log = ln$
	取整：$ceil(),floor(),round()$ 分别为向上、向下、四舍五入
___
- 4. `string.h`
	这是与字符串操作有关的头文件，在字符串复制以及字符串比较方面离不开它。
	
	字符串复制：$strcpy(dest,src)$将`src`复制到`dest`；$strnpy(dest,src,5)$将`src`的前n个值复制到`desr`，如果$len(src) \geq n$ ，`dest`不会自动添加`"\0"`
	字符串连接：$strcat(dest,src)$将`src`追加到`dest`末尾；$strncat(dest,src,n)$将`src`的前n位追加到`dest`末尾。
	字符串比较：$strcmp(s1,s2)$
	字符串长度：$strlen(str)$
### 例题
#### 素数探求之一
>试题描述
>>素数(`Prine Number`)，又称为质数，它是不能被1和它本身以外的其它整数整除的正整数。按照这个定义，负数、0和1都不是素数，而17之所以是素数，是因为除了1和17以外，它不能被2~16 之间的任何整数整除。<br>任务:试商法是最简单的判断素数的方法，用i=2~n一1之间的整数去试商，若存在某个m能被1与m本身以外的整数i整除(即余数为0)，则m不是素数，若上述范围的所有整数都不能整除 m，则 m是素数。<br>采用试商法:使用`goto`语句、break语句或者采用设置标志变量并加强循环测试等三种方法编写素数判断函数 `IsPrime()`，从键盘任意输入一个整数 m，判断 m 是否为素数，如果 m 是素数，则按`%d is a prime number\n`格式打印该数是素数，否则按`%d is not a prime number\n`格式打印该数不是素数。<br>实验目的:熟悉函数设计、循环的控制方法以及程序测试方法，了解什么是边界条件测试，体会模块化程序设计和函数复用的好处和意义。
>___
>输入
>>一个整数
>___
>输出
>>依据题意按格式`%d is a prime number\n`或`%d is not a prime number\n`输出该数是不是素数
```C
#include <stdio.h>  
#include <math.h>  
int main(){  
    int n, m, i, sign = 0;  
    scanf("%d",&n);  
    m = (int)sqrt(n);  
    for(i=2;i<=m;i++){ //只用判断2到sqrt(n)的所有数就行，简化计算量，加快速度  
        if(n%i==0) sign = 1;  
    }  
    if (sign) printf("%d is not a prime number",n);  
    else printf("%d is a prime number",n);  
}
```

___
___
## 三、数据类型及逻辑控制
| 类型     | 声明                           | 格式说明符 | 位数  | 范围                   |
| ------ | ---------------------------- | ----- | --- | -------------------- |
| 整型     | int                          | %d    | 16  | $[-2^{15},2^{15}-1]$ |
| 无符号整型  | unsigned int                 | %u    | 16  | $[0,2^{16}-1]$       |
| 长整型    | long                         | %ld   | 32  | $[-2^{31},2^{31}-1]$ |
| 无符号长整形 | unsigned long                | %lu   | 32  | $[0,2^{32}-1]$       |
| 浮点数    | float                        | %f    | 32  |                      |
| 长浮点数   | double                       | %lf   | 64  |                      |
| 字符     | char                         | %c    | 8   |                      |
| 数组     | int <名称>\[长度]                |       |     |                      |
| 字符串    | char <名称>\[长度+1]             | %s    |     |                      |
| 字符串列表  | char <名称><br>\[字符串数量]\[长度+1] |       |     |                      |
- tips: 如果要输出%，应该打`printf("%%");`

>条件语句：if(判据) {} else
>循环语句：while(判据){}、for(i=0;i<n;i++){}
```C
//这里重点讲一下for循环语句
int i = 0;
for(;i<n;i++) //由于i在外部已经定义取值了，于是可以不写在for的括号里，但是个人不建议这么写，缺少逻辑性
for(i=0;;i++) //一般这种情况都是在函数内部有终止条件，当然，如果函数内部也没有，那这就是一个死循环
for(i=0;i<n;) //一般这种情况都是循环变量在循环内更新
for(;;) //死循环等价于while(1)
```

### 例题
#### 计算e近似值
>试题描述
>>利用$e=1+\displaystyle\sum_1^{\infty} \frac{1}{n!}$,编程计算e的近似值，直到最后一项的绝对值小于$10^{-5}$时为止,输出e的值并统计累加的项数。输出e值要求小数点后必须保留6位有效数字(四舍五入)，不足补零。
>___
>输入
>>无输入。
>___
>输出
>>输出e的值和累加的项数，两项之间用一个空格隔开。输出e值要求小数点后必须保留6位有效数字(四舍五入)，不足补零。
>___
>数据范围
>>输出 double 范围的浮点数和 int 范围的整数
```C
#include<stdio.h>
int main(){
	int n=1;
	double e=1,t;
	t = (double)1/n;
	while(t>1e-5){
		e+=t;
		n++;
		t/=n;
	}
	printf("%.6f",e);
}
```

___
___
## 四、结构体、联合体、枚举
### 1.结构体​（`struct`）

- ​定义​：组合多个不同类型的数据成员，每个成员拥有独立的内存空间。

- ​语法​：
```c
struct 结构体名 {
    数据类型 成员1;
    数据类型 成员2;
    // ...
};
//调用时
int main(){
	struct 结构体名 <name>; //注意，每次调用都要有struct，struct不可省略
}

//或者下面的形式（个人推荐下面的，下面的和别的语言的比较像）
typedef struct{
    数据类型 成员1;
    数据类型 成员2;
    // ...
}结构体名;
//调用时无需struct
int main(){
	结构体名 <name>;
}


```

- 调用样例：
```c
#include <stdio.h>
typedef struct{
	int x;
	int y;
	int z;
}Site;

int main(){
	int i;
	Site site[10],s;   //生成长度为10个组合体的链表，名称为site;生一个结构体，名称为s
	scanf("%d%d%d",&s.x,&s.y,&s.z);
	for (i=0;i<10;i++){
		scanf("%d%d%d",&site[i].x,&site[i].y,&site[i].z);
	}
	//...
}
```

- ​特点​：
    - 成员内存独立，总大小等于各成员大小之和（考虑内存对齐）。
    - 常用于表示实体对象（如学生、坐标等）。
    - 支持嵌套、数组、指针等复杂用法。
	- ​**内存对齐**​：编译器可能插入填充字节以优化访问速度。

___
### 2. 联合体（`union`）

- ​定义​：所有成员共享同一块内存，同一时间只能存储一个成员的值。

- 语法：
```C
union 联合体名 {
    数据类型 成员1;
    数据类型 成员2;
    // ...
};
//调用
int main(){
	union 联合体名 <name>;
}

//当然，和结构体一样，这个也推荐用下面的typedef形式的
typedef union {
    数据类型 成员1;
    数据类型 成员2;
    // ...
} 联合体名;
//调用时无需union
int main(){
	联合体名 <name>;
}
```

- 调用样例：
```c
#include <stdio.h>

typedef union{
    int i;
    float f;
    char str[20];
} Data;

int main(){
	Data data;
	data.i = 10;       // 写入int
	printf("%d", data.i); 
	data.f = 3.14;     // 覆盖之前的int值Z
}
```

- ​特点​：
    - 内存大小为最大成员的大小。
    - 修改一个成员会覆盖其他成员的值。
    - 常用于节省内存或类型转换（如解析二进制数据）。
___
### 3. 枚举（`enum`）​

- ​定义​：定义一组命名的整型常量，提升代码可读性。
- 语法：
```C
enum 枚举名 { 常量1, 常量2, ... };
//调用
int main(){
	enum 枚举名 <name>;
}

//同样可以用typedef
typedef enum { 
常量1,
常量2,
...
} 枚举名;
//调用时无需enum
int main(){
	枚举名 <name>;
}
```

- 调用样例：
```C
#include <stdio.h>
typedef enum Week { Mon = 1, Tue, Wed, Thu, Fri, Sat, Sun };

int main(){
	Week day = Tue; // day的值为2
}
```

- ​**特点**​：
    - 默认从0开始递增，可显式赋值。
    - 枚举变量本质是整型，但应避免直接赋非枚举值。
    - 常用于状态码、选项等场景。
___
### 关键区别​

| ​**特性**​   | ​**结构体（struct）​**​ | ​**联合体（union）​**​ | ​**枚举（enum）​**​   |
| ---------- | ------------------ | ----------------- | ----------------- |
| ​**内存占用**​ | 各成员独立，总和<br>（对齐后）  | 最大成员的大小           | 等同于int<br>（通常4字节） |
| ​**数据存储**​ | 同时存储所有成员           | 同一时间仅存一个成员        | 存储单个整型值           |
| ​**用途**​   | 组合复杂数据             | 节省内存/类型转换         | 定义可读性高的常量         |
| ​**访问成员**​ | `.` 或 `->` 运算符     | `.` 或 `->` 运算符    | 直接赋值或比较           |
### 例题
#### 结构体之第几天 B(date7)
>试题描述
>>请定义一个表示日期的结构体类型，用于存储年、月、日。<br>编写 days 函数，结构体类型变量作为函数参数，计算并返回此日期参数在本年中是第几天,注意国年问题。<br>在主函数中,从键盘读取三个整数(分别代表年、月、日),并存储在结构体变量中。调用 days函数,输出函数返回值。<br>注意:不要改变函数名称，注意大小写敏感。
>___
>输入
>>输入3个整数，分别代表年、月、日，相邻两项之间用一个空格隔开。
>___
>输出
>>输出一个整数，代表该日期是这一年的第几天。
```C
#include <stdio.h>  
typedef struct {  
    int year;  
    int month;  
    int day;  
} Date;  
  
int is_leap(int year) {  
    return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);  
}  
int get_month_days(int year, int month) {  
    int days[12] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};  
    if (month == 2 && is_leap(year)) return 29;  
    return days[month - 1];  
}  
int days(Date d) {  
	int count=d.day,i;
	for(i = 1;i<d.month;i++){
		count+=get_month_days(d.year,i);
	}
	return count;
}
int main(){
	Date d;
	scanf("%d %d %d",&d.year,&d.month,&d.day);
	printf("%d",days(d));
}
```

___
___
## 五、函数？宏？
### 1. 函数
标准结构： `void/int/float/char <函数名>(参数1 <类型>,...){函数体}`

区别在于函数名前面的声明，函数声明为哪一种，就必须返回哪一种内容（void无返回值），顺便提一下，C语言返回值不支持返回多个值，因为C语言没有元组这个概念。
函数不改变`main`函数的内容，但可以通过改变指针的方式改变内容（一般只用于数组中），但是函数可以直接调用并改变全局变量。
### 2.宏
在某些情况下，我们需要反复写同一串代码，但是这些变量我们可不一定每一个都安排一个指针（毕竟这样还不如复制粘贴快呢），这个时候我们就可以选择使用宏。

结构： `#define <名称>(变量1,...) 内容`
>单行简单宏:
>`#define MAX(a,b) ((a) > (b) ? (a) : (b))`，这里解释一下内容部分，a>b是一个判据，输出1(True)或0(False)。后面部分(a):(b)，如果a>b输出1，则返回a；如果输出为0，则返回b。
>___
>多语句宏：
```C
#define SWAP(a,b) do{\
	int temp = a;\
	a = b;\
	b = temp;\
}while(0)
```
>这个就比上面容易理解，但是你们肯定有个疑问，为什么要用do-while，直接写不行吗？
>答案是不行，宏调用情况很复杂，如果宏调用在if-else语句或循环语句中，如果没有用do-while，很有可能因为；提前结束语句导致运行错误。

| 特性     | 宏           | 函数          |
| ------ | ----------- | ----------- |
| ​执行阶段​ | 预处理阶段文本替换   | 运行时调用       |
| ​类型检查​ | 无           | 有           |
| ​调试难度​ | 困难（无符号表）    | 容易          |
| ​性能​   | 无函数调用开销     | 有栈帧开销       |
| ​适用场景​ | 简单逻辑、类型通用操作 | 复杂逻辑、需要类型安全 |

### 例题
#### 最大数与最小数互换
>​试题描述
>>编写函数 `FindMax()`，输入 10 个整数，用函数编程将其中的最大数与最小数位置互换，然后输出互换后的数组。​
>___
>输入
>>输入 10 个整数，相邻两项之间用一个空格隔开。
>___
>输出​
>>输出互换后的数组，相邻两项之间用一个空格隔开。
```C
#include <stdio.h>  
void FindMax(int arr[]){  
    int *p,*max,*min,*temp;  
    max = arr;  
    min = arr;  
    for(p = arr+1;p < arr + 10;p++){  
       max = &p > &max ? p : max;  
       min = &p < &min ? p : min;  
       printf("%d %d\n",*max,*min);  
    }  
    temp = *max;  
    *max = *min;  
    *min = temp;  
}  
int main() {  
    int arr[10],i;  
    for(i = 0;i < 10;i++){  
       scanf("%d",&arr[i]);  
    }  
    FindMax(arr);  
    for(i = 0;i < 10;i++){  
       printf("%d ",arr[i]);  
    }  
}
```

___
___
## 六、指针

### ​（一）指针的本质

#### 1. ​什么是指针？​​

- ​定义​：指针是存储内存地址的变量。
- ​核心意义​：直接操作内存地址，提升程序的灵活性和效率。
- ​内存视角​：每个变量存储在内存中的某个位置，指针保存的是该位置的地址。

#### 2. ​指针的声明与初始化​

```c
int  *p;     // 声明一个指向 int 的指针（未初始化）
int  x = 10;
int  *p = &x; // 将 p 初始化为 x 的地址
```

#### 3. ​关键操作符​

- ​取地址符 `&` ：获取变量的内存地址。
```c
printf("%p", &x); // 输出 x 的地址
```

- ​解引用符 `*`​：通过指针访问其指向的内存内容。
```c
printf("%d", *p); // 输出 p 指向的值（即 x 的值）
```

---

### ​（二）指针的运算​

#### 1. ​基本算术运算​

- ​指针加减整数​：移动指针的位置（步长由数据类型决定）。
```c
int arr[5] = {1,2,3,4,5};
int *p = arr;      // p 指向 arr[0]
p++;               // p 现在指向 arr[1]
```

- ​指针间减法​：计算两指针之间的元素个数。

```c
int *p1 = &arr[2];
int *p2 = &arr[5];
printf("%td", p2 - p1); // 输出 3（间隔3个元素）
```

#### 2. ​指针比较​

```c
if (p1 < p2) { ... } // 比较地址的大小
```

---

### ​（三）指针与数组​

#### 1. ​数组名的本质​

- 数组名是数组首元素的地址（等价于指针）。

```c
int arr[3] = {10, 20, 30};
int *p = arr; // p 指向 arr[0]
```

#### 2. ​通过指针访问数组​

```c
printf("%d", *(p + 1)); // 输出 arr[1] 的值（20）
```

#### 3. ​指针与多维数组​

```c
int matrix[2][3] = {{1,2,3}, {4,5,6}};
int (*p)[3] = matrix; // 指向二维数组的指针
printf("%d", p[1][2]); // 输出 6
```

---

### ​（四）动态内存管理​

#### 1. ​堆内存分配​

```c
int *p = (int*)malloc(5 * sizeof(int)); // 分配5个int的空间
if (p != NULL) {
    p[0] = 10;
    free(p); // 必须手动释放内存
}
```

#### 2. ​常见错误​

- ​内存泄漏​：忘记释放内存。
- ​野指针​：释放后未置空指针。

```c
free(p);
p = NULL; // 防止野指针
```

---

### ​（五）指针与函数​

#### 1. ​指针作为函数参数​

```c
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
int x = 1, y = 2;
swap(&x, &y); // 交换 x 和 y 的值
```

#### 2. ​函数返回指针​

```c
int* createArray(int size) {
    return (int*)malloc(size * sizeof(int));
}
```

#### 3. ​函数指针​

```c
int add(int a, int b) { return a + b; }
int (*funcPtr)(int, int) = add; // 声明函数指针
printf("%d", funcPtr(2, 3));    // 输出 5
```

---

### ​（六）高级指针类型​

#### 1. ​指针的指针（多级指针）​​

```c
int x = 10;
int *p = &x;
int **pp = &p; // 二级指针
printf("%d", **pp); // 输出 10
```

#### 2. ​`void` 指针（通用指针）​​

```c
void *vp = &x;      // 可以指向任意类型
int *p = (int*)vp;  // 使用时需强制类型转换
```

#### 3. ​`const` 修饰指针​

- ​指向常量的指针​：

```c
const int *p = &x; // 不能通过 p 修改 x 的值
```

- ​指针本身为常量​：

```c
int *const p = &x; // p 的地址不可变
```

### 例题
#### 字符统计函数与指针
>试题描述
>>1)编写main 主函数。在其中定义字符数组,从键盘读取一个字符串,存入字符数组中。并调用s_count函数，在 main 主函数中输出s_count 函数回的多个统计数据。<br>2)编写s_count 函数。该函数的功能为:统计数字，字母，空格和其他字符的个数。要求函数的参数均为指针，并将统计出的各项数据值(int型)返回到主函数中，由主函数来输出。注意:不要改变函数名称,注意大小写敏感，注意数据类型的要求，注意不允许使用全局变量返回参数。
>___
>输入
>>输入只有一行。输入不多于 999个字符，以回车结束。
>___
>输出
>>输出s_count函数返回的数字,字母,空格和其他字符的个数,相邻的数据项之间用一个空格隔开。
>___
>数据范围
>>输入为字符串，输出为int 类型的整数。且输入字符串不多于 999 个字符
```C
#include <stdio.h>  
  
int char_count=0,symbol_count=0,num_count=0,space_count=0;//利用函数能改变全局变量的特点，进行值的传递

void s_count(char str[]){  
    char *p=str;  
    while (*p!='\0') {  
        if (*p>='a'&&*p<='z'||*p>='A'&&*p<='Z') {  
            char_count++;  
        }else if (*p>='0'&&*p<='9') {  
            num_count++;  
        }else if (*p==' '||*p=='\n'||*p=='\t') {  
            space_count++;  
        }else {  
            symbol_count++;  
        }  
        p++;  
    }  
}  
int main() {  
    char str[1000];  
    gets(str); //直接获取一行字符串  
    s_count(str);  
    printf("%d %d %d %d",num_count,char_count,space_count,symbol_count);  
}
```
___
#### 指针变量之函数参数作返回值 B
>试题描述
>>输入N个学生的C语言程序设计课程成绩,请你设计一个函数来编程找出这些学生的最高分、并列第一的学生数。函数原型:int search(int x\[],int n,int \*count)
>___
>输入
>>输入包含两行，第一行是 N(0<N<1000)，第二行是N个整数，代表N个学生的C语言程序设计课程成绩，邻近两数之间用一个空格隔开。
>___
>输出
>>按题目要求输出最高分和取得最高分的学生数，用一个空格隔开。
```C
#include <stdio.h>  
  
int search(int x[], int n, int *count) {  
    int max = x[0];  
    *count = 1;  
    for (int i = 1; i < n; i++) {  
        if (x[i] > max) {  
            max = x[i];  
            *count = 1;  
        } else if (x[i] == max) {  
            (*count)++;  
        }  
    }
    return max;  
}  
  
int main() {  
    int N;  
    scanf("%d", &N);  
    int scores[1000];  
    for (int i = 0; i < N; i++) {  
        scanf("%d", &scores[i]);  
    }  
    int count;  
    int max = search(scores, N, &count);  
    printf("%d %d", max, count);  
    return 0;  
}
```

___
---
## 七、文件操作

任何文件操作都遵循以下流程：1. ​打开文件​ → 2. ​读写数据​ → 3. ​关闭文件​

### 1. 打开文件：`fopen`​

```c
FILE *fopen(const char *filename, const char *mode);
```

- ​参数​：
    - `filename`：文件路径（如 `"data.txt"`）。
    - `mode`：打开模式（见下表）。
- ​返回值​：成功返回`FILE*`指针，失败返回`NULL`。

​常用模式​：

| 模式     | 描述                     |
| ------ | ---------------------- |
| `"r"`  | 只读（文件必须存在）             |
| `"w"`  | 只写（创建新文件/清空已有文件）       |
| `"a"`  | 追加（写入文件末尾）             |
| `"r+"` | 读写（文件必须存在）             |
| `"w+"` | 读写（创建新文件/清空已有文件）       |
| `"b"`  | 二进制模式（与上述模式组合，如`"rb"`） |

```c
FILE *fp = fopen("data.txt", "r");
if (fp == NULL) {
    perror("文件打开失败");
    exit(EXIT_FAILURE);
}
```
---
### ​2. 关闭文件：`fclose`

```c
int fclose(FILE *stream);
```

- ​必须调用​：释放系统资源，避免内存泄漏。
- ​返回值​：成功返回`0`，失败返回`EOF`。

```c
if (fclose(fp) != 0) {
    perror("文件关闭失败");
}
```

---

### ​3. 读写文件​

#### ​​(1) 文本文件操作​

- ​写入文本：`fprintf` / `fputs`

```c
fprintf(fp, "Name: %s, Age: %d\n", "Alice", 25);
fputs("Hello World!\n", fp);
```

- ​读取文本：`fscanf` / `fgets`

```c
char buffer[100];
fscanf(fp, "%s %d", name, &age); // 格式化读取（注意安全性）
fgets(buffer, sizeof(buffer), fp); // 读取一行
```

##### ​(2) 二进制文件操作​

- ​写入二进制：`fwrite`

```c
int data[] = {1, 2, 3};
size_t written = fwrite(data, sizeof(int), 3, fp);
```

- ​读取二进制：`fread`

```c
int buffer[3];
size_t read = fread(buffer, sizeof(int), 3, fp);
```

---

### ​4. 文件指针控制

- ​定位指针：`fseek` / `ftell`​

```c
fseek(fp, 0, SEEK_SET); // 移动到文件开头
long pos = ftell(fp);   // 获取当前指针位置
```

- ​重设指针：`rewind`

```c
rewind(fp); // 等价于 fseek(fp, 0, SEEK_SET)
```

### 例题
#### 宝宝读文件左移数列
>试题描述
>>已知文本文件 “le.xt 中连续存放了n(2<=n<= 1000)个整数，邻近两数之间用一个空格隔开。第一个数为文件中存放整数的总数n,后面n-1个数为具体的数值,这些数有正有负,也没有被排序编写程序，读入文件中的数，并且将后面n-1个数读入数组中。由于宝宝讨厌正数，想把这些数面左平移，移动规则是让数列中的最大值落在坐标轴原点上。宝宝的方法是先找出数列中的最大值然后将数列中的每个数都减去最大值，这样就实现数列向左平移了。<br>注意:1.路径及文件名为"fle.txt"，注意不要写路径。2.只允许使用只读方式打开文件。
>___
>输入
>>读文件输入
>___
>输出
>>输出减去最大值之后的 n-1个整数，邻近两数之间用一个空格隔开。
```C
#include <stdio.h>  
int main() {  
    FILE *fp;  
    int n,arr[1000], max, i;  
    fp = fopen("test.txt", "r");  
    fscanf(fp, "%d", &n);  
    for (i = 0; i < n-1; i++) {  
        fscanf(fp, "%d", &arr[i]);  
    }  
    fclose(fp);  
    max = arr[0];  
    for (i = 1; i < n-1; i++) {  
        if (arr[i] > max)  max = arr[i];  
    }  
    for (i = 0; i < n-1; i++) {  
        printf("%d ", arr[i]-max);  
    }  
}
```
___
___
## 附录
### 四种排序
#### 从小到大

方法一：穷举法（原始冒泡排序）<br>时间复杂度$O(n^2)$
```c
#include <stdio.h>  
void fun(int arr[], int t) {  
    int i,j;  
    for (i = 0; i < t-1; i++) {  
        for (j = 0; j < t-i-1; j++) {  
            if (arr[j] > arr[j+1]) {  
                int temp = arr[j];  
                arr[j] = arr[j+1];  
                arr[j+1] = temp;  
            }  
        }  
    }  
}  
int main() {  
    int N, arr[1000], i;  
    scanf("%d", &N);  
    for (i = 0; i < N; i++) {  
        scanf("%d", &arr[i]);  
    }  
    fun(arr, N);  
    for (i = 0; i < N; i++) {  
        printf("%d", arr[i]);  
        if (i != N-1) printf(" ");  
    }  
    printf("\n");  
}
```

方法二：双指针法（鸡尾酒排序）<br>时间复杂度：最好$O(n)$，最坏$O(n^2)$，接近$O(n^2)$
```c
#include <stdio.h>  
void fun(int arr[], int t) {  
    int left = 0,right = t - 1,j;  
    while (left < right) {  
        for (j = left; j < right; j++) {  
            if (arr[j] > arr[j + 1]) {  
                int temp = arr[j];  
                arr[j] = arr[j + 1];  
                arr[j + 1] = temp;  
            }  
        }  
        right--;  
        for (j = right; j > left; j--) {  
            if (arr[j - 1] > arr[j]) {  
                int temp = arr[j];  
                arr[j] = arr[j - 1];  
                arr[j - 1] = temp;  
            }  
        }  
        left++;  
    }  
}  
int main() {  
    int N, arr[1000], i;  
    scanf("%d", &N);  
    for (i = 0; i < N; i++) {  
        scanf("%d", &arr[i]);  
    }  
    fun(arr, N);  
    for (i = 0; i < N; i++) {  
        printf("%d", arr[i]);  
        if (i != N-1) printf(" ");  
    }  
    printf("\n");  
}
```

方法三：快速排序<br>时间复杂度：$O(n\log n)$，最坏$O(n^2)$，但是更接近于$O(n\log n)$
```c
#include <stdio.h>  
void quick_sort(int arr[], int left, int right) {  
    int pivot = arr[(left + right) / 2],i = left, j = right;  
    if (left >= right) return;  
    while (i <= j) {  
        while (arr[i] < pivot) i++;  
        while (arr[j] > pivot) j--;  
        if (i <= j) {  
            int temp = arr[i];  
            arr[i] = arr[j];  
            arr[j] = temp;  
            i++;  
            j--;  
        }  
    }  
    quick_sort(arr, left, j);  
    quick_sort(arr, i, right);  
}  
void fun(int arr[], int t) {  
    quick_sort(arr, 0, t - 1);  
}  
int main() {  
    int N, arr[1000], i;  
    scanf("%d", &N);  
    for (i = 0; i < N; i++) {  
        scanf("%d", &arr[i]);  
    }  
    fun(arr, N);  
    for (i = 0; i < N; i++) {  
        printf("%d", arr[i]);  
        if (i != N-1) printf(" ");  
    }  
    printf("\n");  
}
```

方法四：堆排序<br>时间复杂度：$O(n\log n)$
```c
#include <stdio.h>  
void heapify(int arr[], int n, int i) {  
    int smallest = i,left = 2 * i + 1,right = 2 * i + 2;  
    if (left < n && arr[left] > arr[smallest]) {  
        smallest = left;  
    }  
    if (right < n && arr[right] > arr[smallest]) {  
        smallest = right;  
    }  
    if (smallest != i) {  
        int temp = arr[i];  
        arr[i] = arr[smallest];  
        arr[smallest] = temp;  
        heapify(arr, n, smallest);  
    }  
}  
  
void heap_sort(int arr[], int n) {  
    int i;  
    for (i = n / 2 - 1; i >= 0; i--) {  
        heapify(arr, n, i);  
    }  
  
    for (i = n - 1; i > 0; i--) {  
        int temp = arr[0];  
        arr[0] = arr[i];  
        arr[i] = temp;  
        heapify(arr, i, 0);  
    }  
}  
  
void fun(int arr[], int t) {  
    heap_sort(arr, t);  
}  
  
int main() {  
    int N, arr[1000], i;  
    scanf("%d", &N);  
    for (i = 0; i < N; i++) {  
        scanf("%d", &arr[i]);  
    }  
    fun(arr, N);  
    for (i = 0; i < N; i++) {  
        printf("%d", arr[i]);  
        if (i != N-1) printf(" ");  
    }  
    printf("\n");  
}
```

#### 从大到小

方法一：穷举法（原始冒泡排序）
时间复杂度$O(n^2)$
```c
#include <stdio.h>
void fun(int arr[], int t) {
    int i,j;
    for (i = 0; i < t-1; i++) {
        for (j = 0; j < t-i-1; j++) {
            if (arr[j] < arr[j+1]) {
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}
int main() {
    int N, arr[1000], i;
    scanf("%d", &N);
    for (i = 0; i < N; i++) {
        scanf("%d", &arr[i]);
    }
    fun(arr, N);
    for (i = 0; i < N; i++) {
        printf("%d", arr[i]);
        if (i != N-1) printf(" ");
    }
    printf("\n");
}
```

方法二：双指针法（鸡尾酒排序）
时间复杂度：最好$O(n)$，最坏$O(n^2)$，接近$O(n^2)$
```c
#include <stdio.h>
void fun(int arr[], int t) {
    int left = 0,right = t - 1,j;
    while (left < right) {
        for (j = left; j < right; j++) {
            if (arr[j] < arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
        right--;
        for (j = right; j > left; j--) {
            if (arr[j - 1] < arr[j]) {
                int temp = arr[j];
                arr[j] = arr[j - 1];
                arr[j - 1] = temp;
            }
        }
        left++;
    }
}
int main() {
    int N, arr[1000], i;
    scanf("%d", &N);
    for (i = 0; i < N; i++) {  
        scanf("%d", &arr[i]);  
    }
    fun(arr, N);
    for (i = 0; i < N; i++) {  
        printf("%d", arr[i]);
        if (i != N-1) printf(" ");  
    }
    printf("\n");
}
```
方法三：快速排序
时间复杂度：$O(n\log n)$，最坏$O(n^2)$，但是更接近于$O(n\log n)$
```c
#include <stdio.h>  
void quick_sort(int arr[], int left, int right) {  
    int pivot = arr[(left + right) / 2],i = left, j = right;  
    if (left >= right) return;  
    while (i <= j) {  
        while (arr[i] > pivot) i++;  
        while (arr[j] < pivot) j--;  
        if (i <= j) {  
            int temp = arr[i];  
            arr[i] = arr[j];  
            arr[j] = temp;  
            i++;  
            j--;  
        }  
    }  
    quick_sort(arr, left, j);  
    quick_sort(arr, i, right);  
}  
void fun(int arr[], int t) {  
    quick_sort(arr, 0, t - 1);  
}  
int main() {  
    int N, arr[1000], i;  
    scanf("%d", &N);  
    for (i = 0; i < N; i++) {  
        scanf("%d", &arr[i]);  
    }  
    fun(arr, N);  
    for (i = 0; i < N; i++) {  
        printf("%d", arr[i]);  
        if (i != N-1) printf(" ");  
    }  
    printf("\n");  
}
```
方法四：堆排序
时间复杂度：$O(n\log n)$
```c
#include <stdio.h>  
void heapify(int arr[], int n, int i) {  
    int smallest = i,left = 2 * i + 1,right = 2 * i + 2;  
    if (left < n && arr[left] < arr[smallest]) {  
        smallest = left;  
    }  
    if (right < n && arr[right] < arr[smallest]) {  
        smallest = right;  
    }  
    if (smallest != i) {  
        int temp = arr[i];  
        arr[i] = arr[smallest];  
        arr[smallest] = temp;  
        heapify(arr, n, smallest);  
    }  
}  
  
void heap_sort(int arr[], int n) {  
    int i;  
    for (i = n / 2 - 1; i >= 0; i--) {  
        heapify(arr, n, i);  
    }  
  
    for (i = n - 1; i > 0; i--) {  
        int temp = arr[0];  
        arr[0] = arr[i];  
        arr[i] = temp;  
        heapify(arr, i, 0);  
    }  
}  
  
void fun(int arr[], int t) {  
    heap_sort(arr, t);  
}  
  
int main() {  
    int N, arr[1000], i;  
    scanf("%d", &N);  
    for (i = 0; i < N; i++) {  
        scanf("%d", &arr[i]);  
    }  
    fun(arr, N);  
    for (i = 0; i < N; i++) {  
        printf("%d", arr[i]);  
        if (i != N-1) printf(" ");  
    }  
    printf("\n");  
}
```
> 细心的人肯定发现了，这俩的区别就是改了个大小于号，所以背一个就行。
