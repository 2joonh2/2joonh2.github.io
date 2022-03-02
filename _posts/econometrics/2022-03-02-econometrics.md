---
layout: single
title: "Panel Data"
categories: econometrics
toc: true
use_math:true
---

# 1. What is Panel Data?



![Difference Between Time Series and Panel Data](../../assets/images/2022-03-02-econometrics/Difference-Between-Time-Series-and-Panel-Data-Tabular-Form.jpg)

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
\beta_{pool}=( \Sigma X'X)^-1 (\Sigma X'X)\beta + ( \Sigma X'X)^-1 (\Sigma X'e)
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



# 3. One-Way Error Component Model

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

### Random Effect

one-way component structure w/ random effect : random effects regression model
$$
Y_i=X_i\beta+e_i=X_i\beta+1_Tu_i+\epsilon_i\\
E(e_i|X_i)=0,\;Var(e_i|X_i)=1_t1_t'\sigma_u^2+I_t^2\sigma^2_\epsilon=\Omega\\
\beta_{GLS}=(\Sigma X'\Omega^{-1}X)^{-1}(\Sigma X'\Omega^{-1}y)=(\Sigma X'\Omega^{-1}X)^{-1}(\Sigma X'\Omega^{-1}(X\beta+e)))\\
\beta+(\Sigma X'\Omega^{-1}X)^{-1}(\Sigma X'\Omega^{-1}e)
$$

$$
E(\beta_{GLS}|X)=\beta+E((\Sigma X'\Omega^{-1}X)^{-1}(\Sigma X'\Omega^{-1}e)|X)\\
=\beta+(\Sigma X'\Omega^{-1}X)^{-1}(\Sigma X'\Omega^{-1}E(e|X))\\
=\beta\; ; unbiased
$$

$$
Var(\beta_{GLS}|X)=(\Sigma X'\Omega^{-1}X)^{-1}(\Sigma X'\Omega^{-1}\Omega \Omega^{-1}X)(\Sigma X'\Omega^{-1}X)^{-1}\\
=(\Sigma X'\Omega^{-1}X)^{-1}
$$

$$
Var(\beta_{pool}|X)=(\Sigma X'X)^{-1}(\Sigma X'Var(e|X)X)(\Sigma X'X)^{-1}\\
=(\Sigma X'X)^{-1}(\Sigma X'\Omega X)(\Sigma X'X)^{-1}
$$

$$
V_{GLS}\leq V_{pool}
$$




$$
if\quad \sigma_u^2=0,\,\quad \Omega=\sigma_\epsilon^2I_T\\
then,\quad V_{GLS}=(\Sigma X'\Omega^{-1}X)^{-1}=\sigma^2_\epsilon(\Sigma X'X)^{-1}\\
V_{pool}=(\Sigma X'X)^{-1}(\Sigma X'\Omega X)(\Sigma X'X)^{-1}=(\Sigma X'X)^{-1}\sigma^2
$$

### GLS

given the error structure,

the natural estimator of \beta is GLS
$$
\hat \beta_{GLS}=(\Sigma X'\Omega X)^{-1}\\
\Omega\, is\, consists\, of\,\;\sigma_u,\; \sigma_\epsilon
$$
feasible GLS estimator replace the unknown variance of u and epsilon

When there is no indivudal specific effect (sigma_u=0)

- V_gls=V_pool

- when there is no clear direction; cluster robust variance

```Stata
xtreg depvar indepvars, option
option can be re | fe | vce(robust)
```



### Fixed Effect

assume u_i as time-invariant unobserved missing variable

u is possibly correlated with X_it

ex. 학력과 능력 간의 상관관계 (능력이 높은 사람의 학력이 높은 경향)

-> Endogeneity Problem

let u and X allow to be correlated, u is called **fixed effect** (within estimator)

Correlation between X and u will cause pooled and randome effect estimators to be **biased**. (4)
$$
E[X_{it}\epsilon_{it}]=0
$$
strict mean independence (5)
$$
E[\epsilon_{it}|X_{i}]=0
$$
(4)만해도 충분 (5)는 더 강한 가정



beta가 u에 의존하지 않도록 구분시켜야 함

eliminate u -> within-transformation

**individual specific mean**
$$
Y_i=(1'_T1_T)^{-1} 1'_TY_i=1/T*\Sigma Y_{it}
$$

$$
\dot Y_i=Y_i-1_TY_i\\
=Y_i-1_T(1'_T1_T)^{-1}1'_TY_i\\
=M_TY_i\\\\
M_T\;is\, an\, idempotent\, matrix
$$

as same
$$
\dot X=M_TX_i
$$
then
$$
\dot Y=\dot X\beta+\dot\epsilon\\
\bar u=0
$$
