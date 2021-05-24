### Ch5 OOP  
#### the different between POP and OO  
(Procedure Oriented Programming)POP: more consider the step and the process how to do
(Object Oriented Programming)OOP: consider that class have what function and each step who reponsible to

### OOP feature
+ Encapsulation 封裝
+ Inheritance 繼承
+ Polymorphism 多態

### OOP introduction
+ class(類) and Object(對象) are the core concept
+ class is a desciption of thing so this is abstarct
+ Object is a real and instance
+ class have **Field屬性** , **Method方法**

### Class 格式
```
修飾符 class className{
  //filed
  //method
}
public class Person{
  private int age;
  public void showAge(int i){
    age = i;
  }
}
```
### Create and use object 
``` Java
//create
類名 對象名 = new 類名();
// use
對象名.對象成員 (可以是屬性，方法)
public class Zoo{
  public static void main(String args[]){
  //创建对象
  Animal xb=new Animal();
  xb.legs=4;//访问属性
  System.out.println(xb.legs);
  xb.eat();//访问方法
  xb.move();//访问方法
  }
}
```
### 類的訪問機制
> 類方法可以直接訪問類中的成員變量 (Static方法訪問非static ->error)  
> 在類中訪問機制 先創建喲訪問類的對象->在訪問成員變量  

### object life
```
Person p1 = new Person();
p1 = null // this object become rubiish
```

### 內存解析
Heap堆 - 存放對象實例，eg數組，對象Instance  
Stack棧 - 存儲局部變量，方法執行完，自動釋放
Method Area - 類信息、常量、靜態變量

### 類的成員之一: 屬性(field)
format:
> 修飾符 數據類型 屬性名 = 初始化值;
修飾符: private、缺省、protected、public  
其他修飾符: static、final  
```Java
public class Example{
  private int data = 10;
  public String name = "kelly";
}
```
分類:
- 成員變量: 在方法體外、堆空間 - 實例變量(不以static修飾)、類變量(以static修飾)
- 局部變量: 在方法體內、棧空間- 形參(方法/構造器的變量)、方法局部變量(在方法內)、代碼塊(在代碼塊內)
分別: 
相同: 都有生命週期  
不同: 局部變量除了形參外，都需要有初始化  
### 類的成員之二: 方法(method)  
什麼是方法?
> 對象行為的特徵，用來完成某個功能操作
> 目的: 代碼重用、簡化代碼   必須定義在類裡

```Java
修飾符 返回類型 方法名(數據類型 形參){
  return 返回值;
}
public void setAge(int age){
}
//沒有return 返回類型為void
//方法的結果應該返回給調用者，交由調用者處理
//方法中只能調用屬性/方法，不能在方法內定義方法  

```
### 方法重載(overload)
> 在同一個類，容許存在同一個方法名，但參數類型或數量不一樣即可
> 與返回類型無關。根據類型和數量區分
JavaSE 5.0 提供了Varargs機制，准許直接定義多個實參。
```
//5.0以前
public static void test(int a, String [] args);
//5.0後
public static void test(int a,String...books);
```
### 方法參數的值傳遞機制
> 形參: 方法聲明的參數
> 實參: 傳給形參的參數值

形參是基本數據類型: 傳遞**數據值**  
形參是引用數據類型: 傳遞**地址值** 

### 遞歸(Recursion)
> 循環、重覆執行某段代碼，但這種重負執行無需循環控制
```Java
public int sum(int num){
  if(num==1){
    return 1;
    }else{
     return num+sum(num-1);
    }
}
```

### 面向對象特徵之一: 封裝與隱藏
> 作用: 隱藏對象內部複雜性，只對外公開簡單接口。便與外界調用，從而提高系統的可拓展性、可維護性。
> 高內聚:類的內部數據操作細節自己完成，不允許干涉
> 低耦合:僅對外暴露少量方法用於使用

Java通過私有的private 再提供公共public的方法: getXxx(), setXxx()來操作

四種訪問權限修飾符
|修飾符|類內部|同一個包|不同包的子類|同一個工程|
|---|---|---|---|--|
|private|yes|||
|缺省|yes|yes|||
|protect|yes|yes|yes||
|public |ys|ys|ys|ys|

### 類的成員之三:構造器
特徵:
+ 具有與類相同的名稱
+ 沒有返回值
+ 不能被static final synchronized abstract native修飾

作用:
+ 創建對象，給對象進行初始化
`Order o = new Order();`

格式:
```
修飾符 類名(參數){
語句
}
public Animal(){

}
```

分類:
+ 隱式無參構造器(系統默認)
+ 顯示定義多個構造器
> 至少一個構造器、默認構造器修飾符與類修飾符一樣、定義了構造器系統則不使用默認、可以overload、父類構造器不能被子類繼承

### 屬性賦值過程
1. 默認初始化
2. 顯示初始化
3. 構造器
4. 通過對象.屬性 / 對象.方法賦值

### 關鍵字: this
this作用:
> 調用類的屬性、方法和構造器
this使用:
> 需要調用該類方法、屬性、構造器

+ 可以在類構造器使用`this(形參)` 調用本類其他構造器
+ 一個構造器最多只能聲明一個**this()**

