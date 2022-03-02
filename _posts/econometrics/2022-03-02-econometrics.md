---
layout: single
title: "Panel Data"
categories: econometrics
toc: true
---

# 1. What is Panel Data?

![Difference Between Time Series and Panel Data | Compare the Difference  Between Similar Terms](../../assets/images/2022-03-02-econometrics/Difference-Between-Time-Series-and-Panel-Data-Tabular-Form.jpg)

Time Series(시계열 데이터)란 단일 객체(one individual)에 대한 일정 기간 동안의 attributes를 

Panel Data는 동일 관찰을 통해 얻어지는 복수개의 객체에 대한 Time Series의 집합이라고 할 수 있을 것이다.



### Difference between Cross-Sectional Data

distinguishing feature relative to cross-sectional (횡단면 데이터) is the presence of multiple observations for each invidual





# 2. Pooled Regression

The simplest model in panel regression

- E(e|x)=0 ; mean independent (strict independence) -> unbiasness & variance become homoskedastic, 
- 실제로는 robust 하지 않을 가능성이 다수 -> Cluster-robust covariance estimator


$$
Y_i=X_i*beta+e_i
$$

$$
E(e_i|X_i)=0
$$

then
$$
\beta =( \Sigma X'X)^-1 (\Sigma X'X)\beta + ( \Sigma X'X)^-1 (\Sigma X'e)
$$

$$
E(\beta|X) =\beta + (\Sigma X'X)^{-1} (\Sigma X' E(e_i|X_i)) = \beta  ;  unbiased
$$

$$
Var(\beta | X)=Var(\Sigma (X'X)^{{-1}}(\Sigma X'e)|X)
$$

$$
since\quad Var(Ae)=A*Var(e)*A'
$$

$$
Var((\Sigma X'X)^{-1}(\Sigma X'e)|X) = (\Sigma X'X)^{-1}[\Sigma X'Var(e|X)X](\Sigma X'X)^{{-1}}
$$

if
$$
Var(e|X)=\sigma^2_e*I_T,\quad it\, is\, homoskedastic\\
Var(\beta_p|X)=(\Sigma X'X)^-1(\Sigma X' I_T X)\sigma^2(\Sigma X'X)^-1\\
=\sigma^2(\Sigma X'X)^-1\; ;classical \; (default\,at\,Stata)
$$

$$
V_h=(\Sigma X'X)^-1(\Sigma X'ee'X)(\Sigma X'X)^-1
$$



# One-Way Error Component Model

패널데이터를 pooled regression하는건 메시가 동네축구 하는것(?)

e_it에 대해서 error-component structure를 사용
$$
y_{it}=X_{it}'\beta+e_{it}\\
e_{it}=u_i+\epsilon_{it}
$$
where u is individual-specific effect

and epsilon are idiosyncratic errors
$$
Vector\, Notation)\quad
e_i=1_Tu_i+\epsilon_i
$$
then 
$$
y_{it}=X_{it}'\beta+e_{it}\\
Y_{it}=X_{it}'\beta+u_i+\epsilon_{it}\\
Y_i=X_i\beta+1_Tu_i+\epsilon_i
$$
