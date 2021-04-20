## Java Introduction Java介紹
### 語言概述
+ 1995: SUN (standford university network)推出的高級編程語言
+ 面相Internet編寫語言 - 可以在Web瀏覽器運行
+ Java開始時可以做客戶端 ------> 後來技術熟練可以做到後端開發
+ JavaSE: 技術體系平台標準版 支持桌面級應用
+ JavaEE: 開發企業環境下的一套解決方案,該技體系中包含的技術eg JSP, Servlet
+ JavaME: 移動端

### Java跟C++區別
相同:  
> Java被看成為C語言的洐生產物 eg變量聲明,操作符,參數傳遞等 
 
不同:  
> Java OOP語言，繼承了c++的OOP,但捨棄了指針和運算符重載, `增加垃圾回收器` 回收不再被引用對象所佔據的內存空間，枚舉，自動裝箱拆箱

### Java主要特徵
+ 面形對象  
  **基本概念**: class and Object
  **三大特徵**: 封裝、繼承、多態  
+ 健壯性  
  **吸收c++優點**: 指針，垃圾回收 更加安全  
  >Java有垃圾回收，還會有內存洩漏嗎? Yes
+ 跨平台性  
  **能在不同平台運行**: window,mac,linux   
  JVM: 只需要運行java程序的操作系統上即可。  
  

### JDK JRE
+ JDK  - 給Java開發人員使用
  JRE + 開發工具
+ JRE  - 開發環境
  JVM + JavaSE標準類庫
### Java註釋(comment)
+ 單行註釋  
  ` // xxxxxxx `
+ 多行註釋  
  `/*
  xxxxxxxxx
  //不能嵌套使用 則在/**/內再加/**/ 但是可以加//
  */`
+ 文檔註釋
  `/**
    註釋內容可被JDK提供的javadoc所解析，生成一套網頁文件
  */
  當代碼複雜了，可以開這個文檔給人看是做什麼的
  `
### API文檔
  >保存了Java所有的類庫 ，告訴開發者如何適用這些類
  
### 良好編程風格
  1. 正確使用註釋
  2. 正確縮進和空白
  3. 塊的風格
    >行尾風格 + 次行風格
  
### Java開發工具
  1. 文本編輯
  2. 集成開發環境IDE

***
### 每天測試區
1. JDK,JRE 和JVM關係,以及JDK 和 JRE包含什麼主要結構?、
2. 為什麼要設置path環境變量?如何設置?
3. 常用的幾個命令操作有哪些?
  
恭喜你學完Ch1啦!!  
你現在可以選擇:  
[Ch1 How to learn Java](https://github.com/minfile/minfile/blob/1cbf988b3e908f948ac6791743b970f63fd34ed5/Ch1_HowLearningJava.md)  
[Ch2 Java Introduction](https://github.com/minfile/minfile/blob/1cbf988b3e908f948ac6791743b970f63fd34ed5/Ch2HelloJava.md)  
[Ch3 Java Basic](https://github.com/minfile/minfile/blob/5a67622c4a1016ab332bda215f16982065ae72fc/Ch3Basic1.md)
