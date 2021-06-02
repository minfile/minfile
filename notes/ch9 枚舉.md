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
class Season{
  //1. 聲明season對象的屬性: private final修飾
  private final String seasonName;
  private final String seasonDesc;
  
  //2. 私有化類的構造器, 並給對象屬性賦值
  private Season(String seasonName, String seasonDesc){
    this.seasonName = seasonName;
    this.seasonDesc = seasonDesc;
  }
  //3. 提供當前枚舉類的多個對象: public static final
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

```
## 註解
