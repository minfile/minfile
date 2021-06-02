# Ch9 枚舉類與註解
## 枚舉類
> 類的對象只有有限個,確定的。 距離如下:  
星期: Monday,Tuesday..Sunday  
性別: Man, Woman  
訂單狀態: Nonpayment, paid, delivered  
+ 当需要定义一组常量时，强烈建议使用枚举类
+ 如果枚舉類中只有一個對象,則可以用singleton的實現方式

### 自訂枚舉類
方法一:  
```java
//1. 私有化構造器 - 保證不能在類外部創建其對象

//2.在類的內部創建枚舉類的實例.聲明為: public static final

//3.對象如果有實例變量, 應該聲明為private final,並在構造器中初始化

class Season{
  //1. 聲明season對象的屬性: private final修飾 - 
  private final String seasonName;
  private final String seasonDesc;
  
  //2. 私有化類的構造器, 並給對象屬性賦值 - 保證不能在類外部創建其對象
  private Season(String seasonName, String seasonDesc){
    this.seasonName = seasonName;
    this.seasonDesc = seasonDesc;
  }
  //3. 提供當前枚舉類的多個對象: public static final. 
  public static final Season SPRING = new Season("春天","花開");
  public static final Season SUMMER = new Season("夏天","熱的");
  
  public String getSeasonName(){
        return seasonName;
  }
    public String getSeasonDesc(){
        return seasonDesc;
  }
    public String toString(){
        return "Season{" +
                "seasonName='" + seasonName + '\'' +
                ", seasonDesc='" + seasonDesc + '\'' +
                '}';
  }
} 
```
方法二: 使用enum定義枚舉類
> 使用enum定義的枚舉類默認繼承了java.lang.Enum類, 因此不能再繼承其他類  
> 枚舉類的構造器只能使用private權限修飾符  
> 枚舉類所有實例必須在枚舉類顯示列出(,分隔 ; 結尾).列出的實例系統會自動添加public static final修飾  
> 必須在枚舉類的第一行聲明枚舉類對象  
JDK 1,5 可以用switch表達式使用Enum定義枚舉類的對象作表達式
```
//使用enum關鍵字  
public enum SeasonEnum {
  //1.提供当前枚举类的对象，多个对象之间用","隔开，末尾对象";"结束
  SPRING("春天","春风又绿江南岸"),
  SUMMER("夏天","映日荷花别样红"),
  AUTUMN("秋天","秋水共长天一色"),
  WINTER("冬天","窗含西岭千秋雪");
  
//2.声明Season对象的属性:private final修饰
private final String seasonName;
private final String seasonDesc;

//3.私化类的构造器,并给对象属性赋值

private SeasonEnum(String seasonName, String seasonDesc) {
this.seasonName = seasonName;
this.seasonDesc = seasonDesc;
}

public String getSeasonName() {
return seasonName;
}
public String getSeasonDesc() {
return seasonDesc;
}
}
```

使用enum定義枚舉類之後，枚舉類常用方法: 

```
        //toString():返回枚舉類對象的名稱
        Season summer = Season.SUMMER;
        System.out.println(summer.toString()); //summer
        
        //values():返回所的枚舉類對象構成的數組
        Season value[] = Season.values();
        for(int i = 0; i<value.length;i++){
            System.out.println(value[i]); // SPRING SUMMER
        }
        //valueOf(String objName): 返回枚舉類中對象，若沒有對象則拋出異常
        Season sp = Season.valueOf("SPRING");
        System.out.println(sp); //SPRING
```
實現接口的枚舉類:
> 枚舉類可以實現一個或多個接口  
> 每個枚舉值在調用實現的接口方法呈現相同的行為方式，則只要同一實現該方法即可
> 若每個枚舉都有不同行為方式，則可以讓每個枚舉值分別來實現該方法
```
interface Info{
  void show();
}

public enum Season implements Info{
  SPRING("春天","開花"){
    public void show(){
      System.out.println("春天在哪裡?");
    }
  },
  SUMMER("夏天","炎熱"){
    public void show(){
      System.out.println("夏天在哪裡?");
    }
  };

}

```
## 註解  - JDK 5新增的功能
概述:  
> Annotation 其實就是代碼裡的特許標記, 這些標記可以在編譯，類加載，運行時被讀取，並執行相應的處理。  
> 使用annotation, 程序員可以在不改變原邏輯的情況下，在源文件中嵌入一些不從信息  
> 在JavaEE / Android中註解佔據了重要的角色，例如配置應用程序的任何切面，代替JavaEE舊版遺留的繁冗  
框架  = 注解 + 反射機制 + 設計模式

