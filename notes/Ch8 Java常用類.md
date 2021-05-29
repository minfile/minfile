# Ch8 Java常用類

## 字符串相關類  

**String的特性** 
> 代表字符串。所有字符串字面值都作為此類的實例實現
> String 是一個final類，不可變的字符序列 - 不可被繼承
> String 實現serializable接口:表示字符串支持序列化， Comparable接口，可以比較大小
> final char [] valie用於儲存字符串數量
> 不可變，但是當字符串重新賦值時，需要重寫自定內存區域賦值，不能使用原有的value進行賦值。 當你拼接新內容，也需要新造

```Java
public void Test1(){

  String s1 = "abc"; //字面量
  String s3 = "abc";
  s1 = "hello";
  
  System.out.println(s1==s3) //true --同一個地址值 內容有一樣就true，內容沒有一樣就是false
  System.out.println(s1) //hello
 
  String s4 = "abc";
   s4.replace('a','b') //也是創建新的區域
  
}
```
**String的實例化方式**
方式1: 通過字面量定義方法 - 聲明在方法去的字符串常量池  
`String str = "123";`  
方式2: 通過new +構造器 - 堆空間開闢空間以後，對應的地址值  
`String s3 = new String("123"); `  
`str == s3 //false`  

```Java
String s1 = "hello"; //在方法区
String s2 = "world";//在方法区
String s3 = s1+s2; //在堆内存
String s4 = s1+"world";//在堆内存
String s5 = (s1+s2).intern(); //把它指向方法区
String s6 = "helloworld";
  System.out.println(s3==s4); //false
  System.out.println(s5==s6); //true
  
```

String 常用方法:

1. int length(): 返回字符串長度  
2. char charAt(int index): 返回return value[index]  
3. boolean isEmpty(): 判斷是否是空字符串，retuen value.length ==0  
4. String toLowerCase(): 將字符串換成小寫  
5. String toUpperCase(): 將字符串換成大寫  
6. String trim(): 返回字符串的副本，忽略前導空白和尾部空白 
7. boolean equals(Object obj): 比較字符串的內容是否相同
8. boolean equalsIgnoreCase(String anotherString): 與equals一樣 忽略大小寫   
9. String concat(String str):將指定字符串連接到字符串的結尾。等於用"+"  
10. int compareTo(String anotherString): 比較2字符串大小, 如果大於就return 1,小於return -1 
11. String substring(int beginIndex): 返回一個新的字符串，它是此字符串的從beginIndex開始截取到最後一個字符串  
12 String substring(int beginIndex,int endIndex): 返回一個新字符串，它是有頭和尾index  
13. boolean endsWith(String suffix): 測試字符串是否以指定的后缀结束  
14. boolean startsWith(String prefix):測試字符串是否以指定的前缀開始
15. boolean startsWith(String prefix, int toffset): 測試此字符串從指定索引開始的字符串是否以指定前缀開始  
16. boolean contains(CharSequence s): 字符串包含指定的char值序列返回true
```
 String myStr = "Hello";
    System.out.println(myStr.contains("Hel")); //true
    System.out.println(myStr.contains("e")); //true
    System.out.println(myStr.contains("Hi")); //false

```
17. int indexOf(String str): 返回指定字符串在此字符串第一次出現的索引  
18. int indexOf(String str,int fromIndex)  
19. int lastIndexOf(string str)  
20. int lastIndexOf(String str,int fromIndex)   
21. String replace(char oldChar, char newChar)  
22. String replace(CharSequence target, CharSequence replacement)  
23. String replaceAll(String regax, String replacement)  
24. String replaceFirst(String regex, String replacement)  
25. boolean matches(String regex)  
```Java
 String Str = new String("www.runoob.com");

        System.out.print("返回值 :" );
        System.out.println(Str.matches("(.*)runoob(.*)")); //true
        
        System.out.print("返回值 :" );
        System.out.println(Str.matches("(.*)google(.*)")); //false

        System.out.print("返回值 :" );
        System.out.println(Str.matches("www(.*)")); //true

```
26. String [] split(String regex): 根據給定正則表達式的匹配拆分此字符串
27. String [] split(String regex, int limit), 拆分字符串，不超過limit個

