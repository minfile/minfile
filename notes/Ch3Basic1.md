## Ch3 Basic

### 同一個class 可以有多個class類
```Java
class A{
  public static void main(String[] args){
  }
}

class B{

}

class C{

}
// 當你進行編譯的時候，會幫你輸出多個class file
```
### 標識符使用
> 凡是自己可以起名字都叫標識符 eg class name、變量名、方法名、接口名、包名
#### 標識符規則  
>如果不遵守 編譯不通過
1. 英文字母大小寫和 _ $組成
2. 數字不可開頭
3. 不可是關鍵字
4. Java嚴格區分大小寫
5. 標識符不能包含空格

### Java命名規範
Package Name: 多單詞組成 所有字母小寫xxxyyyy  
Class name: PxxYxx  
Variable name: xxYy
Constant Name:PPXXYY

### Variable
> 內存有一個存儲區域  
> 該區域的數據可以在同一類型範圍內不斷變化  
> 變量是程序中最基本存儲單位，包含`變量類型`、`變量名`和`存儲的值`  

### Variable function
**內存中保存數據**

### Variable use
格式:
`type name = value; `  
`int age = 20;`  
注意事項:
+ 變量必須先聲明、後使用
+ 變量都定義在其作用域內，在作用域內，它是有效的，換句話說，除了作用域就失效了  

### Variable data type
Primitive Type -  byte,short,int,long,float,double,char, boolean
Reference Type - class（String在這） , interface, array

|Data Type| Bits |   Math  |
|---------|-------|--------|
|Byte| 1 Byte = 8 bit| 2^(8)  = -128~127|
|short|2 Byte|2^(16)  =  |
|int |4 Byte|2^(32) =  |
|long (要l / L尾)| 8 Byte|2^(64) =  |
|float（要f 或 F）|4 Byte|          |
|double|8 Byte|         |
|char|排int後面，在short前面| 'x' '\n' '\u0043'|
|boolean| |true \ false |

### Variable transfer (只有7種數據類型)
#### Primitive Type
1. 自動轉換
> 當容量小的和容量大的做運算時，結果自動轉換
+ byte\ short\char -> int -> long -> float -> double
+ 當byte 、char、short做運算時，結果為int
```Java
char c1 = 'a';
int i3 = 10;
System.out.pringln(c1+i3);
```
3. 強制轉換
> 強制類型轉換，可能導致精度損失
```java
double d1 = 12.9;
int i = (int)dl
```
#### Reference Type
1. String variable 
+ 字符串，使用一對"", 由多個char組成
+ String可以和8個基本數據類型做運算 ,並只能是+ (運算後依然是string)
```Java
String a= "Hi";
int number = 123;
System.out.println(a+number); //Hi123
boolean b = true;
System.out.println(a+b); //Hitrue
```
練習
```Java
char c = 'a'; //97
int num = 10;
String str = "Hello";
System.out.println(c+num+str);                  //107Hello
System.out.println(c+str+num);                  //aHello10
System.out.println(c+(num+str));                //a10Hello
System.out.println((c+num)+str);                //107Hello
System.out.println(str+num+c);                  //Hello10a

//--------------------------------
System.out.println("*   *");
System.out.println('*'+'\t'+'*'); //93
System.out.println('*'+"\t"+'*');//*  *
System.out.println('*'+'\t'+"*"); //51*
System.out.println('*'+('\t'+"*"));//*  *
```
Excersice -can it run?
```
short s = 5;
s = s-2;                                        //no

byte b = 3;
b = b + 4;                                       //no
b = (byte)(b+4);                                 //yes

char c = ‘a’;
int i = 5;
float d = .314F;
double result = c+i+d;                            //yes

byte b = 5;
short s = 3;
short t = s + b;                                        //no

```
### 運算符

#### 三元運算符
(條件表達)?表達式1:表達式2
