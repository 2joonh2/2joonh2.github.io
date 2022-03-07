---
layout: single
title: "[Econometrics] 2. Fixed Effect"
categories: Econometrics
toc: true
toc_sticky: true
---

응용계량경제학 필기노트

![image-20220307170244209](../../assets/images/2022-03-07-econometrics_2/image-20220307170244209.png)

웃으면 복이 와요.  ~~복이 와서 웃는거 아닌가요.~~



# Fixed Effect

$u_i$ as time-invariant(시간 불변) unobserved missing variable

$u$는 높은 확률로 $X_{it}$와 correlate 되어있을 것이다. 

ex. 학력과 능력 간의 상관관계 (능력이 높은 사람의 학력이 높은 경향)

그렇다면 u와 X의 상관관계로 인한 Endogeneity Problem이 발생한다.

Correlation between X and u는 pooled와 random effect estimators 모두 편향성을 갖게하는데,

이 때의 u를 **fixed effect** 라고 정의한다. 

아래 사진을 통해 예시와 함께 설명해보자.

<img src="../../assets/images/2022-03-02-econometrics/image-20220302195304570.png" alt="heterogeneity bias" style="zoom:67%;" />

Image Reference: [Introduction Describe what panel data is and the (slidetodoc.com)](https://slidetodoc.com/introduction-describe-what-panel-data-is-and-the/)



Firm 1부터 4까지의 전체 데이터를 가지고 단일 OLS, 즉 Pooled Regression을 진행하게 되면 점선과 같은 Estimator와 수식을 얻을 것이다.

하지만 각 Firm 별로 실제 적용되는 붉은 선 상으로 표현된 Estimator의 기울기는 Pooled Estimator보다 작은 것을 알 수 있다.

이는 개별 회사들에 대한 u; fixed effect가 존재하기 때문이며 이를 감안하는 모델을 구하기 위한 작업이 필요할 것이다.



본 과정에선 아래의 두개의 가정 조건 중 (아래의 strict mean indep. 조건이 위의 조건보다 강한 조건) 위의 **strict exogenous** 조건만이라도 만족한다고 가정한다.


$$
\displaylines{E[X_{it}\epsilon_{it}]=0\newline
E[\epsilon_{it}|X_{i}]=0}
$$



$\beta$가 u에 의존하지 않도록 구분시켜 예시와 같은 붉은선의 estimator를 구하기 위한 작업이 필요하며, 작업의 옵션 중 하나는 아예 u를 제거하는 것이다.

대표적인 이 과정은 **within-transformation** 라고 한다.



## A) Within-Transformation

### Individual Specific Mean & Demeaned Values


$$
\bar Y_i=(1'_T1_T)^{-1} 1'_TY_i=1/T*\Sigma Y_{it}
$$



Observations들의 평균인 **Individual Specific Mean**을 뺀 차이를 **Demeaned Values / Deviations from individual means**라고 부른다.


$$
\displaylines{\dot Y_i=Y_i-1_T\bar Y_i\newline
=Y_i-1_T(1'_T1_T)^{-1}1'_TY_i\newline
=M_TY_i\newline\newline
M_T\;is\, an\, idempotent\, matrix}
$$



동일하게 X에 대해서도 유도할 수 있다.



$$
\dot X=M_TX_i
$$



그렇다면 X와 Y의 Demeaned Values를 가지고 Model를 생성하면, u가 사라지는 것을 확인할 수 있을 것이다.



$$
\displaylines{from \quad Y_i=X_i\beta+1_Tu_i+\epsilon_i\newline
\dot Y=\dot X\beta+\dot\epsilon\newline
Since \quad M_T1_T=0}
$$



Individual Speicific mean은 곧, Individual마다 Intercept (ex. $\beta_0$)가 따로 있다는 뜻이다.



### Derivation of Fixed Effect Estimator


$$
\displaylines{\dot Y_i=\dot X_i\beta+\dot\epsilon_i\newline
after\;OLS,\quad \hat\beta_{fe}=(\Sigma \dot X'\dot X)^{-1}(\Sigma \dot X'\dot y)=(\Sigma X'M_T'M_TX)^{-1}(\Sigma X'M_T'M_Ty)\newline
= (\Sigma X'M_TX)^{-1}(\Sigma X'M_Ty)\quad (M\; is\; idempotent \, and \, symmetric)\newline
=\beta+0+ (\Sigma X'M_TX)^{-1}(\Sigma X'M_T\epsilon)}
$$

$$
\displaylines{E(\hat\beta_{fe}|X)=\beta+(\Sigma X'M_TX)^{-1}(\Sigma X'M_TE(\epsilon|X))=0\quad\newline
with\;assumption\;of\;strict\;mean\;indep.}
$$

$$
let\;E(\epsilon_i'\epsilon_i|X_i)=\Sigma_i
$$

$$
\displaylines{Var(\hat\beta_{fe}|X)=(\Sigma X'M_TX)^{-1}(\Sigma X'M_T\Sigma M_TX)(\Sigma X'M_TX)^{-1}\newline
=(\Sigma \dot X'\dot X)^{-1}(\Sigma \dot X'\Sigma \dot X)(\Sigma \dot X'\dot X)^{-1}\newline\newline
if\quad \Sigma=\sigma_\epsilon^2I_T\;(homoskedastic),\quad V_{fe}^0=\sigma_\epsilon^2(\Sigma \dot X'\dot X)^{-1}\newline
V_{fe}^0>= V_{pool}}
$$

Robust, but low efficiency



## B) Differenced Estimator



$$
\displaylines{\Delta Y_{it}=Y_{it}-Y_{it-1} \quad for\;t=2,...,T\newline
then,\quad \hat\beta_\Delta=(\Sigma \Delta X'\Delta X)^{-1}(\Sigma \Delta X'\Delta y)\newline\newline
we\;can\;find\;out\;for\;T=2,\quad \hat\beta_{fe}=\hat\beta_\Delta}
$$


On can show that the differenced estimator is less efficient than within-transformation estimator.



## C) Dummy Variable Regression



$$
\displaylines{Y_{it}=X_{it}'\beta+u_1D_1+u_2D_2+...+u_ND_N+\epsilon_{it}\newline
D_i \;is\; dummy\; variable\;(0\,or\,1)\newline}
$$

$$
\displaylines{by\; FLW\; theorem,\; 1)\; reg\; Y\; on\; D\; ->\; resdiual\; Y\newline
2)\; reg\; X\; on\; D\; ->\; residual\; X\newline
3)\; reg\; residual\; y\; on\; residual\; X\; ->\; \beta}
$$

$$
\displaylines{then\;also\; by\; FLW\; theorem,\; 1)\; reg\; Y\; on\; D\; ->\; resdiual\; \dot Y\newline
2)\; reg\; X\; on\; D\; ->\; residual\; \dot X\newline
3)\; reg\; residual\; y\; on\; residual\; X\; ->\; \beta}
$$

## Cluster-Robust Covariance



allows $\epsilon$ to be heteroskedastic and serially correlated across t is the cluster-robust covariance matrix estimator


$$
\hat V_{fe}^{cluster}=(\dot X'\dot X)^{-1}(\Sigma\dot X'\epsilon'\epsilon\dot X)(\dot X'\dot X)^{-1}
$$



## D) Between Estimator



$$
\displaylines{\bar Y=\bar X'\beta+u+\epsilon\newline
\hat\beta_{be}=(\Sigma\bar X \bar X')^{-1}(\Sigma \bar X \bar Y)\newline
V_{be}=Var(\hat\beta_{be}|X)=(\Sigma\bar X \bar X')^{-1}(\sigma^2_u+\sigma^2_\epsilon/T)
\newline\newline
for \;simple\;understand}
$$




## Hausman Test for Random vs Fixed Effects



Random Effect의 조건(무려 6가지)에 비해 Fixed Effect의 조건은 1가지로 약한편이다.

곧, 이는 Random Effect의 조건이 훨씬 Fixed Effect에 비해 강한 assumption이라고 할 수 있다.




$$
\displaylines{H_0:\;RE \quad \hat\beta_{RE} \simeq \hat\beta_{FE}\newline
H_1:\;FE \quad \hat\beta_{RE}\neq \hat\beta_{FE}\newline
\newline
H=(\hat\beta_{FE}-\hat\beta_{RE})'(\hat V_{FE}-\hat V_{RE})(\hat\beta_{FE}-\hat\beta_{RE})}
$$



Random Effect의 조건 중 강력한 가정은 Strict Mean Independence이다. ~~???:기억하라고~~


$$
E[u|X]=0
$$


Fixed Effect는 위 조건을 굳이 만족시키지 않아도 된다. 하지만 그 조건이 만족된다면 Random Effect가 효과적이면서도 Robustness를 만족할 것이다.



하지만 최근 연구동향은 Robustness를 훨씬 중요하게 생각한다. 따라서 Fixed Effect Estimator를 일차적으로 필수 이용하고, 상황에 따라 Random Effect Estimator를 사용하는 것이 좋겠다.



## Two-Way Error Components


$$
Y_{it}=X_{it}'\beta+v_t+u_i+\epsilon_{it}
$$



v는 시간에 따른 모든 individual에게 영향을 미치는 (ex. 경기동향, 인플레이션, 금리 등) 요소이다.

보통은 u에 대해선 앞선 방법처럼 within-transformation을 통해 indivdual mean을 빼주고, v에 대해선 dummy variable representation을 진행하는 편이다.



## Dynamic Panel Models

지금까지의 모델은 **Static Panel Model**에 해당한다

**Dynamic Panel Model**에선... 말을 말자(?)





## Example 

예를 들어 미국 주별 주세율에 따른 음주운전 사고률 및  사상자수를 분석해보자.



$u_i$ : 각 individual에 Y를 향해 영향을 미치는 확인되지 못한 변수들 (주별 음주문화에 대한 문화 및 규제 등) --> state **fixed effect**

$v_t$: 모든 individual에 대해 영향을 미치는 요소; 차량 안전기능의 발전, 미국 연방 안전규제의 강화 등 --> time **fixed effect**



자세한 실습의 내용은 다음 포스팅으로 기약하자
