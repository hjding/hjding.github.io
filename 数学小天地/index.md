# 数学小天地


## 学习对数log有什么用？

1. 简化运算。

   > 乘法变加法:
   > $$
   > \lg a·b=\lg a+\lg b
   > $$
   > 除法变减法:
   > $$
   > \lg \frac{a} {b}=\lg a-\lg b
   > $$
   > 乘方变乘法:
   > $$
   > \lg a^n=n·\lg a
   > $$
   > 开方变除法:
   > $$
   > \lg\sqrt [n] {a}=\frac {\lg{a}}{n}
   > $$
   >


2. 可以知道你把钱存银行什么时候能当上世界首富~

   > 例如，你现在手里有1万美元，2021年世界首富杰夫·贝佐斯以1914亿美元，就算天天存银行4%吧。
   >
   > 你现在手里$a_0=10000$，每年的钱都是前一年的1.04倍，n年之后你手里的钱：
   > $$
   > a_n=a_0·b^n
   > $$
   > 两边取个对数：
   > $$
   > \lg a_n=\lg a_0 +n·\lg b
   > $$
   > 稍微整理一下：
   > $$
   > n= \frac{(\lg a_n-\lg a_0)} {\lg b}
   > $$
   > 代入数据：
   > $$
   > n=\frac {\lg 1914,0000,0000-\lg 1,0000}{\lg 1.04}≈427.511118384年
   > $$
   > 

   

## 自然常数e≈2.71828182846…

### 复利

可以用**复利**解释。

> 1. 1块钱，一年付1次利息(利率100%)，一年后2块。
> 2. 一年付2次利息，1/2年(6个月)付1次利息(利率1/2)，一年后，2.25块。
> 3. 一年付3次利息，1/3年(4个月)付1次利息(利率1/3)，一年后2.37元。
> 4. ...
> 5. 一年付n次利息，1/n年付一次利息(利率1/n)，一年后(1+1/n)^n。
> 6. 当n趋向于无穷大时，一年后的钞票不会无限变多，有个极限值e！
>

| n        | (1+1/n)^n |
| -------- | --------- |
| 1        | 2         |
| 2        | 2.25      |
| 3        | 2.37      |
| 5        | 2.488     |
| 10       | 2.5937    |
| 100      | 2.7048    |
| 1000     | 2.7169    |
| 1,0000   | 2.71814   |
| 10,0000  | 2.718268  |
| 100,0000 | 2.7182804 |
| …        |           |

### 细胞分裂  

类似的，也可以用**细胞分裂**解释。

## 1和0.9的循环哪个大？

> $$
> ∵ 1 = \frac{1}{3}+\frac{2}{3}
> $$
>
> 
> $$
> 又∵0.999\cdots = 0.333\cdots+0.666\cdots
> $$
>
> $$
> ∴ 1=0.999\cdots！！！
> $$
>
> 

## 神奇的6174

任意的4个数字，组成的**最大四位数**减**最小四位数**，循环下去，最后都是6174！

> $$
> 9876－6789＝3087
> $$
>
> $$
> 8730－378＝8352
> $$
>
> $$
> 8532－2358＝6174
> $$
>
> $$
> 7641－1467＝6174
> $$
>
> $$
> \cdots
> $$
>
>
> 

## 素数(质数)的作用:RSA密码原理

> RSA密码，这种密码可靠性的基础是目前人们对于**素因子分解**的困难性。简单的说，将两个大素数相乘十分容易，但是想要对其乘积进行因式分解却极其困难。

## 斐波拉契数列

### 简介

第1、2项都为1，从第三项开始，后一项等于前面2项之和。
$$
F_1=1,F_2=1,F_{n}=F_{n-1}+F_{n-2} (n\geq3)
$$
1,1,2,3,5,8,13,21,34,55,89,134，…

### 自然现象

#### 向日葵花瓣

它依两个方向螺旋形排列，朝一个螺旋方向生长的花瓣数同朝向相反螺旋方向生长的花瓣数，几乎总等于斐波拉契数列中两个相邻的数。

#### 松树松果

果鳞的排列呈螺旋状，各螺旋线上果鳞的数目，构成斐波拉契数列。

#### 花瓣

一些花的花瓣构成斐波拉契数列中的一串数字：

1. 百合花，3个花瓣
2. 梅花，5个花瓣
3. 飞燕草，8个花瓣
4. 万寿菊，13个花瓣
5. 紫苑，21个花瓣
6. ……

#### 数木的分支

