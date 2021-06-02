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
```
引用數據: 字符串
+ 字符串转换成基本数据类型
通過構造器:
`int i = new Integer("12")`
通过包装类的parseXxx(String s)静态方法：
`Float f = Float.parseFloat("12.1")`
+ 字符串转换成基本数据类型
```
```
//调用字符串重载的valueOf()方法：
String fstr = String.valueOf(2.34f);
//更直接的方式：
String intStr = 5 + ""
```
---
### 關鍵字: Static
> 某些特定數據在內存只有一份
```
class Circle{
private double radius; //instance variable實例變量
public Circle(double radius){
this.radius = radius; 
}
static double radius = 12.0; 類變量
}
```
設計思想
> 分析哪些屬性**不因對象不同而改變**，將這些屬性設為類屬性
> 如果方法和調用者無關，則定義為類方法，不需要**創建對象就可以調用類方法**

使用範圍:
> static修飾: 屬性、方法、代碼塊、內部類

修飾後的特點:
+ 隨著類加載而加載
+ 優先於對象存在
+ 修飾的成員，被所有對象共享
+ 訪問權限允許時，可不創建對象，直接調用

`Person.total = 100;` 去訪問靜態成員
`Person.method1()`去訪問static方法
> **在static方法內，只能訪問static屬性**
> 因為static不需要實例，因此static不能有this(也不能有super)
> static修飾的方法不能被重寫

#### 單例設計模式(Singleton)
> 只能存在一個對象實例，並提供取得instance的方法
step 1: 構造器的權限設置為private 因此不能在外new對象
step 2: 調用靜態方法，以返回類內部創建的對象
step 3: 由於方法只能訪問靜態成員變量，必須是static
```
//餓漢式
class Singleton{
  private static Singleton singleton = new singleton();
  public static Singleton(){ }
  public static Singleton getInstance(){
    return singleton;
  }
}
//懶漢式 --- 存在線程安全問題
class Singleton{
  private Singleton(){ }
  private static Singleton single;
  public static Singleton getInstance(){
    if(single==null){
      single = new Singleton();
    }
    return single;
  }
}
```
+ 優點:
減少系統性能開銷 -> 一個對象的產生需要較多資源，如讀取配置、產生其他依賴對象時，則可以通過在應用啟動時直接產生一個單例對象，永久駐留內存的方式來解決

+ 應用場景:
網站計時器 - 易於同步
應用程序的日志應用 - 共享的日誌文件一直處於打開狀態
數據庫連接池 
讀取配置文件的類
application
task manager 任務管理器
recycle bin 回收站

### 理解main方法的語法
> 是public: 因為JVM 需要調用類的main()方法
> 是static: 因為不必創建對象，不能直接訪問該類的非靜態成員，必須創建實例，才能訪問
> 有String 參數: 保存執行Java命令時傳遞給所運行的類的參數

### 類的成員之四：代碼塊
作用:
> 對Java類/對象進行初始化
> 若代碼塊有修飾符，則只能被static修飾 - 靜態代碼塊
> 若沒有static修飾 - 非靜態代碼塊
```

class Program{
  public static int total;
  static{
    total = 100;
  }
}
```
| |靜態代碼塊|非靜態代碼塊|
|---|---|---|
|1. |可以有輸出語句|same|
|2. |可以對類的屬性、類的聲明進行初始化|same|
|3. |不可以調用非靜態的屬性和方法|可以調用靜態和非靜態方法和屬性|
|4. |多個代碼塊，則從上到下順序執行|same|
|5. |靜態代碼執行先於非靜態||
|6. |靜態代碼隨著類加載而加載，只執行一次|每次new object都只會執行一次，且先於構造器執行|

次序:
1. 聲明成員變量的默認初始化
2. 顯示初始化，多個初始化塊依次執行
3. 構造器對成員進行初始化
4. 通過對象.屬性/方法 賦值

### 關鍵字: final-"最終的"
> 可以聲明類、變量、方法
> final標記的類不能被繼承
> final標記的方法不能重謝
> final標記的變量 (要大寫) 只能賦值一次

### 抽象類與抽象方法
> 將一個父類設計得非常抽象，沒有具體實例，便是抽象類  
> 用abstract關鍵字修飾 -- 抽象類  
> 用abstract修飾一個方法 -- 抽象方法 -- 只有方法聲明，沒有方法實現，以分號結束`public abstract void talk();`  
> 含有抽象方法的類 必須 聲明為抽象類  
> 抽象類不能實例化，是用來被繼承的。抽像類的子類必須重寫父類的抽象方法，並提供方法體。 若沒有重寫，則是抽象類  
> 不能用abstract修飾變量、代碼塊、構造器  
> 不能用abstract修飾私有方法、靜態方法、final方法、final的類  
抽象類:
是用來模型化哪些父類無法確定全部實現，而是由子類提供具體實現的對象類

