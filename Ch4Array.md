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
1. 數組元素的賦值(楊輝三角、回形數等)
2. 求數值型數組中元素最大值、最小值、平均數、總和等
3. 數組的複製、反轉、查找(線性查找、二分法查找)
4. 數組元素的排序算法
#### 楊輝三角
```
/*

使用二維複印打印一個10行楊輝三角。
【提示】
1.第一行有1個元素，第n行有n個元素
2.每一行的第一個元素和最後一個元素都是1
3.從第三行開始，對於非第一個元素和最後一個元
素的元素。即：
yanghui [i] [j] = yanghui [i-1] [j-1] + yanghui [i-1] [j];
*/

```
> 面試題目：創建一個 長度為6的int型陣列，要求取值為1-30，同時元素值各不相同
``` Java
 int array[] = new int[6];
       for (int i = 0;i<array.length;i++){
           array[i] = (int)(Math.random()*30+1);
          for(int j = 0;j<i;j++){
              if(array[i] == array[j]){
                  //array[i] = (int)(Math.random()*30+1);
                  i--;
                  break;
              }
          }

       }
        for(int k = 0;k<array.length;k++){
            System.out.println(array[k]);
        }
    }
```
> 面試題目：楊輝三角形

```Java

public class Ex1 {
    public static void main(String[] args) {
    int [][] a = new int[10][];
    for(int i =0;i<a.length;i++){
        a[i] = new int[i+1];
        for(int j=0;j<=i;j++){
            if(j==0 | j==i){
                a[i][j] = 1;

            }else {
                a[i][j] = a[i-1][j-1] + a[i-1][j];

            }
        }


    }
    for(int k = 0;k<a.length;k++){
        for(int l =0;l<k+1;l++){
            System.out.print(a[k][l]+"  ");
        }
        System.out.println("");
    }

    }

}


```
#### 回形數
```Java
class RectangleTest {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("输入一个数字");
		int len = scanner.nextInt();
		int[][] arr = new int[len][len];

		int s = len * len;
		/*
		 * k = 1:向右 k = 2:向下 k = 3:向左 k = 4:向上
		 */
		int k = 1;
		int i = 0, j = 0;
		for (int m = 1; m <= s; m++) {
			if (k == 1) {
				if (j < len && arr[i][j] == 0) {
					arr[i][j++] = m;
				} else {
					k = 2;
					i++;
					j--;
					m--;
				}
			} else if (k == 2) {
				if (i < len && arr[i][j] == 0) {
					arr[i++][j] = m;
				} else {
					k = 3;
					i--;
					j--;
					m--;
				}
			} else if (k == 3) {
				if (j >= 0 && arr[i][j] == 0) {
					arr[i][j--] = m;
				} else {
					k = 4;
					i--;
					j++;
					m--;
				}
			} else if (k == 4) {
				if (i >= 0 && arr[i][j] == 0) {
					arr[i--][j] = m;
				} else {
					k = 1;
					i++;
					j++;
					m--;
				}
			}
		}

		// 遍历
		for (int m = 0; m < arr.length; m++) {
			for (int n = 0; n < arr[m].length; n++) {
				System.out.print(arr[m][n] + "\t");
			}
			System.out.println();
		}
	}
}
```
### Arrays 工具類的使用
> java.util.Arrays類即為操作數組的工具類，包含了用作操作數組（比如排序和搜索）的各種方法
|語句|用法|
|--|--|
|boolean equals(int[]a, int[]b)|判斷2個數組是否相等|
|String toString(int [] a)|輸出數組信息|
|void fill(int [] a,int bal)|將指定值填充到數組之中|
|void sort(int[]a)|數組進行排序|
|int binarySearch(int[]a,int key)|對排序後的數組進行二分法檢索指定的值|

```Java
import java.util.Arrays;
public class SortTest {
public static void main(String[] args) {
int [] numbers = {5,900,1,5,77,30,64,700};
Arrays.sort(numbers);
for(int i = 0; i < numbers.length; i++){
System.out.println(numbers[i]);
}
}
}

```
