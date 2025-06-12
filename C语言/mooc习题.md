## 第一章
### 1. 求两个整数之和
```C
#include <stdio.h>
int main(){
     int a,b;
     scanf("%d%d",&a,&b);
     printf("%d",a+b);
}
```
___
### 2. 字母的大小写转换问题
```C
#include <stdio.h>
int main(){
    char a;
    scanf("%c",&a);
    printf("%c",a-32);
}
```
___
### 3. 整型数据的拆分问题
```C
#include <stdio.h>
int main(){
    int n,a,b,c;
    scanf("%d",&n);
    c = n%10;
    b = n/10%10;
    a = n/100%10;
    printf("%d\n%d\n%d",a,b,c);
}
```
___
### 4. 字符型数据参与运算
```C
#include <stdio.h>
int main(){
    char m,n,temp;
    scanf("%c %c",&m,&n);
    temp = m;
    m = n;
    n = temp;
    printf("%c %c",m,n);
}
```
___
### 5. 求球体的表面积
```C
#include <stdio.h>
#define PI 3.1415
int main(){
    float r,S;
    scanf("%f",&r);
    S = 4*PI *r *r;
    printf("%.2f",S);
}
```
___
___
## 第二章
### 1. 学生成绩判断
```C
#include <stdio.h>
int main(){
    int grade;
    scanf("%d",&grade);
    if (grade<60) printf("failure");
    else printf("pass");
}
```
___
### 2. 4的倍数
```C
#include <stdio.h>
int main(){
    int n;
    scanf("%d",&n);
    if (n%4==0) printf("OK");
    else printf("NO");
}
```
___
### 3. 字符类型判断
```C
#include <stdio.h>
#include <ctype.h>

int main() {
    char c;
    scanf("%c", &c);
    
    if (isdigit(c)) {
        printf("数字\n");
    } else if (isupper(c)) {
        printf("大写字母\n");
    } else if (islower(c)) {
        printf("小写字母\n");
    } else {
        printf("其他类型\n");
    }
    
    return 0;
}
```
___
### 4.   三个数排序
```C
#include <stdio.h>

int main() {
    int a, b, c, temp;
    scanf("%d %d %d", &a, &b, &c);
    
    if (a > b) { temp = a; a = b; b = temp; }
    if (a > c) { temp = a; a = c; c = temp; }
    if (b > c) { temp = b; b = c; c = temp; }
    
    printf("%d %d %d\n", a, b, c);
    return 0;
}
```
___
### 5.  计算总金额
```C
#include <stdio.h>

int main() {
    float price;
    int x;
    scanf("%f %d", &price, &x);
    
    int discount_case;
    if (x < 5) discount_case = 0;
    else if (x < 10) discount_case = 1;
    else if (x < 20) discount_case = 2;
    else if (x < 30) discount_case = 3;
    else discount_case = 4;
    
    float discount;
    switch (discount_case) {
        case 0: discount = 0.00; break;
        case 1: discount = 0.01; break;
        case 2: discount = 0.02; break;
        case 3: discount = 0.04; break;
        case 4: discount = 0.06; break;
    }
    
    float total = price * x * (1 - discount);
    printf("%.2f\n", total);
    return 0;
}
```
___
___
## 第三章
### 1. 求1+1/2+1/3+......+1/n
```C
#include <stdio.h>

int main() {
    int n;
    scanf("%d", &n);
    
    double sum = 0.0;
    for (int i = 1; i <= n; i++) {
        sum += 1.0 / i;
    }
    
    printf("%.2f\n", sum);
    return 0;
}
```
___
### 2. 求素数
```C
#include <stdio.h>
#include <stdbool.h>

bool is_prime(int num) {
    if (num < 2) return false;
    for (int i = 2; i * i <= num; i++) {
        if (num % i == 0) return false;
    }
    return true;
}

int main() {
    int m, n;
    scanf("%d %d", &m, &n);
    
    bool first = true;
    for (int num = m; num <= n; num++) {
        if (is_prime(num)) {
            printf("%d,", num);
        }
    }
    return 0;
}
```
___
### 3. 统计并输出最高成绩
```C
#include <stdio.h>

int main() {
    int score, max = -1;
    
    while (1) {
        scanf("%d", &score);
        if (score < 0) break;
        if (score > max) max = score;
    }
    
    printf("%d\n", max);
    return 0;
}
```
___
### 4. s=a+aa+aaa+......+aa...aaa。
```C
#include <stdio.h>

int main() {
    int n, a, term = 0, sum = 0;
    scanf("%d %d", &n, &a);
    
    for (int i = 1; i <= n; i++) {
        term = term * 10 + a;
        sum += term;
    }
    
    printf("%d\n", sum);
    return 0;
}
```
___
### 5. 水仙花数
```C
#include <stdio.h>

int isNarcissistic(int num) {
    int original = num;
    int sum = 0;
    while (num > 0) {
        int digit = num % 10;
        sum += digit * digit * digit;
        num /= 10;
    }
    return sum == original;
}

int main() {
    int m, n, count = 0;
    scanf("%d %d", &m, &n);
    
    for (int i = m; i <= n; i++) {
        if (isNarcissistic(i)) {
            count++;
        }
    }
    
    printf("%d\n", count);
    return 0;
}
```
___
___
## 第四章
### 1. 数列首尾交换
```C
#include <stdio.h>

int main() {
    int n, arr[20];
    scanf("%d", &n);
    
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    
    for (int i = 0; i < n / 2; i++) {
        int temp = arr[i];
        arr[i] = arr[n - 1 - i];
        arr[n - 1 - i] = temp;
    }
    
    for (int i = 0; i < n; i++) {
        printf("%d,", arr[i]);
    }
    printf("\n");
    
    return 0;
}
```
___
### 2. 数学成绩统计
```C
#include <stdio.h>

int main() {
    int n, scores[30], sum = 0, count = 0;
    scanf("%d", &n);
    
    for (int i = 0; i < n; i++) {
        scanf("%d", &scores[i]);
        sum += scores[i];
    }
    
    float average = (float)sum / n;
    
    for (int i = 0; i < n; i++) {
        if (scores[i] < average) {
            count++;
        }
    }
    
    printf("%.1f\n%d\n", average, count);
    return 0;
}
```
___
### 3. 方阵对角线
```C
#include <stdio.h>

int main() {
    int n;
    scanf("%d", &n);
    int matrix[10][10];
    
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            scanf("%d", &matrix[i][j]);
        }
    }
    
    int sum_main = 0, sum_sec = 0;
    for (int i = 0; i < n; i++) {
        sum_main += matrix[i][i];
        sum_sec += matrix[i][n - 1 - i];
    }
    
    printf("%d %d\n", sum_main, sum_sec);
    return 0;
}
```
___
### 4. 字符串的子串
```C
#include <stdio.h>
#include <string.h>

int main() {
    char s1[100], s2[100];
    int k;
    
    fgets(s1, sizeof(s1), stdin);
    s1[strcspn(s1, "\n")] = '\0';
    
    scanf("%d", &k);
    strncpy(s2, s1, k);
    s2[k] = '\0';
    
    printf("%s\n", s2);
    return 0;
}
```
___
### 5. 字符串比较
```C
#include <stdio.h>
#include <string.h>

int main() {
    char s1[100], s2[100];
    fgets(s1, sizeof(s1), stdin);
    fgets(s2, sizeof(s2), stdin);
    
    s1[strcspn(s1, "\n")] = '\0';
    s2[strcspn(s2, "\n")] = '\0';
    
    int len1 = strlen(s1);
    int len2 = strlen(s2);
    
    for (int i = 0; ; i++) {
        char c1 = (i < len1) ? s1[i] : 0;
        char c2 = (i < len2) ? s2[i] : 0;
        
        if (c1 != c2) {
            printf("%d\n", c1 - c2);
            return 0;
        }
        
        if (i >= len1 && i >= len2) {
            printf("0\n");
            return 0;
        }
    }
}
```
___
___
## 第五章
### 1. 水仙花数
```C
#include<stdio.h>
int func(int n) {
    int a, b, c;
    a = n / 100; 
    b = (n / 10) % 10; 
    c = n % 10; 
    if (n == a * a * a + b * b * b + c * c * c) {
        return 1;
    }
    return 0;
}
int main() {
    int num, s;
    int func(int n);
    scanf("%d", &num);
    s = func(num);
    printf("%d", s);
    return 0;
}
```
___
### 2. 递归法求数
```C
#include <stdio.h>
int recursiveFunc(int n) {
    if (n == 1) {
        return 6;
    }
    return recursiveFunc(n - 1) + 3;
}

int main() {
    int n;
    scanf("%d", &n);
    int result = recursiveFunc(n);
    printf("%d\n", result);
    return 0;
}
```
___
### 3. 字符个数统计
```C
#include <stdio.h>
int fact(char str[]) {
    int count = 0;
    int i = 0;
    while (str[i] != '\0') {
        if (str[i] >= 'a' && str[i] <= 'z') {
            count++;
        }
        i++;
    }
    return count;
}

int main() {
    int res;
    char s[50];
    gets(s);
    res = fact(s);
    printf("%d", res);
    return 0;
}
```
___
### 4. 成绩统计
```C
#include <stdio.h>
int sum_scores(int *scores, int n) {
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += scores[i];
    }
    return sum;
}

int main() {
    int M, N;
    scanf("%d %d", &M, &N);
    int totals[M];
    for (int i = 0; i < M; i++) {
        int scores[N];
        for (int j = 0; j < N; j++) {
            scanf("%d", &scores[j]);
        }
        totals[i] = sum_scores(scores, N);
    }
    for (int i = 0; i < M; i++) {
        printf("%d,", totals[i]);
    }
    return 0;
}
```
___
### 5. 数据排序
```C
#include <stdio.h>
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] < arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

int main() {
    int n;
    scanf("%d", &n);
    int a[n];
    for (int i = 0; i < n; i++) {
        scanf("%d", &a[i]);
    }
    bubbleSort(a, n);
    for (int i = 0; i < n; i++) {
        printf("%d ", a[i]);
    }
    return 0;
}
```
___
___
## 第六章
### 1. 排序问题
```C
#include <stdio.h>
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
void bubbleSort(int *arr, int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (*(arr + j) > *(arr + j + 1)) {
                swap(arr + j, arr + j + 1);
            }
        }
    }
}

int main() {
    int a[10];
    int *p = a;
    for (int i = 0; i < 10; i++) {
        scanf("%d", p + i);
    }
    bubbleSort(p, 10);
    for (int i = 0; i < 10; i++) {
        printf("%d ", *(p + i));
    }
    return 0;
}
```
___
### 2. 求一组数据中的最大值和最小值
```C
#include <stdio.h>
void findMaxMin(int *arr, int n, int *max, int *min) {
    *max = *min = *arr;
    for (int i = 1; i < n; i++) {
        if (*(arr + i) > *max) {
            *max = *(arr + i);
        }
        if (*(arr + i) < *min) {
            *min = *(arr + i);
        }
    }
}

int main() {
    int n;
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    int max, min;
    findMaxMin(arr, n, &max, &min);
    printf("%d %d", max, min);
    return 0;
}
```
___
### 3. 统计字符串中空格的个数
```C
#include <stdio.h>

int main() {
    char str[100];
    fgets(str, 100, stdin);
    int count = 0;
    char *p = str;
    while (*p != '\0') {
        if (*p == ' ') {
            count++;
        }
        p++;
    }
    printf("%d", count);
    return 0;
}
```
___
### 4. 将字符串中的数字改为\*
```C
#include <stdio.h>
#include <string.h>
int main() {
    char str[100];
    fgets(str, 100, stdin);
    size_t len = strlen(str);
    if (len > 0 && str[len-1] == '\n') {
        str[len-1] = '\0';
    }
    char *p = str;
    while (*p != '\0') {
        if (*p >= '0' && *p <= '9') {
            *p = '*';
        }
        p++;
    }
    printf("%s", str);
    return 0;
}
```
___
### 5. 求方阵的转置矩阵
```C
#include <stdio.h>
void transposeMatrix(int *matrix, int n) {
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            int temp = *(matrix + i * n + j);
            *(matrix + i * n + j) = *(matrix + j * n + i);
            *(matrix + j * n + i) = temp;
        }
    }
}

int main() {
    int n;
    scanf("%d", &n);
    int matrix[n][n];
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            scanf("%d", &matrix[i][j]);
        }
    }
    transposeMatrix((int *)matrix, n);
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            printf("%d ", matrix[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```
___
___
## 第七章
### 1. 物品排序
```C
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int wi;
    int pi;
} Item;

int compare(const void *a, const void *b) {
    Item *itemA = (Item *)a;
    Item *itemB = (Item *)b;
    if (itemA->wi != itemB->wi) {
        return itemA->wi - itemB->wi;
    } else {
        return itemB->pi - itemA->pi;
    }
}

int main() {
    int n;
    while (scanf("%d", &n) == 1) {
        Item items[100];
        for (int i = 0; i < n; i++) {
            scanf("%d", &items[i].wi);
        }
        for (int i = 0; i < n; i++) {
            scanf("%d", &items[i].pi);
        }
        qsort(items, n, sizeof(Item), compare);
        for (int i = 0; i < n; i++) {
            printf("%d %d\n", items[i].wi, items[i].pi);
        }
    }
    return 0;
}
```
___
### 2. 单链表的链接
```C
#include <stdio.h>

int main() {
    int n,m;
    char A[90][2];
    scanf("%d",&n);
    for (int i = 0; i < n; i++) {
        scanf("%s",A[i]);
    }
    scanf("%d",&m);
    for (int i = n; i < m+n; i++) {
        scanf("%s",A[i]);
    }
    for (int i = 0; i < m+n; i++) {
        printf("%s ",A[i]);
    }
}
```
___
### 3. 遍历单链表(这也是我不推荐qsort的原因，配置复杂的很)
```C
#include <stdio.h>
#include <stdlib.h>

int cmpfunc(void *a, void *b) {
    int x = *(int *)a;
    int y = *(int *)b;
    if (x < y) return -1;
    if (x > y) return 1;
    return 0;
}

int main() {
    int n, arr[100];
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    qsort(arr, n, sizeof(int), cmpfunc);
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```
___
### 4. 删除单链表指定元素
```C
#include <stdio.h>  
  
int main() {  
    int n, m, arr[1000];  
    scanf("%d", &n);  
    for (int i = 0; i < n; i++) {  
        scanf("%d", &arr[i]);  
    }  
    scanf("%d", &m);  
  
    int filtered[1000], count = 0;  
    for (int i = 0; i < n; i++) {  
        if (arr[i] != m) {  
            filtered[count++] = arr[i];  
        }  
    }    int *p = filtered;  
    if (!*p) printf(" ");  
    else {  
        for (p; p < count+filtered; p++) {  
            printf("%d ", *p);  
        }  
        printf("\n");  
    }  
    return 0;  
}
```
___
### 5. 结构体练习
```C
#include <stdio.h>
#include <string.h>

typedef struct {
    char id[20];
    char name[20];
    float scores[3];
    float average;
} Student;

int main() {
    Student students[5];
    float totalScore = 0;
    int bestStudentIndex = 0;
    for (int i = 0; i < 5; i++) {
        scanf("%s %s %f %f %f", students[i].id, students[i].name, &students[i].scores[0], &students[i].scores[1], &students[i].scores[2]);
        float sum = students[i].scores[0] + students[i].scores[1] + students[i].scores[2];
        students[i].average = sum / 3;
        totalScore += sum;
        if (students[i].average > students[bestStudentIndex].average) {
            bestStudentIndex = i;
        }
    }
    float overallAverage = totalScore / (5 * 3);
    printf("%.2f\n", overallAverage);
    printf("%s %s %.2f %.2f %.2f %.2f\n", students[bestStudentIndex].id, students[bestStudentIndex].name,
           students[bestStudentIndex].scores[0], students[bestStudentIndex].scores[1],
           students[bestStudentIndex].scores[2], students[bestStudentIndex].average);
    return 0;
}
```