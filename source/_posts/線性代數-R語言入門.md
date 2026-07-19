---
title: "線性代數 - R語言入門"
date: 2018-12-24T20:24:42.000Z
tags:
  - "Linear Algebra"
categories:
  - "線性代數"
toc: true
---

# 線性代數 - R語言入門

-   時間 : 2018/12/25(二) 12:10 - 13:00
-   地點 : 學思樓040103教室
-   書籍 : [Linear algebra in R](https://www.math.uh.edu/~jmorgan/Math6397/day13/LinearAlgebraR-Handout.pdf)
-   程式碼 : [https://github.com/CaoCharles/Linear_Algebra_R](https://github.com/CaoCharles/Linear_Algebra_R)

## 簡介

介紹向量及矩陣在R語言的使用方法，並能使用R語言對向量及矩陣做基本運算。

## 基本安裝

[參考網頁](https://dotblogs.com.tw/michael80321/2014/12/15/147656)

-   前往([http://cran.csie.ntu.edu.tw/)安裝](http://cran.csie.ntu.edu.tw/\)安裝) R 程式
-   前往([https://www.rstudio.com/products/rstudio/download/)安裝RStudio](https://www.rstudio.com/products/rstudio/download/\)安裝RStudio)

## 下載教材

[教材網頁](https://github.com/CaoCharles/Linear_Algebra_R)

1.進入網頁點選綠色按鈕  
![](https://i.imgur.com/4IQdN6f.png)

2.點選Download ZIP 下載壓縮檔並解壓縮至桌面  
![](https://i.imgur.com/fb3V2wH.png)

3.開啟RStudio並點選File按下New Project  
![](https://i.imgur.com/y5zeKw9.png)

4.點選Existing Directory並選擇剛剛的資料夾  
![](https://i.imgur.com/BTPxMfL.png)

5.按下Create Project將專案匯入  
![](https://i.imgur.com/b6sd20X.png)

6.專案匯入即可執行程式碼  
![](https://i.imgur.com/KM8xaAY.png)

## 專案內容

RStudio右下角為專案資料夾檔案，可以點選不同檔案執行程式碼

-   共有3個程式碼檔案
    -   1_Vectors (向量基本運算)
    -   2_Augmented matrix (增廣矩陣基本運算)
    -   3_Matrices (矩陣基本運算)

執行程式碼的方式有下列幾種方式

-   點選R Script右上角Source執行全部程式碼
-   圈選要執行的範圍點選右上角Run執行程式碼
-   將滑鼠指標點選要執行的程式按下
    -   Ctrl + Enter 執行程式並換行
    -   Alt + Enter 執行程式不換行

### 向量基本運算

在R裡面使用c( )生成的向量都為 n x 1 的行向量，a *b 為兩向量相同位置的元素相乘，sum(a* b) 為兩向量內積的結果。

![](https://i.imgur.com/9fxbuaW.png)

### 增廣矩陣基本運算

-   [矩陣的等價關係](https://ccjou.wordpress.com/2011/04/26/%E7%9F%A9%E9%99%A3%E7%9A%84%E7%AD%89%E5%83%B9%E9%97%9C%E4%BF%82/)
-   [基本矩陣](https://ccjou.wordpress.com/2010/02/02/%E7%89%B9%E6%AE%8A%E7%9F%A9%E9%99%A3-%E5%8D%81%EF%BC%9A%E5%9F%BA%E6%9C%AC%E7%9F%A9%E9%99%A3/)

$x + 2y + 3z = 6$  
$2x - 3y +2z = 14$  
$3x + y - z = -2$

將增廣矩陣的運算過程用R語言程式來表達，要搞懂R語言矩陣的寫法及運算規則，再將複雜的運算過程用程式碼來執行。

![](https://i.imgur.com/mtipy5H.png)

### 矩陣基本運算

-   [伴隨矩陣](https://ccjou.wordpress.com/2012/06/27/%E4%BC%B4%E9%9A%A8%E7%9F%A9%E9%99%A3/)
-   [高斯消去法](https://ccjou.wordpress.com/2013/02/22/%E9%AB%98%E6%96%AF%E2%94%80%E7%B4%84%E7%95%B6%E6%B3%95/)

介紹矩陣一般常用的基本運算，並使用矩陣的列運算計算出其反矩陣，也可使用R語言專屬的套件計算其餘因子及伴隨矩陣，運用公式來計算其反矩陣。

![](https://i.imgur.com/27YCx05.png)
