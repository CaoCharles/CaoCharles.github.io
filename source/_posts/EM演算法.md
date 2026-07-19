---
title: "EM演算法"
date: 2018-08-28T09:31:35.000Z
tags:
  - "EM"
  - "Algorithm"
categories:
  - "機器學習"
toc: true
---

[參考網址](https://www.jianshu.com/p/1121509ac1dc)  
[Maximum Likelihood from Incomplete Data via the EM Algorithm](http://web.mit.edu/6.435/www/Dempster77.pdf)

* * *

**最大期望演算法**（**Expectation-maximization algorithm**，又稱**期望最大化算法**）  
在資料分析中常用於分群，在給定群數及機率模型下，去尋找觀測值變數間的所隱藏的訊息，可用此演算法來估計機率模型中的參數估計或遺失值填補。

* * *

## 名詞介紹

-   樣本: $x$
    
-   概似函數: $L(\theta|x)=p(x|\theta)$
    
-   目的: 找到能讓 $L(\theta|x)$ 最大化的參數
    

我的想法就是找到符合我們樣本資料的”最大”概似函數的機率模型參數，  
以往都是假設好機率模型中的參數，並計算其MLE，  
現在透過樣本及樣本所隱藏的隱變數，來推導適合這些樣本的模型參數。

## 思考

-   argument : $y$ (遺失值或是隱變數)
-   complete-data likelihood : $L(\theta|x,y)=p(x,y|\theta)$ 加入隱變數後完整的概似函數
-   What about $max_\theta L(x,y)$?
-   need to recursively update y and $\hat\theta$?

## E步驟(更新y)

根據現在給定的模型參數及樣本觀測值，我們去計算其log完整概似函數的期望值如下:  
$$Q(\theta|\theta^{(t)})\equiv E_y[log p(x,y|\theta)|x,\theta^{(t)}]$$

## M步驟(更新參數$\theta$)

最大化E步驟獲得的期望值  
$$\theta^{(t+1)} = arg max_\theta Q(\theta|\theta^{t})$$

**重複上述過程直到收斂**

## EM推導

-   $X:observed \space data$
-   $Y:latent\space variable$

$Log\space likelihood \space function$

$$ l(\theta) $$

$$= lnP(X|\theta) $$

$$= ln\sum_yP(X,y|\theta) $$

$$= ln(\sum_yP(X,y|\theta))\frac{Q(y)}{Q(y)}$$

$$\ge\sum_yQ(y)ln\frac{P(X,y|\theta)}{Q(y)} $$

$$\because log \in concave\space by\space Jensen’s\space inequality $$

$$(解決ln\sum 不好計算的問題，Q:機率分配) $$

$$= E_Q(ln\frac{P(X,y|\theta)}{Q(y)})$$

在$Jensen’s \: inequality 中，當E(x)中，x=常數時，等號成立。$

$$\Rightarrow\frac{P(X,y|\theta)}{Q(y)}=c \in Constant，且\sum_yQ(y)=1$$

$$\Rightarrow\sum_yP(X,y|\theta)=c\sum_yQ(y)=c$$

$$\Rightarrow Q(y)=\frac{P(X,y|\theta)}{\sum_yP(X,y|\theta)}=P(y|x_i,\theta)$$，

$$Q:在樣本給定下之隱藏變數條件分布$$

$$\therefore E_Q(ln\frac{P(X,y|\theta)}{Q(y)})=E_y(ln\frac{P(X,y|\theta)}{P(y|x_i,\theta)}|X,\theta)$$

$$\theta^{(t+1)}=arg\max\limits_\theta l(\theta)\Longleftrightarrow arg\max\limits_\theta\sum_{y}P(y|x_i,\theta^{(t)})ln\frac{P(X,y|\theta)}{P(y|x_i,\theta^{(t)})}$$

$$\: \: \Longleftrightarrow arg\max\limits_\theta\sum_{y}P(y|x_i,\theta^{(t)})lnP(X,y|\theta)=E_y(lnP(X,y|\theta)|X,\theta^{(t)})=Q(\theta|\theta^{(t)})$$

$$\therefore E-step :Find \: Q(\theta|\theta^{(t)})$$

$\Longleftrightarrow$ Find the expectation of the complete-data loglikelihood with respect to the missing data y given the observed data x and the current parameter estimates $\theta^{(t)}$.

$$M-step=\theta^{(t+1)}=arg\max\limits_\theta Q(\theta|\theta^{(t)})$$

## EM收斂性

* * *

## 範例1

197 animals are distributed multinomially into four categories with cell-probabilities$(\frac{1}{2}+ \frac{\theta}{4}, \frac{(1-\theta)}{4}, \frac{(1-\theta)}{4}, \frac{\theta}{4})$, where $\theta \in (0,1)$is unknown

Observed Data:  
$$x=(x_1,x_2,x_3,x_4)=(125,18,20,34)$$

Likelihood:  
$$L(\theta；x)=\frac{n!}{x_1!x_2!x_3!x_4!}(\frac{1}{2}+\frac{\theta}{4})^{x_1}(\frac{1}{4}-\frac{\theta}{4})^{x_2}(\frac{1}{4}-\frac{\theta}{4})^{x_3}(\frac{\theta}{4})^{x_4}$$

Find MLE by maximizing loglikelihood

Now use EM to find MLE

假設我們的隱藏變數在a裡面，令$y=x_{11}+x_{12}$

完整的變數擴展為$(x_{11},x_{12},x_{2},x_{3},x_{4})$有5個

初始其參數 $(\frac{1}{2}, \frac{\theta}{4}, \frac{1}{4}-\frac{\theta}{4}, \frac{\theta}{4})$

其概似函數如下

$$L(\theta；x)=\frac{n!}{x_{11}!x_{12}!x_2!x_3!x_4!}(\frac{1}{2})^{x_{11}}(\frac{\theta}{4})^{x_{12}}(\frac{1}{4}-\frac{\theta}{4})^{x_{2}+x_{3}}(\frac{\theta}{4})^{x_{4}}$$

-   E 步驟

給定機率模型參數$\theta^{(t)}$和$(x_1,x_2,x_3,x_4)$，$$x_{11}=\frac{2x_{1}}{2+\theta}\quad and \quad x_{12}=\frac{\theta x_{1}}{2+\theta}$$

推導Q函數(令$y=x_{12}$)  
$$Q(\theta |\theta^{(t)})=E_y[log p(x,y|\theta)|x, \theta^{(t)}]$$

$$=E_y[(x_{12}+x_{4})log\theta +(x_{2}+x_{3})log(1-\theta)|x,\theta^{(t)}]$$

$$=(E_y[x_{12}|x, \theta^{(t)}]+x_{4})log\theta +(x_{2}+x_{3})log(1-\theta)$$

$$=(\frac{\theta^{(t)}x_{1}}{2+\theta^{(t)}}+x_{4})log\theta + (x_{2}+x_{3})log(1-\theta)$$

其中$$x_{12}|_{x,\theta^{(t)}}\sim Binomial(x_{1},\frac{\theta^{(t)}}{2+\theta^{(t)}})$$

$$x_{12}^{(t)}=E_y[x_{12}|x,\theta^{(t)}]=\frac{\theta^{(t)}x_{1}}{2+\theta^{(t)}}$$

-   M 步驟

對Q函數進行微分

給定$(x_{11},x_{12},x_{3},x_{4},x_{5})$

$$\theta^{(t+1)}=\frac{x_{12}^{(t)}+x_{4}}{x_{12}^{(t)}+x_{2}+x_{3}+x_{4}}$$

**重複以上步驟到參數迭代至穩定**

## R 實作

```r
mult = function(theta, x, n){
    tmp = theta
    for(i in 1:n){
        # E-step
        x12 = x[1]*(theta/ (2 + theta))
        # M-step
        theta = (x12 + x[4])/(x12 + x[2] + x[3] + x[4])

        tmp = c(tmp, theta)
    }
}
x=c(125, 18, 20, 34)
mult(0.1, x, 10)
```

## 範例2

## 範例3

假設現在有兩枚硬幣A、B

-   我們用一枚公正的硬幣來決定，投擲 A 或 B 硬幣
    
-   依據結果，投擲 A 或 B 硬幣 1次，記錄其結果
    
-   反覆進行n次，最終可得到類似如下結果: 10111011….
    
    -   1表示正面，0表示反面

如果我們今天只能觀察到最終結果，無法知道每一次投擲來自哪一枚硬幣，該如何估計出兩個硬幣出現正面機率?

:

Observed Data : $X=(x_1,x_2,…,x_n), x_i:正面出現次數$  
A、B 出現正面機率 : $\theta =(p,q)$

$1^{\circ}$ 從MLE想法出發

概似函數 :  
$$L(\theta|X)=P(X|\theta)=\prod_{i=1}^nP(x_i|\theta)$$

$$\hat p=\frac{使用A硬幣骰到正面次數}{使用A硬幣總投擲次數}$$

$$\hat q=\frac{使用B硬幣骰到正面次數}{使用B硬幣總投擲次數}$$

但因為我們並不知道 $x_i$來自哪個硬幣(機率模型)，所以無法進行計算。

$2^{\circ}$ 嘗試添加隱藏變數，使其變成complete data，運用EM演算法

-   根據observed data，我們無從得知 $x_i$來自哪個硬幣(機率模型)，
    
-   因此我們添加一個隱藏變數 $y_i$，其表示 $x_i$ 來自哪個硬幣，$Y=(y_1,y_2,…,y_n)$
    

$y_i = 1$ or $2$，$x_i|y_{i}=1 \sim Ber(p_{1})$，$x_i|y_{i}=2 \sim Ber(p_{2})$

E-step :

$$\Rightarrow Q(\theta|\theta^{(t)})=E_y[ln(p(x,y|\theta))|x,\theta ^{(t)}]=E_y[\sum_{i=1}^{n}ln(p(y_i|\theta)p(x_i|y_i,\theta))|x,\theta^{(t)}]$$

$$=\sum_{i=1}^{n}E_y[ln(p(y_i|\theta)p(x_i|y_i,\theta))|x,\theta^{(t)}]=\sum_{i=1}^{n}\sum_{y_i=0}^{1}[ln(p(y_i|\theta)p(x_i|y_i,\theta))p(y_i|x_i,\theta^{(t)} )]$$

$$=\sum_{i=1}^{n}\sum_{j=0}^{1}[ln(p(y_i=j|\theta)p(x_i|y_i,\theta))p(y_i=j|x_i,\theta^{(t)} )]$$

其中$p(y_i=j|x_i,\theta^{(t)} )$ : 在第t次迭代下，當前數據來自哪個硬幣的機率

Q-step :

<1>

$$\frac{\partial Q}{\partial p}=\frac{\partial (\sum_{i=1}^{n}ln(\frac{1}{2}p^{x_i}(1-p)^{1-x_i})p(y_i=1|x_i,\theta^{(t)} )}{\partial p}$$

$$=\frac{\partial (\sum_{i=1}^{n}ln(\frac{1}{2})+x_iln(p)+(1-x_i)ln(1-p)p(y_i=1|x_i,\theta^{(t)} )}{\partial p}$$

$$=\sum_{i=1}^{n}(\frac{xi}{p}-\frac{(1-x_i)}{1- p})p(y_i=1|x_i,\theta^{(t)} )=0$$

$$\Rightarrow p^{(t+1)}=\frac{\sum_{i=1}^{n}x_ip(y_i=1|x_i,\theta^{(t)})}{\sum_{i=1}^{n}p(y_i=1|x_i,\theta^{(t)})}$$

<2>

$$\frac{\partial Q}{\partial q}=0$$

同理可得,$$q^{(t+1)}=\frac{\sum_{i=1}^{n}x_ip(y_i=2|x_i,\theta^{(t)})}{\sum_{i=1}^{n}p(y_i=2|x_i,\theta^{(t)})}$$

$3^{\circ}$ 綜觀以上結果，可以發現實際上我們只需要計算出$p(y_i=j|x_i,\theta^{(t)} )$，就可以拿來進行EM迭代。

$\Rightarrow$ 給定初始值$(p^{(0)},q^{(0)})$，計算出$p(y_i=j|x_i,\theta^{(0)} )$，代入更新參數$p^{(t+1)},q^{(t+1)}$，重複迭代，直到收斂或者達到自行給定tolerance內.

$4^{\circ}$ 若改成依據結果，連續投擲 A 或 B 硬幣 10次，記錄其結果

-   反覆進行n次，最終可得到類似如下結果:
    
    -   1表示正面，0表示反面
    

![](https://i.imgur.com/TIuGBly.png)

最終Q-step 的參數公式 :  
$$p^{(t+1)}=\frac{\sum_{i=1}^{n}x_ip(y_i=1|x_i,\theta^{(t)})}{\sum_{i=1}^{n}10p(y_i=1|x_i,\theta^{(t)}}$$

$$q^{(t+1)}=\frac{\sum_{i=1}^{n}x_ip(y_i=2|x_i,\theta^{(t)})}{\sum_{i=1}^{n}10p(y_i=2|x_i,\theta^{(t)})}$$

## Python 實作

```python
import numpy as np
import pandas as pd
from scipy import stats

# 5組硬幣投擲結果(n=5,k=10)，1代表正面，0代表反面
observations = np.array([[1, 0, 0, 0, 1, 1, 0, 1, 0, 1],
                         [1, 1, 1, 1, 0, 1, 1, 1, 1, 1],
                         [1, 0, 1, 1, 1, 1, 1, 0, 1, 1],
                         [1, 0, 1, 0, 0, 0, 1, 1, 0, 0],
                         [0, 1, 1, 1, 0, 1, 1, 1, 0, 1]])
da=pd.DataFrame(observations,
                index=["第一次","第二次","第三次","第四次","第五次"])
da.columns = [1,2,3,4,5,6,7,8,9,10];da

###
def em_single(priors,observations):

    """
    EM算法-單次疊代
    ------------
    priors:[theta_A,theta_B]
    observation:[m X n matrix]

    Returns
    ---------------
    new_priors:[new_theta_A,new_theta_B]
    :param priors:
    :param observations:
    :return:
    """
    counts = {'A': {'H': 0, 'T': 0}, 'B': {'H': 0, 'T': 0}}
    theta_A = priors[0]
    theta_B = priors[1]
    #E step
    for observation in observations:
        len_observation = len(observation)      #計算投擲次數
        num_heads = observation.sum()           #正面次數
        num_tails = len_observation-num_heads   #反面次數
        
        #二項分配公式求解
        contribution_A = scipy.stats.binom.pmf(num_heads,len_observation,theta_A)    #Bin(x,n,p)
        contribution_B = scipy.stats.binom.pmf(num_heads,len_observation,theta_B)
        
        #計算在給定資料、當前參數下，資料來自哪個硬幣的機率
        weight_A = contribution_A / (contribution_A + contribution_B)     # p(y=1|x,theta)
        weight_B = contribution_B / (contribution_A + contribution_B)     # p(y=0|x,theta)
        
        #更新在當前參數下A，B硬幣產生的正反面次數
        counts['A']['H'] += weight_A * num_heads  # num += 1  => num = num+1， sum p(y_i=1|x,theta)*x_i
        counts['A']['T'] += weight_A * num_tails
        counts['B']['H'] += weight_B * num_heads
        counts['B']['T'] += weight_B * num_tails

    # M step
    new_theta_A = counts['A']['H'] / (counts['A']['H'] + counts['A']['T'])  #sum p(y_i=1|x,theta)*x_i / sum 10*p(y_i=1|x,theta)
    new_theta_B = counts['B']['H'] / (counts['B']['H'] + counts['B']['T'])  #sum p(y_i=0|x,theta)*x_i / sum 10*p(y_i=1|x,theta)
    return [new_theta_A,new_theta_B]
    
###
def em(observations,prior,tol = 1e-6,iterations=10000):
    """
    EM算法
    ：param observations :觀測數據
    ：param prior：模型初始值
    ：param tol：迭代结束阈值
    ：param iterations：最大迭代次數
    ：return：局部最佳的模型參數
    """
    iteration = 0;
    while iteration < iterations:
        new_prior = em_single(prior,observations)
        delta_change = np.abs(prior[0]-new_prior[0])
        if delta_change < tol:
            break
        else:
            prior = new_prior
            iteration +=1
    return new_prior,iteration
print ("(p,q,iteration)=",em(observations,[0.7,0.5]))
```

Ans : (p,q,iteration)= ([0.79678865844706648, 0.51958340803243785], 12)
