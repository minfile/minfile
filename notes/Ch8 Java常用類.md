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
tring s3 = new String("JavaEE");







## 日期時間API

## Java比較器- 比較大小

## System類

## Math類

## BigInteger與BigDecimal
