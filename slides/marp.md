---
marp: true
theme: uncover
class:
    - lead
paginate: true
_paginate: false
---

# 病毒传播里的简单数学模型

---

# 显而易见
- `常识1`: 病毒携带者人数越多，感染的速率就越快。
- `常识2`: 易感人群的人口基数越大，单个病毒携带者的感染能力越强。
- `常识3`: 由于人类自身免疫力，医学的进步和科学的治疗，被感染的人中总有一定比例会被治愈。

---
![bg 80%](./assets/SIR.svg)

---
![h:150px ](./assets/IR.svg)

- `常识3`:每天都有一部分感染人群$I$以一个恒定的比例$\gamma$转变为康复人群$R$。


---
$\dot{R}=\gamma I$

- $I$: 感染人群数量
- $\gamma$: 康复率($\gamma>=0$) recovery rate
- $R$: 康复人群数量
- $\dot{R}$: 康复人群数量增长率

---
![h:150px ](./assets/SI.svg)

- `常识1`: 病毒携带者数量（感染人群）越大，感染的速度就越快 $\dot{S}\propto I$
- `常识2`: 易感人群数量越大，单个病毒携带者能感染的速度就越快 $\dot{S}\propto S$

---
$\dot{S}=-\beta SI$

- $I$: 感染人群数量
- $\beta$: 传染率($\beta>=0$) infection/transmission rate
- $S$: 易感人群数量
- $\dot{S}$: 易感人群数量下降率
- 负号: 易感人群数量是`减少`的

---
![h:150px ](./assets/SIRm.svg)
- 前面已知易感人群的下降率$\dot{S}$，又已知康复人群的增长率$\dot{R}$，那么`感染人群`的变化率$\dot{I}$则为这二者之和。

---
$\dot{I}= \beta SI - \gamma I = (\beta S - \gamma)I$

- $I$: 感染人群数量
- $\beta$: 传染率
- $\gamma$: 康复率
- $S$: 易感人群数量
- $R$: 康复人群数量

---
# 经典 SIR 模型
$\dot{S}=-\beta SI$
$\dot{I}= \beta SI - \gamma I$
$\dot{R}=\gamma I$

- [Kermack-McKendrick Theory 1927](https://en.wikipedia.org/wiki/Kermack%E2%80%93McKendrick_theory)
- [Sir Ronald Ross 1902 诺贝尔生理学或医学奖](https://en.wikipedia.org/wiki/Ronald_Ross)
- 被用于Ebola，疟疾，HIV，流感等传染病动力学的建模。
- 易于扩展

---
`非常识1`: 随着时间推移，感染人群$I$一定会朝着消减的方向发展，最终感染人群数量$I(\infty)$一定为0。

---
反证法：若$I(\infty)>0$，根据$\dot{R}=\gamma I$, 在$t=\infty$时我们有$\dot{R}>0$，那么康复人群数量会接近$+\infty$，这明显与事实相违背。

---
`非常识2`: 疫情拐点会出现在$S=\frac{\beta}{\gamma}$处，通过该点后感染人数$I$就会下降

---
$\dot{I}= (\beta S - \gamma)I$

---
令$\dot{I}=0$，则有$(\beta S - \gamma)I = 0$。
得到
$I=0$或$\beta S - \gamma=0$

---
#### 政策解读
- 降低$\beta$: 隔离，洗手，戴口罩。
- 增大$\gamma$: 抗病毒药物研制，建医院，增加医护人员。
- 降低$S(0)$: 打疫苗。

---
#### 结论2: 病毒一定不会将所有易感人群都感染。

将等式1除以等式3，并对两侧积分我们可以得到:
$S(t) = S(0)exp(-\beta(R(t)-R(0))/\gamma)$

而$R(t)-R(0)\leq N$，得到：
$S(t)\geq S(0)exp(-\beta N/\gamma)$。

---







---
通过这波操作，我们可以看到，随着易感人数的下降，被感染的速率也会下降，当$S(t)$低于$\gamma/\beta$时，人群康复的速率就会大于被感染的速率。进而，最终疫情就会由于缺少新的感染人群，而不是缺少易感人群而结束。




---
- 感染人数一定存在极值点，并且可以确定极值点大小。
- 何时才能停止。

---
# 数学模型的意义
- 通过将这三个显而易见的规律联立组合，可用数学的方法严格分析出下面一些很难显而易见的结论。
- 可以用科学的方式解释公共卫生政策的实际意义。