1. 主干，1个分支
2. 上面第2的枝干，2个分支
3. 上面第3的枝干，3个分支
4. 上面第4枝干，5个分支
5. 上面第5枝干，8个分支
6. 上面第6枝干，13个分支
7. ……

### 黄金分割

#### 黄金分割比怎么来的？

> 黄金分割比是把一条线段分割为两部分，使其中一部分与全长之比等于另一部分与这部分之比。

> 例如，一条线段，切割成两段，较短的一段(记为a)与较长的一段(记为b)的比值等于b与总体的比值。
>
> 设这条线段为1，b=x，则a=1-x
>
> 得：
> $$
> \frac {1-x}{x}=\frac{x}{1}
> $$
> 解得：
> $$
> x=\frac {\sqrt{5} -1}{2}(负值舍去)≈0.61803398875
> $$

#### 斐波拉契数列与黄金分割

前一项与后一项的比值$\frac {F_{n}} {F_{n+1}}$：
$$
\frac {F1}{F2}=\frac {1}{1} =1; \frac {F2}{F3}=\frac {1}{2} =0.5
$$

$$
\frac {F3}{F4}=\frac {2}{3} =0.666\cdots; \frac {F4}{F5}=\frac {3}{5} =0.6
$$

$$
\frac {F5}{F6}=\frac {5}{8} =0.625; \frac {F6}{F7}=\frac {8}{13} =0.615
$$

**相邻两数的比值**交替地大于或小于黄金比($\frac {\sqrt{5} - 1}{2}$)，并且该比值无限趋近于黄金比。



## 何为函数?

> 函，同"含"，意为包含，含有。
> 凡此变数中函彼变数者，则此为彼之函数”，也即函数指一个量随着另一个量的变化而变化，或者说一个量中包含另一个量。

## 莫比乌斯带

> 莫比乌斯带由德国数学家莫比乌斯（Mobius，1790～1868）和约翰·李斯丁于1858年发现。就是把一根纸条扭转180°后，两头再粘接起来做成的纸带圈，具有魔术般的性质。比如，一只蚂蚁可以从纸带的一个表面不跨越式的爬到另一个表面。

## 什么是数学？

> 数学是符号加逻辑。——罗素
>
> 在数学中，我们发现真理的主要工具是归纳和模拟。—— 拉普拉斯
>
> 数学中的一些美丽定理具有这样的特性：它们极易从事实中归纳出来，但证明却隐藏的极深。——高斯
>
> 当我听别人讲解某些数学问题时，常觉得很难理解，甚至不可能理解。这时便想，是否可以将问题化简些呢﹖往往，在终于弄清楚之后，实际上，它只是一个更简单的问题。——希尔伯特

### 抽象

抽象是一个孤立的过程，是思考着逐渐将信息降维，以保留最普遍信息的一个过程。

### 逻辑

逻辑则是建立不同事物之间关系的过程，但并不涉及到信息的减少。

### 抽象和逻辑的关系

一个是简化信息，一个建立信息之间的联系。这两者实际上代表着数学学习过程中的两个不同过程，然而在实际的数学学习过程中，它们并不是明显可分的。

> 比如，孩子想要学习勾股定理并应用在梯子放在墙边的问题里，需要将这个实际问题抽象为基本的三角形问题，然后根据演绎推理：直角三角形满足勾股定理，梯子斜放墙边可以抽象为直角三角形，因此，可以用勾股定理求解。

所以，不要将两者孤立开来，它们同等重要。缺乏抽象思维，则面临信息过多而被淹没，缺乏逻辑，则难以建立问题与求解的关系。一边简化信息，一边建立问题与解的关系，才是最根本也是最重要的做法。而作为教育者，教会孩子如何看到这些东西，可能会比教会他怎么做题更有意义一些。

## 数学题目的提问清单 

想学好数学，当别人眼中的学霸，乃至学神，需要常常问自己这些问题：

1. 这道题目考察的是什么知识点？
2. 这道题目有什么特点？哪些条件是关键条件？
3. 这道题目是如何运用书中的定理/定义的？这些知识点有什么变形方式？
4. 这个类型题都有什么解法？
5. 这道题目除了答案给出的解法，是否可以用别的解法？
6. 哪种解法更适用，为什么？

## 数学中最重要的能力

1. 理解能力。知其然，更要知其所以然。
2. 概括能力。知识之间的联系，知识网络。
3. 发现问题，解决问题的能力。
4. 独立思考，深入研究的能力。
