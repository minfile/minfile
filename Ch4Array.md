## Ch4 Array  
### Introduction Array
> Array多個相同類型數據按一定順序排列的集合  
> 使用一個名字命名，並通過編號方式對這些數據進行統一處理
> 創建數組，內存開闢一整塊**連續的空間**，而數組名中引用的是整塊連續空間**首地址**  
> 長度一旦確定，不能修改

### 一維數組
+ 一維數組的聲明和初始化
`type [] ;`  
`int a[];`  
`int [] a1;`
**動態初始化**
>數組為數組元素分配空間，與賦值是分開操作
```
int [] arr = new int[3];
arr[0] = 3;
arr[1] = 9;
```
**靜態初始化**
>在定義數組的同時就為數組元素分配空間並賦值
```
int arr [] = new int[] {1,2,3,5};
int arr[] = {1,2,3};
```
+ 如何調用數組指定位置的元素
+ 如何獲取數組的長度
+ 如何遍歷數組
+ 數組元素的默認初始化值
> 基本數據類型，默認初始化值各有不同
|Type| Star Value|
|-----|------|
|byte|0|
|short|0|
|int|0|
|long|0L|
|float|0.0F|
|double|0.0|
|char|0 \u000|
|boolean|false|
|引用|null|
> 引用數據類型，為null
+ 數組的內存解析
Stack: 局部變量  
Heap: new出來的結構: 對象、數據  
方法區: 常量池、靜態域  
```
String[] arr2 = new String[3];
arr2[1] = "Jack"；
arr2 = new String[5];
```
### 多維數組
**動態初始化**
```
//method 1
int [][] arr = new int[3][2];
//method 2
int [][] arr = new int[3][];
arr[0] = new int[3];
//int[][] arr = new int[][3]; 是不行的
```
**靜態初四化**
```
int [][] arr = new int[][]{{3,8,2},{2,7}};
```
`int p[ x,y[]; x是一維數組，y是二維數組`

### 數組涉及到的常見算法
