# 107_2_ComputerOrganization_Midterm
107-2 計算機組織 期中專案

> 老師：朱守禮  
> 組別：第十三組  
> 班級：資訊二甲  
> 學生：10627107  黃立至  
> 學生：10627109  陳力維   
> 學生：10627150  林易賢  
> 學生：10627152  吳承宗  

## 背景
本次期中Project是以ModelSim撰寫，撰寫語法為Verilog，程式部分大略分為六部分，`ALU`, `Muitplier`, `Shifters`, `HiLo`, `Mux`, `Total ALU`。

### ALU  
包含`32-bits`的`AND`, `OR`, `ADD`, `SUB`, `SLT`等功能，alu由邏輯閘做起，其中`AND`, `OR`閘為較簡單的邏輯電路，而`ADD`, `SUB`兩項功能則多由`XOR`閘組
成(Full Adder)，至於`SLT`是利用`assign out = ( a < b ) ? 1 : 0`來實現。

### Multiplier  
乘法器主要由第一版乘法器方式設計，即每次乘法只看乘數的第0位元與被乘數的乘積，連續累加且每做下一次乘法之前將被乘數左移一位元( `<<` )，乘數右移一位元( `>>` )，直至乘數的32位元皆右移為0。

### Shifter  
主要以Barrel Shifter的方式實現，透過Mux_2to1此函式對每1`bit`進行移位，移位方式分成五種: 1、2、4、8、16 bits移位，其中`inputb`的前五個位元為判斷是否執行此五種位移的條件。

### HiLo  
將乘法器算出的64`bits`結果分成兩個32`bits`轉存至`Hi`, `Lo`暫存器。

### Mux  
透過`ALU Control`所給予的6 `bits`訊號，來選擇要輸出`ALU`, `Muitplier`, `Shifters`, 哪一個Output。

### Total ALU  
負責呼叫各類電路，完成算數及邏輯運算。

## 方法
![image](https://user-images.githubusercontent.com/51331397/183279322-41b139f4-954e-4f02-a14b-d86c86e11d05.png)
### ALU
![image](https://user-images.githubusercontent.com/51331397/183279329-83f00539-e301-44c3-9318-3c016d3d3bc3.png)
### Multiplier
![image](https://user-images.githubusercontent.com/51331397/183279338-bca1c744-b4b0-43f1-be71-25485424c5be.png)
### Shifter
![image](https://user-images.githubusercontent.com/51331397/183279342-e27297a4-a839-431a-b2b7-aa06f14dfaca.png)
### Mux
![image](https://user-images.githubusercontent.com/51331397/183279350-96fdeb43-7f15-4842-8bc1-a2efb4418998.png)

## 結果
Waveform輸出圖形。
### 輸入
![image](https://user-images.githubusercontent.com/51331397/183279441-ad70c4cb-af0a-4d17-9ee7-08e53dfac993.png)
### AND
inputA = 12, inputB = 10, output = 8  
![image](https://user-images.githubusercontent.com/51331397/183279566-847d58fc-e442-40eb-9e9a-25e7ae1a619f.png)
### OR
inputA = 12, inputB = 10, output = 14  
![image](https://user-images.githubusercontent.com/51331397/183279597-720320a7-adac-4f70-84c4-2152f1030f48.png)
### ADD
inputA = 12, inputB = 10, output = 22  
![image](https://user-images.githubusercontent.com/51331397/183279611-1a613e39-97a1-40f3-9ada-dc68a061a5fd.png)  
### SUB
inputA = 12, inputB = 10, output = 2  
![image](https://user-images.githubusercontent.com/51331397/183279634-db4a3987-0b78-473e-b5d2-0f6e96cbfcbc.png)  
### SLT
inputA = 12, inputB = 2, output = 0  
![image](https://user-images.githubusercontent.com/51331397/183279648-51ff90d9-105a-4154-84de-bf55e05b1bad.png)  
### SHIFT
inputA = 12, inputB = 2, output = 48
![image](https://user-images.githubusercontent.com/51331397/183279675-58d0b387-5af3-4086-953f-0cfcba2fe0b6.png)
### MULTI
inputA = 10, inputB = 3, output = 30  
![image](https://user-images.githubusercontent.com/51331397/183279713-ac8804f2-457e-4be4-aed3-7d36e99358d1.png)  

ModelSim驗證結果  
![image](https://user-images.githubusercontent.com/51331397/183279723-9c190265-9a56-4786-87fc-9bfaa11a0fd6.png)

## 討論  
這學期計組的期中Project相較於上學期組語Project，優: 編寫程式時變得方便許多，這次使用ModelSim，不用像上次需要到樹梅派模擬器裡撰寫，模擬器用起來不順手，滑鼠有時候還會亂飄；劣: 不像組語課本上那樣有程式碼&範例，計組的課本提供的多是概念，語法得要上網找資料慢慢試；寫的時候多半都是語法錯誤影響到資料的傳遞，在編譯的時候光是語法的錯誤就抓了好幾個小時，然而當語法沒問題後，接著面臨的是資料傳遞的問題，語法可以用，不代表是正確的，循序邏輯以及組合邏輯的語法更是不好理解。
