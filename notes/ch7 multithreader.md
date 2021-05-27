# Ch7 Multithreader多線程
程序Program - 是完成特定任務、用某種語言編寫的一組指令的集合 ，即指一段靜態代碼
進程progress - 是程序的一次執行過程/正在運行的一個程序，動態過程有生成，存在，消失
線程thread - 進程進一步細化。同一時間執行多個線程  

### 單核CPU和多核CPU
- 單核CPU是一種假多線程 - 在一個時間單元內，只能執行一個線程任務eg好多收費站，但只有一個工作人員
- 多核CPU是能更好發揮多線程  
- Java有至少3個線程main()主線程，gc() 垃圾回收線程, 異常處理線程

### 並行與並發
- 並行: 多個CPU同時執行多個任務eg 多個人同時做不同的事  
- 並發: 一個CPU同時執行多個任務eg 多個人同時做同一件事  

### 多線程優點
+ 提高應用程序的響應。對圖形化界面更有意義  
+ 提高計算機系統CPU的利用率  
+ 改善程序結構, 將長又複雜的進程分為多個線程，獨立運行，利於理解和修改  

### 何時需要多線程
+ 程序需要同時執行兩個或多個任務
+ 程序需要實現一些等待的任務，如用戶輸入、文件讀寫、文件操作搜索等  
+ 需要一些後台運行的程序

### 線程的創建和使用
**線程的創建和啟動**
- 每個線程都是Thread對象的run()方法來完成操作的，經常把run()方法稱為線程體  
- Thread對象的start()方法來啟動這個線程，而非直接調用run()

構造器
```
Thread(): 創建Thread的對象
Thread(String threadname): 創建線程並指定線程實例名
Thread(Runnable target): 指定創建線程的目標對象，他實現了Runnable接口中的run方法
Thread(Tunnable target,String name): 創建新的Thread對象
```
### 多線程創建方法
方法1: 繼承Thread類的方法
1. 定義子類繼承Thread類
2. 子類重寫Thread類中的run方法
3. 創建Thread子類對象
4. 調用線程對象start方法: 啟動線程,調用run

```
public class MyThread extends Thread{ //step 1
  public Mythread(){
  
  }
  public void run(){ //step2
    for(int i =0;i<100;i++) System.out.println(i);
  }
  
}
public class Demo{
  public static void main(String[] args){
    Mythread mt = new Mythread(); //step3
    mt.start(); //step 4
  }
}
```

> 注意事項  
> 如果手動調用run()方法，就只是普通方法，沒有啟動多線程  
> 調用start方法，啟動多線程
> 只能調用一次start()， 如果調多過一次，則拋出"IIIegalThreadStateException"

方法2: 實現Runnable接口的方法
Step 1: 實現Runnable接口
Step 2: 重寫Runnable接口中的run方法
Step 3: 通過Thread類含參構造器創建線程對象
Step 4: 將Runnable接口中的子類對象作為實際參數傳遞給Thread類的構造器
Step 5: 調用Thread的start方法
```
class MyThread implements Runnable{ //step1
  public void run(){ //step2
    System.out.println("thread is running");
  }
  public static void main(String [] args){
    MyThread mt = new MyThread();
    Thread th = new Thread(mt); //step3,step4
    th.start(); //step5
  }

}

```

### Thread繼承和Implements 區別
區別:
Extends: 線程代碼存放在Thread子類的方法中  
實現Runnable: 線程代碼存在接口的子類run方法中  

實現方式的好處:
避免單繼承的局限性  
多個線程可以共享同一個接口實現類的對象，非常適合多個相同線程來處理同一個資源  

### Thread類有關方法
```
void start(): 啟動線程，並執行對象的run()方法
run(): 線程在被調用的操作
String getName(): 返回線程名稱
void setName(String name): 設置該線程名稱
static Thread currentThread():返回當前線程。在Thread子類中就是this，通常用於主線程和Runnable實現類
static void yield(): 線程讓步 - 暫停當前執行的線程，把它讓給優先級相同或更高的線程
join(): 當某個程序執行調用其他線程的join()方法時，調用線程將被阻塞，直到join()方法加入的join線程執行完為止 - 低優先線程也可以獲得執行
static void sleep(long millis): (指定時間:毫秒)   - 令當前活動線程在指定時間內放棄對CPU控制
stop():強制線程聲明期結束 不推薦使用
boolean isAlive(): 判斷線程是否活著

```
Java的調度方法
> 同優先級線程組成先進縣出隊，使用時間片策略
> 對高優先級，使用優先調用的搶占式策略

