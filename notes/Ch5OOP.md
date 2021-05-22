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
|protect|yesy|yes|yes||
|public |ys|ys|ys|ys|

