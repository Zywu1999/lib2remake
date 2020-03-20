# logistic回归

假设：$h_\theta(x)=g(\theta^Tx)$
$z=\theta^Tx$  
$g(z)=\displaystyle\frac{1}{1+e^{-x}}$
$h_\theta(x)=\displaystyle\frac{1}{1+e^{-\theta^Tx}}$
$g(z)$的图像如下图所示
![Logistic_function](https://i.loli.net/2019/12/23/5DpqVJz6xiO2IPm.png)
$h_\theta(x)$的现实意义——显示了在x的取值下y=1的概率
$h_\theta(x)=P(y=1|x;\theta)=1-P(y=0|x;\theta)$

## 决策边界（Decision Boundary）

一般来说若假设的输出${\displaystyle h_\theta(x)\geq 0.5\rightarrow y=1\choose {\displaystyle h_\theta(x)\leq 0.5\rightarrow y=0}}\Rightarrow {\displaystyle \theta^Tx\geq 0\rightarrow y=1\choose {\displaystyle \theta^Tx\leq 0\rightarrow y=0}}$
$\theta^Tx=0$即样本的决策边界
*The decision boundary is the line that separates the area where y = 0 and where y = 1. It is created by our hypothesis function.*

## 代价函数（cost function）

$J(\theta)=\displaystyle{\frac{1}{m}\sum^m_{i=1}Cost(h_\theta(x^{(i)}),y^{(i)})}$
$Cost(h_\theta(x^{(i)}),y^{(i)})=-log(h_\theta(x))\quad if\quad y=1$
![Logistic_regression_cost_function_negative_class.png](https://i.loli.net/2019/12/23/ZHMVWQlwpTzvtnN.png)

$Cost(h_\theta(x^{(i)}),y^{(i)})=-log(1-h_\theta(x))\quad if\quad y=0$

![Logistic_regression_cost_function_positive_class.png](https://i.loli.net/2019/12/23/V6uRGWHji7QBTpX.png)

why use it?(与最大似然法有关)

### 简化

$Cost(h_\theta(x),y)=-ylog(h_\theta(x))-(1-y)log(1-h_\theta(x))$
$Cost\,function:J(\theta)=\displaystyle{\frac{1}{m}\sum^m_{i=1}[-y^{(i)}log(h_\theta(x^{(i)}))-(1-y^{(i)})log(1-h_\theta(x^{(i)}))]}$
*向量化表示*
$ h = g(X\theta)\newline  J(\theta) = \frac{1}{m} \cdot \left(-y^{T}\log(h)-(1-y)^{T}\log(1-h)\right) $

## 梯度下降

$ Repeat \; \lbrace \newline  \; \theta_j := \theta_j - \alpha \dfrac{\partial}{\partial \theta_j}J(\theta) \newline  \rbrace$

*计算偏导数*
$\displaystyle{ Repeat \; \lbrace \newline  \; \theta_j := \theta_j - \frac{\alpha}{m} \sum_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)}) x_j^{(i)} \newline  \rbrace }$
*向量化*
$\displaystyle{\theta:=\theta-\frac{\alpha}{m}X^T(g(X\theta)-\vec y)}$

## 多分类的logistic回归

$ y \in \lbrace0, 1 ... n\rbrace \newline h_\theta^{(0)}(x) = P(y = 0 | x ; \theta) \newline h_\theta^{(1)}(x) = P(y = 1 | x ; \theta) \newline \cdots \newline h_\theta^{(n)}(x) = P(y = n | x ; \theta) \newline \mathrm{prediction} = \max_i( h_\theta ^{(i)}(x) )\newline$

> 额外的笔记：很多更高级的算法比梯度下降法运行速度更快，并不用了解细节，会使用即可。如octave里的fminunc()函数。
```octave/matlab
function [jVal, gradient] = costFunction(theta)
  jVal = [...code to compute J(theta)...];
  gradient = [...code to compute derivative of J(theta)...];
end
options = optimset('GradObj', 'on', 'MaxIter', 100);
initialTheta = zeros(2,1);
   [optTheta, functionVal, exitFlag] = fminunc(@costFunction, initialTheta, options);