**StringBuffer類**
> java.lang.StringBuffer代表可變的字符序列， 可以對字符串內容進行增刪，此時不會產生新的對象  
> 很多方法與String相同
> 作為參數傳遞時，方法內部可以改變值

StringBuffer的三個構造器:  
StringBuffer(): 初始容量為16的字符串緩衝區  
StringBuffer(int size): 構造指定容量的字符串緩衝區    
StringBuffer(String str):將內容初始化為指定字符串的內容  

StringBuffer類的常用方法: 
public int indexOf(String str)  
public String substring(int start, int end)  
public int length()  
public char charAt(int n)  
public void setCharAt(int n,char ch)  

**StringBuilder類**  
與StringBuffer相似， 可變的字符序列，而且提供相關功能方法也一樣

區別:
String(JDK1.0): 不可變字符序列  
StringBuffer(JDK1.0): 可變字符序列、效率低、線程安全  
StringBuilder(JDK 5.0): 可變字符序列、效率高、線程不安全

## 日期時間API
JDK8 之前日期時間API 
1. java.lang.System類  
public static long currentTimeMillis() 用來返回當前時間與1970年1月1日 0時0分0秒之間以毫秒為單位的時間差
計算世界時間主要標準有:
UTC(coordinated universal time)  
GMT(greenwich mean time)  
CST(Central Standaed Time)  

2. java.util.Date類  
表示特定的瞬間，精確到毫秒
構造器:
Date(): 使用無參構造器創建的對象可以獲取本地當前時間  
Date(long date)  

常用方法:
getTime(): 返回自1970年1月1日 00:00:00 GMT以來此Date對象表示的毫秒數  
toString(): 把此Date對象轉換為以下形式的String: dow mon dd hh:mm:ss zzz yyy  
dow: 一周中的某一天(Sun,Mon,Tue,Wed, Thu,Fri,Sat)  
zzz:時間標準

3. java.text.SimpleDateFormat類
Date類的API不易於國際化，大部分被廢棄了 java.text.SimpleDateFormat類是一個不與語言環境有關的方式來格式化和解析日期的具體類  
它允許進行 格式化: 日期->文本、解析:文本->日期

格式化:  
SmpleDateFormat(): 默認的模式和語言環境創建對象  
public SimpleDateFormat(String pattern): 構造方法可以用參數pattern指定的格式創建一個對象，該對象調用:  
public String format(Date date): 方法格式化時間對象date  

解析:
public Date parse(String source): 從給定字符串的開始解析文本，以生成一個日期  
```Java
Date date = new Date(); //產生一個Date的實例
//產生一個formater格式化的實例
SimpleDateFormat format = new SimpleDateFormat();
System.out.println(formater.format(date)); //打印默認的格式
SimpleDateFormat formater2 = new SimpleDateFormat("yyyy年MM月dd日 EEE HH:mm:ss");
System.out.println(formater2.format(date));

try{

  Date date2 = formater2.parse("2008年08月08日 星期一 08:08:08");
  System.out.println(date2.toString());
}catch(ParseException e){
  e.printStackTrace();
}

```
4. java.util.Calendar日曆類
Calendar是一個抽象基類，主要用於完成日期字段之間相互操作的功能  
獲取Calendar 實例方法  
  Calendar.getInstance() 方法  
  調用它的子類GregorianCalendar的構造器  
一個Calendar的實例是系統哦南方時間抽象表示，通過get(int field)方法來取得想要的時間信息。比如Year,Month, Day_of_week, Hour_of_day, Minute, Second  

public void set(int field,int value)   
public void add(int field, int amount)  
public final Date getTime()  
public final void setTime(Date date)  

JDK8中新日期時間API
java.time - 包含值對象的基礎包   
java.time.chrono - 提供對不同的日曆系統的訪問  
java.time.format - 格式化和解析時間和日期  
java.time.temporal - 包含底層框架和擴展特性  
java.time.zone - 包含時區支持的類  


## Java比較器- 比較大小

## System類

## Math類

## BigInteger與BigDecimal
