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
2. 就緒: 處於新建狀態的線程被start()後，將進入線程隊列等待CPU時間片,此時它已具備運行的條件，只是沒分配到CPU資源
3. 運行: 進入運行狀態，run()方法定義了線程的操作和功能
4. 阻塞: 掛起執行/輸入輸出操作，讓出CPU並臨時終止自己的執行，進入阻塞狀態
5. 死亡: 線程完成了全部工作/線程被提前強制性地中止/出現異常導致結束

```mermaid
graph LR
A[新建] -->B[就緒]
B --> C[運行]
C --> D[阻塞]
D --> B
C --> E[死亡]
   
​```




