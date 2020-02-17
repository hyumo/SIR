Slides, code and scripts used for this introductory [video](https://youtu.be/UBbgcmnelLw) on the SIR epidemic model. 

## Modelica

```Modelica
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
