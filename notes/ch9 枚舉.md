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
## 註解