### 接口Interface
> 因為Java不支持多重繼承，有了接口就可以有多繼承  
> 必須從幾個類中抽取出一些共同的行為特徵，而他們之間又沒有is-a 關係。  
> 繼承是"是不是關係"，接口是"能不能關係"  
> 接口本質是契約，標準，規範的
接口是**抽象方法** 和 **常量值**定義的集合
接口特點:  
- 用Interface 定義
- 成員變量是默認為public static final
- 抽出方法默認為public abstract
- 接口**沒有構造器**
- 接口採用多繼承機制
接口定義舉例:
```
public interface Runner{
  int ID = 1; //public static final int ID = 1;
  void start(); //public abstract void start();
  public void run(); //public abstract void run();
  void stop();
}
```

定義Java類的格式: 先寫extends， 後寫implements
> 一個類可以繼承多個接口，接口可以繼承其他接口  
> 實現接口的類必須提供接口中所有方法具體內容，才可以實例化，否則依然是抽像類  
> 接口主要用途就是被實現類實現  
> 接口與類存在多態性
```
interface Runner { public void run();}
interface Swimmer {public double swim();}
class Creator{public int eat(){…}} 

class Man extends Creator implements Runner ,Swimmer{ //一個類可以實現多個無關接口
public void run() {……}
public double swim() {……}
public int eat() {……}
}
// 存在多態性
public class Test{
public static void main(String args[]){
Test t = new Test();
Man m = new Man();
t.m1(m);
t.m2(m);
t.m3(m);
}
public String m1(Runner f) { f.run(); }
public void m2(Swimmer s) {s.swim();}
public void m3(Creator a) {a.eat();}
}

```

#### 接口引用 - 代理模式(Proxy)
> 代理設計是為其他對象提供一種代理以控制對這個對象的訪問
```
interface Network{
  public void browse();
}
class RealServer implements Network{ //被代理
  public void browse(){
    System.out.println("真實服務器上網瀏覽信息");
  }
}
//代理類
class ProxyServer implements Network{
  private Network network;
  public ProxyServer(Network network){
    this.network = network;
  }
  public void check(){
    System.out.println("檢查網絡連接等操作");
  }
  public void browse(){
    check();
    network.browse();
  }

}

public class Demo{
  public static void main(String[] args){
    Network net = new ProxyServer(new RealServer());
    net.browse();
  }

}
```
應用場景: 
+ 安全代理: 屏蔽對真實角色的直接訪問
+ 遠程代理: 通過代理類處理遠程方法調用(RMI)
+ 延遲加載: 先加載輕量級的代理對象，真正需要加載真實對象

比如你要开发一个大文档查看软件，大文档中有大的图片，有可能一个图片有  
100MB，在打开文件时，不可能将所有的图片都显示出来，这样就可以使用代理  
模式，当需要查看图片时，用proxy来进行大图片的打开。  

在Java8中，可以為接口添加靜態方法/默認方法。  
靜態方法: 以static修飾，可以通過接口直接調用靜態方法  
默認方法：deault關鍵字修飾，可以通過實現類對象來調用

```
public interface AA {
double PI = 3.14;
public default void method() {
System.out.println("北京");
}
default String method1() {
return "上海";
}
public static void method2() {
System.out.println(“hello lambda!");
}
}
```
接口衝突:若2個接口有同名同參數方法
解決: 实现类必须覆盖接口中同名同参数的方法，来解决冲突。  

若一个接口中定义了一个默认方法，而父类中也定义了一个同名同参数的非
抽象方法，则不会出现冲突问题。因为此时遵守：类优先原则。接口中具有
相同名称和参数的默认方法会被忽略。
```
interface A{
  default void help(){System.out.println("老妈，我来救你了"); 
  }
}
interface B{
  default void help(){System.out.println("BB，我来救你了");
  }
}
class Man implements A,B{
  public void help(){
    System.out.println("what can i do?");
    A.super.help();
    B.super.help();
  }
}
```
### 類的內部成員之五: 內部類
內部類: 
> 一個事物的內部，還需要一個完整的結構進行描述，而這個內部的完整結構只為外部事物提供服務，那麼這個內部的完整結構是內部類
> 一般情況下，類和類之間是互相獨立的，內部類的意思就是打破這個獨立。讓一個類成另外一個類的內部成員，和成員變量、成員方法同等級別

分類:
成員內部類：
+ static
> 靜態內部類結構不需要依賴於外部類對象，類中的所有靜態組件都不需要依賴任何對象，可以直接通過類本身進行構造
```
public class Outerclass {
    public static void main(String[] args) {
        Outer ot = new Outer();
        ot.display();
        Outer.Inner in = new Outer.Inner();
        in.display();
    }
}

class Outer{
    private String name = "peter";
    public String getName(){
        return name;
    }
    public void display(){
        System.out.println(getName());


    }

    public static class Inner{
        private String innerName;
        public Inner(){
            innerName = "inner class";
        }

        public void display(){
            System.out.println("Inner class display");
            System.out.println(innerName);
        }

    }
}
```

+ 非static
> 將內部類當作外部類的
> 一個成員變量/成員方法來使用，所以必須依賴於外部類的對象才能調用，用法和成員變量/成員方法是一致的
為什麼使用內部類?
+ 可以隱藏細節和內部結構，封裝性更好，讓程序結構更加合理

