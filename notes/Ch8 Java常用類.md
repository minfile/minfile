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
10. int compareTo(String anotherString): 比較2字符串大小  
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
## 日期時間API

## Java比較器- 比較大小

## System類

## Math類

## BigInteger與BigDecimal