Annotation示例
**使用Annotation時，前面增加@符號，並把該Annotation當成一個修飾符使用**  

示例一: 生成文檔相關的註解
```
@author:表明開發該模塊的作者
@version: 標明類模塊的版本
@see: 參考轉向，也就是相關主題
@since: 從那個版本開始增加
@param: 對方法中的某參數說明 -方法 格式:@parm 形參名 形參類型 形參說明
@return: 對方法返回值說明 - 方法 格式@return 返回值類型 返回值說明
@exception: 可能拋出的異常說明 -方法 @exception 異常類型 異常說明
```
package com.annotation.javadoc;
/**
* @author shkstart
* @version 1.0
* @see Math.java
*/
public class JavadocTest {
/**
* 程序的主方法，程序的入口
* @param args String[] 命令行参数
*/
public static void main(String[] args) {
}
/**
* 求圆面积的方法
* @param radius double 半径值
* @return double 圆的面积
*/
public static double getArea(double radius){
return Math.PI * radius * radius;
}
}

```

示例二:在編譯時進行格式檢查(JDK內置的三個基本註解)
```
@Override: 限定重寫父類方法，該註解只能用於方法
@Deprecated: 用於表示所修飾的元素(類，方法等)已過時。
@SuppressWarnings: 抑制編譯器警告  

public class AnnotationTest{
  public static void main(String [] args){
    @SuppressWarnings("unused")
    int a = 10;
    
    @Deprecated
    public void print(){
      System.out.print("過時方法");
    }
    @Override
    public String toString() {
      return "重写的toString方法()";
    }
  }
}

```
示例三: 跟踪代碼依賴性，實現替代配置文件功能  
```Java
  //Servlet3.0提供了注解(annotation),使得不再需要在web.xml文件中进行Servlet的部署。
  @WebServlet("/login")
public class LoginServlet extends HttpServlet {
  private static final long serialVersionUID = 1L;
  protected void doGet(HttpServletRequest request, HttpServletResponse response) throws
  ServletException, IOException { }
  protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
doGet(request, response);
} }

```
自定義Annotation
定義新的Annotation類型使用@interface關鍵字
自定義註解自動繼承了java.lang.annotation.Annotation接口
* ② 内部定义成员，通常使用value表示
 * ③ 可以指定成员的默认值，使用default定义
 * ④ 如果自定义注解没成员，表明是一个标识作用。
@MyAnnotation(value="尚硅谷")
public class MyAnnotationTest {
  public static void main(String[] args) {
    Class clazz = MyAnnotationTest.class;
    Annotation a = clazz.getAnnotation(MyAnnotation.class);
    MyAnnotation m = (MyAnnotation) a;
    String info = m.value();
    System.out.println(info);
  }
}
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
@interface MyAnnotation{
  String value() default "auguigu";
}

4. 元注解 ：对现有的注解进行解释说明的注解。 
jdk 提供的4种元注解：
Retention：指定所修饰的 Annotation 的生命周期：SOURCE\CLASS（默认行为\RUNTIME
       只声明为RUNTIME生命周期的注解，才能通过反射获取。
       
Target:用于指定被修饰的 Annotation 能用于修饰哪些程序元素

*******出现的频率较低*******
Documented:表示所修饰的注解在被javadoc解析时，保留下来。
Inherited:被它修饰的 Annotation 将具继承性。

5. 如何获取注解信息:通过发射来进行获取、调用。
前提：要求此注解的元注解Retention中声明的生命周期状态为：RUNTIME.
6.JDK8中注解的新特性：可重复注解、类型注解

6.1 可重复注解：① 在MyAnnotation上声明@Repeatable，成员值为MyAnnotations.class
               ② MyAnnotation的Target和Retention等元注解与MyAnnotations相同。

6.2 类型注解：
ElementType.TYPE_PARAMETER 表示该注解能写在类型变量的声明语句中（如：泛型声明。
ElementType.TYPE_USE 表示该注解能写在使用类型的任何语句中。