### 關鍵字package、import
package:
> 定義類所在的包
`package 頂層包名.子包名;`
作用:
+ 幫助管理大型軟件系統:將功能相近類劃分到同一個包: MVC設計模式
+ 便於管理
+ 解決重名問題
+ 控制線職權

### MVC設計模式
model 模型層(處理數據)
> model.bean/domain 數據對象封裝
> model.dao 數據庫操作 
> model.db 數據庫
controller 控制層(處理業務邏輯)
> controller.acitivity 引用界面相關
> controller.fragment 存放fragment
> controller.adapter 顯示列表適配器
> controller.service 服務器
> controller.base 抽取基類
view顯示數據
view.utils 工具類
view.io 自定義的view
controller -> model -> view

### 包
java.lang - 核心類
java.net - 與網絡相關接口/類
java.io - 輸入輸出
java.util - 工具類
java.text - java格式化相關的類
java.sql - 數據庫接口
java.awt - 抽象窗口工具 GUI
`import 包名.類名;`

--------------------------------------
### 面向對象特徵之二: 繼承 inheritance
為什麼要inheritance?
> 多個類中存在相同屬性與行為時，將這些內容抽取到單獨類  
多個類稱子類(subclass)，單獨類父類(superclass)
“subclass is a superclass”
語法規則:
`class Subclass extends Superclass{}`
作用:
+ 提高复用性
+ 利於功能曠張
+ 多態前提

特徵:
+ 子類繼承父類，就繼承父類屬性和方法，也可以創建新的屬性/發那個發
+ **不能直接訪問private的成員變量和方法**-要get set
+ 只支持單繼承和多層繼承

### 方法重寫 override/overwrite
定義:
> 子類可以根據父類繼承來的方法進行改造。子類的方法覆蓋父類發那個發
要求:
+ 重寫方法名和參數一樣
+ 返回值類型不能大於父類返回值
+ 訪問權限不能小於父類
+ 子類拋出異常不能大於父類重寫方法異常
**非static才重寫，或同時static(不是重寫)**

### 關鍵字: super
> 可以訪問父類的屬性、成員方法、構造器
> *尤其出現自父類同名成員，便用super
> super不僅限於直接父類
> 子類默認父類中的空參數構造器

### 面向對象特徵之三: 多態性 Polymophsim
作用:
+ 提高代碼通用性，作接口重用
前提:
+ 需要有繼承
+ 方法重寫
成員方法:
+ 編譯看左邊，執行看右邊
成員變量:
+ **不具備多態**
> 父類引用指向子類object
> 可以應用在抽象類和接口
引用變量類型: 編譯時類型 | 運行時類型
> 編譯看左邊，運行看右邊
如果左和右類型不一樣，便是polymorphism **子類對象替代父類對象使用**
```java
# upcasting -父類指向子類
Person p = new Student();
Object o = new Person();

// 編譯非法 - 編譯看左邊，左邊必須能通過
```
#### Instanceof操作符
```
//X instancceof A: 檢查x是不是為A的對象，返回boolean
public class Person extends Object {…}
public class Student extends Person {…}
public class Graduate extends Person {…}
-------------------------------------------------------------------
public void method1(Person e) {
if (e instanceof Person) 
// 处理Person类及其子类对象
if (e instanceof Student) 
//处理Student类及其子类对象
if (e instanceof Graduate)
//处理Graduate类及其子类对象
}
```
#### 對象類型轉換
向上轉型: 子類-> 父類 多態
向下轉型: 父類->子類 使用instanceof判斷

### Object 類使用
Object是所有Java類的根父類
#### == 和 equals
==:
基本數據類型比較: 只要2個變量值相等，即為true
引用類型比較(是否指向同一對象): 如是同一對象 true
equals(): 繼承object，獲得equals()方法，可以重寫
`obj1.equals(obj2)`
> 當用equals()方法進行比較，對於file、String、Date及包裝類 是比較類型及內容而不考慮是否引用同一對象 原因是:重寫equales()

#### toString()方法
> toString()在Object class定義，返回值是String,返回類名和地址
```
Date now=new Date();
System.out.println(“now=”+now); 相当于
System.out.println(“now=”+now.toString());

可以根据需要在用户自定义类型中重写toString()方法
如String 类重写了toString()方法，返回字符串的值。
s1=“hello”;
System.out.println(s1);//相当于System.out.println(s1.toString());
基本类型数据转换为String类型时，调用了对应包装类的toString()方法
int a=10; System.out.println(“a=”+a);

```
### 包裝類使用 Wrapper class
基本數據類型--裝箱
```
int i = 500;
Integer t = new Integer(i);
Float f = new Float("4.56");

//猜箱
boolean b = bObj.booleanValue();
// JDK1.5之后，支持自动装箱，自动拆箱。但类型必须匹配。

```
引用數據: 字符串
+ 字符串转换成基本数据类型
通過構造器:
`int i = new Integer("12")`
通过包装类的parseXxx(String s)静态方法：
`Float f = Float.parseFloat("12.1")`
+ 字符串转换成基本数据类型
```
调用字符串重载的valueOf()方法：
String fstr = String.valueOf(2.34f);
 更直接的方式：
String intStr = 5 + “”
```