```Java
public class HelloWorld{

     public static void main(String []args){
        //先New outerclass
        Outerclass ot = new Outerclass();
        System.out.println(ot.getName());
        
        //注意格式 - Classname . InnerClassname name = object.new innerClassname();
        
        Outerclass.InnerClass inner = ot.new InnerClass();
        System.out.println(inner.getName());
        
     }
}
class Outerclass{
    
    private String name = "peter";
    public String getName(){
        return name;
    }
    class InnerClass{
        String name = "inner";
        public String getName(){
            return name;
        }
    }
}

```
局部內部類(不談修飾符)
```
public class Outerclass {
    public static void main(String[] args) {
        Outer ot = new Outer();
        ot.display();
    }
}

class Outer{
    String name = "outer";
    public void display(){
        class InnerClass{
            String name = "inner";
            public void show(){
                System.out.println(name);
            }
        }
        //在方法內部創建
        InnerClass inner = new InnerClass();
        inner.show();
    }
}

```
匿名內部類
```
//正常是這樣的
public interface MyInterface {
    public void task();
}
public class MyImplement implements MyInterface{
  public void task(){
    System.out.println("do something");
  }
}

public class ImpleTest{
//正常做法
  MyInterface myinterface = new MyImplement();
  myinterface.task();
//匿名做法 -- 不需要單獨開一個文件，直接在裡面寫。缺點:耦合高
  MyInterface myinter = new MyInterface(){
    public void test(){
      System.out.println("匿名");
    }
  }
  myinter.test();
}

```

成員內部類作為類的成員角色
+ 可以聲明private / protected
+ 可以調用外部類的結構
+ 可以是static

成員內部類作為類的角色
+ 可以在內部定義屬性、方法、構造器
+ 可以聲明為abstract類
+ 可以聲明為final 的
+ 編譯以後生產OuterClass$InnerClass.class

注意:
1. 非static的成员内部类中的成员不能声明为static的，只有在外部类或static的成员
内部类中才可声明static成员。
2. 外部类访问成员内部类的成员，需要“内部类.成员”或“内部类对象.成员”的方式
3. 成员内部类可以直接使用外部类的所有成员，包括私有的数据
4. 当想要在外部类的静态成员部分使用内部类时，可以考虑内部类声明为静态的
```

class Outer {
  private int s;
  //內部類也可以當一個接口
  public class Inner {
    public void mb() {
    s = 100;
    System.out.println("在内部类Inner中s=" + s);
    }
  }
  public void ma() {
    Inner i = new Inner();
    i.mb();
  }
}
public class InnerTest {
  public static void main(String args[]) {
    Outer o = new Outer();
    o.ma();
  }
}
----------------
public class Outer {
  private int s = 111;
  public class Inner {
    private int s = 222;
    public void mb(int s) {
      System.out.println(s); // 局部变量s
      System.out.println(this.s); // 内部类对象的属性s
      System.out.println(Outer.this.s); // 外部类对象属性s
    }
}
public static void main(String args[]) {
  Outer a = new Outer();
  Outer.Inner b = a.new Inner();
  b.mb(333);
  }
}
```

如何聲明**局部內部類**
```
class 外部类{
  方法(){
    class 局部内部类{
      }
   }
{
class 局部内部类{
    }
  }
}

如何使用局部内部类
1. 只能在声明它的方法或代码块中使用，而且是先声明后使用。除此之外的任何地方
都不能使用该类
2. 但是它的对象可以通过外部方法的返回值返回使用，返回值类型只能是局部内部类
的父类或父接口类型

```
**局部内部类的特点**:

+ 内部类仍然是一个独立的类，在编译之后内部类会被**编译成独立的.class文件**，但
是前面冠以外部类的类名和$符号，以及数字编号。

+ 只能在声明它的 **方法** 或 **代码块** 中使用，而且是先声明后使用。除此之外的任何地方
都不能使用该类。

+ 局部内部类可以使用**外部类的成员，包括私有的。**  

+ 局部内部类可以使用外部方法的 **局部变量**，但是**必须是final的** 。由局部内部类和局
部变量的声明周期不同所致。  

+ 局部内部类和局部变量地位类似，不能使用**public,protected,缺省,private**  

+ 局部内部类不能使用static修饰，因此也不能包含静态成员  

匿名內部類:
> 匿名内部类不能定义任何**静态成员、方法和类**，只能创建匿名内部类的**一个实例**。一个匿名内部类一定是在new的后面，用其隐含实现一个接口或实现一个类。  

格式：
new 父类构造器（实参列表）|实现接口(){
//匿名内部类的类体部分
}
匿名内部类的特点: 
+ 匿名内部类必须**继承父类或实现接口**
+ 匿名内部类只能有一个对象
+ 匿名内部类对象只能使用**多态形式引用**
```
interface A{
  public abstract void fun1();
}
public class Outer{
  public static void main(String[] args) {
    new Outer().callInner(new A(){
    //接口是不能new但此处比较特殊是子类对象实现接口，只不过没有为对象取名
      public void fun1() {
        System.out.println(“implement for fun1");
      }
     }
  );// 两步写成一步了
}
  public void callInner(A a) {
    a.fun1();
  }
} 
```