```
MAX_PRIORITY:10
MIN_PRIORITY:1
NORM_PRIORITY:5

getPriority(): 返回當前線程優先值
setPriority(int newPriority): 改變線程的優先級

說明:
> 線程創建時繼承父線程的優先級  
> 低優先級只是獲得調度的概率低，並非一定是在高優先級線程之後才被調用

線程分類
- 守護線程: 用來服務用戶線程的，通過start()方法前調用thread.setDaemon(true) 把用戶線程變成守護線程
  - Java垃圾回收
  - 若JVM是守護線程，當前JVM退出
  
- 用戶線程: -運行前台的線程，而守護線程是運行在後台的線程

```
### 線程的生命週期
1. 新建: 當一個Thread或其子類的對象被聲明並創建時，新生的線程對象處於新建狀態
> 調用start

2. 就緒: 處於新建狀態的線程被調用start()後，將進入線程隊列等待CPU時間片,此時它已具備運行的條件，只是沒分配到CPU資源
> 去運行: 獲取CPU執行權

3. 運行: 進入運行狀態，run()方法定義了線程的操作和功能
> 去就緒: 失去CPU執行權/ yield()
> 去阻塞: sleep(long time),join(), wait(),suspend()
> 去死亡: 執行完run(), 調用線程stop(); 出現Error/ Exception且沒處理

4. 阻塞: 掛起執行/輸入輸出操作，讓出CPU並臨時終止自己的執行，進入阻塞狀態
> 去就緒: sleep()時間到, join()結束
> notify() / notifyAll(), resume()
 
5. 死亡: 線程完成了全部工作/線程被提前強制性地中止/出現異常導致結束

### 線程的同步
線程問題:
> 多個線程執行的不確定性引起執行結果的不穩定  
> 多個線程對賬本的共享，會造成操作的不完整性，會破壞數據
eg 當戶口有3000,你取2000 你家人取2000

問題出現原因:
> 當多條語句操作同一個線程共享數據時， 一個線程對多條語句執行了一部分，還沒有執行完，另一個線程參與進來執行，導致共享數據的錯誤

解決辦法:
- 只能讓一個線程都執行完，在執行過程中，其他線程不可以參與

### Synchronized的使用方法 - 同步機制

1. 同步代碼塊:

```Java
synchronized(對象){
  //需要被同步的代碼;
}
```

2. synchronized還可以放在方法聲明中，表示整個方法為同步方法
```Java
public synchronized void show(String name){
  ...
}

```

**synchronized的鎖是什麼?**
- 任意對象都可以作為同步鎖    
- 同步方法的鎖: 靜態方法(類名.class)、非靜態方法(this)  
- 同步代碼塊: 自己指定，很多時候也是指定為this或類名.class  
注意: 
必須確保使用同一資源的**多個線程共用一把鎖**, 靜態類名.class，非靜態this

### 同步的範圍（重要）
1. 如何找問題?即代碼是否存在線程安全?
+ 明確哪些代碼是多線程運行的代碼  
+ 明確多個線程是否有共享數據  
+ 明確多線程運行代碼中是否有多條語句操作共享數據  

2. 如何解決?
+ 對多條操作共享數據的語句，只能讓一個線程都執行完，在執行過程中，其他線程不可以參與執行

3. 切記
+ 範圍太小: 沒鎖住所有有安全問題的代碼
+ 範圍太小: 沒發揮多線程的功能

釋放鎖的操作
> 當前線程的同步方法、同步代碼塊執行結束
> 當前線程在同步代碼塊、同步方法中遇到break、return終止了該代碼塊、該方法的繼續執行
> 出現Erroe、Exception
> 有wait()方法

