---
marp: true
theme: uncover
class:
    - lead
paginate: true
_paginate: false
---
# 病毒传播数学模型

---
`数学模型`:用数学语言描述一些具有规律性或常识性的现象

---
# 经典 SIR 模型
$\dot{S}=-\beta SI$
$\dot{I}= \beta SI - \gamma I$
$\dot{R}=\gamma I$

- [Sir Ronald Ross 1902 诺贝尔生理学或医学奖](https://en.wikipedia.org/wiki/Ronald_Ross)
- 被用于Ebola，疟疾，HIV，流感等传染病动力学的建模。
- 易于扩展

---
![bg 80%](./assets/SIR.svg)

---
![h:150px ](./assets/IR.svg)

$\dot{R}=\gamma I$

- 每天都有一部分感染人群$I$以一个恒定的比例$\gamma$转变为康复人群$R$。
- $\gamma$: 康复率($\gamma>=0$) recovery rate
- $\dot{R}$: 康复人群数量增长率

---
![h:150px ](./assets/SI.svg)

$\dot{S}=-\beta SI$

- 病毒携带者数量（感染人群）越大，感染的速度就越快 $\dot{S}\propto I$
- 易感人群数量越大，单个病毒携带者能感染的速度就越快 $\dot{S}\propto S$
- $\beta$: 传染率($\beta>=0$) infection/transmission rate
- 负号: 易感人群数量总是`下降`的

---
![h:150px ](./assets/SIRm.svg)

$\dot{I}= \beta SI - \gamma I = (\beta S - \gamma)I$

- 前面已知易感人群的下降率$\dot{S}$，又已知康复人群的增长率$\dot{R}$，那么`感染人群`的变化率$\dot{I}$则为这二者之和，符号相反。

---
# 仿真

---
```python
model SIR "Susceptible, Infected and Recovered model"
  Real S "易感人群";
  Real I "感染人群";
  Real R "康复人群";
  parameter Real beta(min=0) = 0.7/50000 "感染率";
  parameter Real gamma(min=0) = 0.2 "康复率";
  parameter Integer N(min=0) = 50000 "总人口";
  parameter Integer I0(min=0) = 5 "初始感染人群数量";
protected 
  final parameter Integer R0=0 "初始康复人群数量";
  final parameter Integer S0=N - I0 - R0 "初始易感人群数量";
  final parameter Real Re=S0*beta/gamma "有效繁殖数";
initial equation 
  S = S0;
  I = I0;
  R = R0;
equation 
  der(S) = -beta*S*I "易感人群方程";
  der(I) = beta*S*I - gamma*I "感染人群方程";
  der(R) = gamma*I "康复人群方程";
end SIR;
```

---
![h:550px](./assets/SIRplot.svg)
- $\beta=1.4\times 10^{-5}, \gamma=0.2, R_e=3.5$
- $N=50000,I(0)=1$

---
# 分析

---
`非常识性结论`:
疫情拐点会出现在$S(t)=\frac{\gamma}{\beta}$处
通过该点后感染人数$I$就会下降

---
$\dot{I}= (\beta S - \gamma)I = (\frac{\beta}{\gamma} S - 1)\gamma I$

---
$R_e = S(0)\frac{\beta}{\gamma}$ - 有效繁殖数
- 当$R_e \leq 1$时，$I(t)$会随着时间推移递减至$0$。
- 当$R_e > 1$时，$I(t)$会先增加，并达到其峰值，最后递减至$0$。

---
### 公共卫生政策解读
$R_e = S(0)\frac{\beta}{\gamma}$ - 有效繁殖数
- 降低$\beta$: 隔离，洗手，戴口罩。
- 增大$\gamma$: 抗病毒药物研制，建医院，增加医护人员。
- 降低$S(0)$: 打疫苗。

---
### 其他结论
- 感染人数存在极大值。
- 病毒不会以“清空”所有易感人群$S$的方式结束 $S(\infty)>S(0) e^{−\beta/\gamma}$
- 可以预测疫情大小，疫情结束时间等。
