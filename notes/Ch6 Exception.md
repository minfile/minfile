# Exception 異常  

+ Error
> Java虛擬機無法解決的嚴重問題 eg StackOverFlowError, OOM
> 一般不編寫真對象的代碼

+ Exception
> 因編程錯誤/外在因素導致一般性的問題
> eg 空指針訪問, 讀取不存在的文件,網絡連接中斷, 數組角標越界

解決方法:
1. 終止程序運行
2. 錯誤處理

如何捕獲錯誤:
+ 編譯時異常 - 編譯期間
> 必須處理異常，外界因素造成的一般性異常

+ 運行時異常 - 運行時才發現
> 編程邏輯錯誤 eg `java.lang.RuntimeException` - 可以不做處理，若全處理會對程序可讀性/運行效率產生影響


### 常見異常
+ java.lang.RuntimeException  

  + ClassCastException
  ```
  public class Order {
    public static void main(String[] args) {
      Object obj = new Date();
      Order order;
      order = (Order) obj;
      System.out.println(order);
    }
   }
  ```
  + ArrayIndexOutOfBoundsException 
  ```
  String friends[] = { "lisa", "bily", "kessy" };
  for (int i = 0; i < 5; i++) {
  System.out.println(friends[i]); // friends[4]?
  }
  System.out.println("\nthis is the end");

  ```
  + NullPointerException  
  ```
  public class NullRef {
  int i = 1;
  public static void main(String[] args) {
    NullRef t = new NullRef();
    t = null; //把object變成null
    System.out.println(t.i);
    }
  }
  
  ```
  + ArithmeticException  
  ```
  public class DivideZero {
    int x;
  public static void main(String[] args) {
      int y;
      DivideZero c=new DivideZero();
      y=3/c.x;  // 錯誤因為x沒賦值
      System.out.println("program ends ok!");
    }
  }
  
  ```
  + NumberFormatException  
  + InputMismatchException  
  + ...
+ java.io.IOExeption  
  + FileNotFoundException
  + EOFException  
+ java.lang.ClassNotFoundException  
+ java.lang.InterruptedException  
+ java.io.FileNotFoundException  
+ java.sql.SQLException  

### 異常處理機制一: try-catch - finally

> Java的異常處理是抓拋模式 
> 如果出現異常，會生成一個**異常類對象**, 該異常對象將給Java運行系統，這個過程稱拋出(throw)異常

異常對象生成:
1. 自動生成:
> 虛擬機會在當前代碼找到相應的處理程序，在後台自動創建一個對應異常類的實例對象並拋出

2. 手動生成
```Java 
Exception exception = new ClassCastException();
//創建好的異常對象不拋出對程序沒有任何影響，和創建一個普通對象一樣
```


try-catch-finally 語句

```Java
try{
//捕獲異常
}catch(Exception e){
//處理異常
}catch(Exception e){

}finally{
//無論如何都要執行
}

//捕獲異常相關信息
getMessage() //獲取異常信息，返回字符串
printStackTrace() //獲取異常類名和異常信息，以及異常出現的位置，返回void

public class Sample{
  int x = 0;
  public static void main(String[]args){
     Sample sp = new Sample();
     int y;
      try{
        y = 12/sp.x; 
      }catch(ArithmeticException e){
       Systen.out.println("0 error");
      }finally{
        System.out.println("haha");
      }
  }
}
```
### 不捕獲異常的情況
> 前面的例子都是RuntimeException 類或是子類，即使沒有try 和 catch捕獲。 Java也能捕獲，並且編譯通過。  
> 但是，如果拋出的異常是IOException, 則必須捕獲，否則編譯錯誤。  


### 異常處理機制二: throws
> 如果一個方法可能生成某種異常，但是並不確定如何處理這種異常，則可以使用throws  
> throes 語句可以聲明拋出異常的列表，throws後面的異常類型可以是方法中產生的異常類型，也可以是父類

```
//方法中產生的異常類型
public void readFile(String file) throws FileNotFoundException{
...
}
public void readFile(String file) throws IOException{

}

//重寫方法不能拋出比被重寫方法範圍更大的異常類型
public class A {
  public void methodA() throws IOException {
  ……
  } }
  public class B1 extends A {
    public void methodA() throws FileNotFoundException {
     ……
   } }
  public class B2 extends A {
    public void methodA() throws Exception { //报错
      ……
    } }

```

### 手動拋出異常
step1: 創建要生成異常類對象，通過throw語句實現拋出操作
```
public class Outerclass {
    int day;
   public void checkDay(int day) throws Exception{ //step1
       this.day = day;
       if(day>30){
           throw new Exception("你的day大於30"); //step2
       }
   }

    public static void main(String[] args) {
        Outerclass ot = new Outerclass();
       try{                             //step3
            ot.checkDay(31);
        }catch (Exception e){
           System.out.println(e.getMessage());
       }
    }
}

```
### 用戶自定義異常類
> 一般用戶自定義異常類都是RuntimeException的子類  
> 自定義異常類通常需要編寫幾個**重載構造器**
> 自定義類的異常通常需要**提供serialVersionUID**  
> 通過throw拋出

```
//必須繼承
class MyException extends Exception{
  static final long servialVersionUID = 13212311L;
  private int idnumber;
  
  public MyException(String message,int id){
    super(message);
    this.idnumber = id;
  }
  public int getID(){
    return idnumber;
  }

}

public class Test{
  public void regist(int num) throws MyException{
  if(num<0) throw new MyException("不能這樣啊"); //注意throw沒有s
  }
  public void manager() {
    try {
        regist(100);
    } catch (MyException e) {
        System.out.print("登记失败，出错种类" + e.getId());
    }
        System.out.print("本次登记操作结束");
    }
    public sttaic void main(String [] args){
      Test t = new Test();
      t.manager();
  }
}

```
總結:
try-catch-finally:  
執行可能異常的代碼  
抓取異常  
無論如何都發生的代碼  

throw:  
在手動拋出異常對象時使用

throws:  
異常處理方式