不會釋放鎖的操作
> 線程執行同步方法/同步代碼塊時，程序調用Thread.sleep()、Thread.yield()暫停當前線程執行
> 線程執行同步代碼塊時， 其他線程調用了suspend()

```
//singleton 瀨漢式
class Singleton{
  private sttaic Singleton instance = null;
  private Singleton(){}
  private static Singleton getInstance(){
    if(instance == null){
      synchronized(Singleton.class){
        if(instance == null){
          instance = new Singleton();
        }
      }
    }
    return instance;
  }
  
}
public Test{
  public static void main(String [] args){
    Singleton s1 = Singleton.getInstance();
    Singleton s2 = Singleton.getInstance();
    System.out.println(s1==s2) //true
  }

}

```

### 死鎖
> 不同線程分別佔用對方需要的同步資源不放棄，都在等待對方放棄自己需要的同步資源，就形成了死鎖  
> 出現死鎖後，不會出現異常，不會出現提示，只是所有的線程都處於阻塞狀態，無法繼續  
解決方法:
- 專門的算法、原則
- 盡量減少同步資源的定義
- 避免嵌套同步

### Lock(鎖)
> JDK 5.0後 加強線程同步機制
`java.util.concurrent.locks.Lock`接口是控制多個線程對共享資源進行訪問的工具。
> 鎖提供了對共享資源的獨占訪問，每次只能有一個線程對Lock對象加鎖，線程開始訪問共享資源之前應先獲得Lock對象
> ReentrantLock 類實現了Lock,它擁有與syncharonized相同的並發性和內存語義，在實現線程安全的控制中，比較常用的是reentrantLock，可以顯式加鎖、釋放鎖。


```
class A{
  private final ReentrantLock lock = new ReenTrantLock();
  public void m(){
    lock.lock();
    try{
      //保證線程安全的代碼;
    }finally{
      lock.unlock();
    }
  }
}
```
### synchronized與lock的對比
|Lock|Sysnchronized|
|--|--|
|是顯示鎖，手動釋放|隱式鎖，自動釋放|
|有代碼塊鎖|有代碼塊鎖和方法鎖|
|JVM將花費較少時間調度線程，性能更好，並具有更好擴展性||

優先使用順序:
Lock -> 同步代碼塊 -> 同步方法

### 線程的通訊
`wait()`: 令當前線程掛起並放棄CPU、同步資源並等待，使別的線程可訪問並修改共享資源，而當線程排隊等候其他線程調用notify()或notifyALL()方法喚醒，喚醒後等待重新獲得對監視器的所有權後才能繼續執行

`notify()`: 喚醒正在排隊等待同步資源的線程中優先級最高者結束等待  
`notifyAll()`: 喚醒正在排隊等待資源的所有線程結束等待  
**只能在synchronized方法或synchronized代碼塊中使用**，否則會出現Exception  

### wait()方法
在當前線程中調用方法: 對象名.wait()    
使當前線程進入等待(某對象)狀態，直到另一線程對該對象發出notify / notifyAll為止 - 重新獲得監控權，然後從斷點處繼續代碼的執行  
使用條件: 必須有監控權
使用該方法後: 當前線程將釋放對象監控權，進入等待  
### notify() / notifyAll()
調用方法: 對象名.notify()  
功能: 喚醒等待該對象監控器的一個/所有線程
調用方法條件: 當前線程將釋放對象監控權

### JDK5.0新增線程創建方法
方式一: 實現Callable接口
- Callable比Runnable功能更強大
- 相比run()方法，可以有返回值
- 方法可以拋出異常
- 支持泛型的返回值
- 需要借助Future Task

Future接口
 - 可以對具體Runnable、Callable任務的執行結果進行取消、查詢是否完成、獲取結果等
 - FutureTask是Future接口的唯一的實現類
 - FutureTask 同時實現了Runnable, Future接口。 它既可以作為Runnable被線程執行，有可以作為Future得到Callable的返回值

方式二: 線程池相關API
5.0的API: ExecutorService 和 Executors
ExecutorService: 真正的線程池接口

Executors: 工具類、線程池的工廠類
