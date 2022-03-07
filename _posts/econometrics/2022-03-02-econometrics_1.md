---
layout: single
title: "[Econometrics] 1. Panel Data & Error Component Model"
categories: Econometrics
toc: true
toc_sticky: true
---

응용계량경제학 필기노트

(이것은 차마 교수님(Dr. Yoon)의 지도학생이라 할수도 없는 형편없는 지식을 만회하기 위한 하찮은 노력이었던 것이다)

![image-20220302223536865](../../assets/images/2022-03-02-1_Panel_Data_n_Error_Component_Model/image-20220302223536865.png)



# Panel Data & Error Component Model

## 1. What is Panel Data?



![Difference Between Time Series and Panel Data](../../assets/images/2022-03-02-econometrics/Difference-Between-Time-Series-and-Panel-Data-Tabular-Form.jpg)

Image Reference: [Difference Between Time Series and Panel Data, Compare the Difference Between Similar Terms](https://www.differencebetween.com/difference-between-time-series-and-panel-data/)



Time Series(시계열 데이터)란 단일 객체(one individual)에 대한 일정 기간 동안의 관찰 데이터를 의미한다. 

**Panel Data**는 복수개의 객체에 대한 일정 기간 동안의 관찰 데이터로서, 같은 기간에 대한 Time Series들의 집합이라고 할 수 있을 것이다.



### Difference between Cross-Sectional Data

Distinguishing feature relative to **cross-sectional** (횡단면 데이터) is the presence of **multiple observations for each individual**



## 2. Pooled Regression

패널데이터에 별도 작업 없이 Regression을 실행할 때, 이를 **Pooled Regression**이라고 한다.

Pooled Regression에서도 **Strict Mean Independence**를 가정한다; 이는 Estimator의 Unbiasedness를 만족시키기 위함이다.

(Strict Mean Independence는 Pairwise Mean Independence보다 강한 가정이다.)



$$
\displaylines{Strict\, Mean\, Independence)\quad E(e_{it}|X_{it})=0\newline
Pairwise\, Mean \,Independence) \quad E[X_{it}e_{it}]=0
}
$$




### Derivation of Pooled Regression Estimator



$$
\displaylines{Y_i=X_i*\beta+e_i\newline
E(e_{it}|X_i)=0 \; (strict \, independence)}
$$



$\hat\beta_{pool}$은 일반 OLS estimator의 공식을 사용하여 유도한다.


$$
\displaylines{\hat\beta_{pool}=( \Sigma X'X)^{-1} (\Sigma X'Y)}
$$


Estimator는 Strict Mean Independence를 통해 unbiased 하며 증명은 아래와 같다.




$$
\displaylines{\hat\beta_{pool}=( \Sigma X'X)^{-1} (\Sigma X'X)\beta + ( \Sigma X'X)^{-1} (\Sigma X'e)\newline
E(\hat\beta_{pool}|X) =\beta + (\Sigma X'X)^{-1} (\Sigma X' E(e_i|X_i)) = \beta\;  ;\;unbiased}
$$





Estimator의 Variance는 위와 같이 구할 수 있는데, 아래와 같이 Variance의 Homoskedasticity를 가정한다면, $\sigma^2(\Sigma X'X)^{-1}\$라는 간단한 공식을 유도할 수 있다.




$$
\displaylines{Var(\hat\beta_{pool} | X)=Var(\Sigma (X'X)^{-1}(\Sigma X'e)|X) = (\Sigma X'X)^{-1}[\Sigma X'Var(e|X)X](\Sigma X'X)^{-1}\newline
(since\quad Var(Ae)=A*Var(e)*A')\newline\newline
if\quad Var(e|X)=\sigma^2_e*I_T\;;\quad homoskedastic\newline
Var(\hat\beta_{pool}|X)=(\Sigma X'X)^{-1}(\Sigma X' I_T X)\sigma^2(\Sigma X'X)^{-1}\newline
=\sigma^2(\Sigma X'X)^{-1}\; ;classical \; (default\,at\,Stata)}
$$





하지만 실제 준실험이나, 현장에서는 robust 하지 않을 가능성이 다수일텐데, 이를 보완하기 위해 Cluster-robust covariance estimator를 사용한다.





$$
Cluster-robust\, Covariance\, Matrix\, estimator)\quad\hat V_{pool}=(\Sigma X'X)^{-1}(\Sigma X'ee'X)(\Sigma X'X)^{-1}
$$



## 3. One-Way Error Component Model



> 패널데이터를 pooled regression하는건 메시가 동네축구 하는것(?)

그렇다고 한다. (난 메시도 아닌데)



$e_{it}$에 대해서 **Error Component Structure**를 사용한다.



$$
\displaylines{y_{it}=X_{it}'\beta+e_{it}\newline
e_{it}=u_i+\epsilon_{it}}
$$





where $u$ is individual-specific effect, and $\epsilon$ is idiosyncratic (i.i.d.) errors




$$
\displaylines{Vector\, Notation)\quad
e_i=1_Tu_i+\epsilon_i}
$$





각 notation 별로 아래와 같은 수식들을 생각해볼 수 있다.




$$
\displaylines{y_{it}=X_{it}'\beta+e_{it}\newline
Y_{it}=X_{it}'\beta+u_i+\epsilon_{it}\newline
Y_i=X_i\beta+1_Tu_i+\epsilon_i}
$$



### Random Effect

Random Effect는 앞선 u와 $\epsilon$이 conditionally mean zero, uncorrelated, and homoskedastic 이라 가정하는 것이다.



$$
\displaylines{
<Random\; Effects\; Specification>\newline\newline
E[\epsilon|X]=0\newline
E[\epsilon^2|X]=\sigma_\epsilon^2\newline
E[\epsilon_{it}\epsilon_{ij}|X]=0\newline
E[u|X]=0\newline
E[u^2|X]=\sigma_u^2\newline
E[u\epsilon|X]=0\newline
}
$$



Random Effect를 만족하는 Error Component Structure의 Regression을 **Random Effects Regression Model** 이라고 한다.



### GLS

본 Model에서 일반적인 Estimator는 GLS로부터 구해진 것이다. 아래에서 GLS를 통한 Estimator를 유도해보자.



#### Derivation of $\hat\beta_{GLS}$

​	

$$
\displaylines{Y_i=X_i\beta+e_i=X_i\beta+1_Tu_i+\epsilon_i\newline
E(e_i|X_i)=0\newline
Var(e_i|X_i)=1_t1_t'\sigma_u^2+I_t^2\sigma^2_\epsilon=\Omega\newline\newline

\hat\beta_{GLS}=(\Sigma X'\Omega^{-1}X)^{-1}(\Sigma X'\Omega^{-1}y)=(\Sigma X'\Omega^{-1}X)^{-1}(\Sigma X'\Omega^{-1}(X\beta+e)))\newline
=\beta+(\Sigma X'\Omega^{-1}X)^{-1}(\Sigma X'\Omega^{-1}e)}
$$



Random Effect를 만족하는 상황에서 $ \hat\beta_{GLS}$는 unbiased를 만족한다.

#### Expectation of $\hat\beta_{GLS}$ at Random Effect Assumption



$$
\displaylines{E(\hat\beta_{GLS}|X)=\beta+E((\Sigma X'\Omega^{-1}X)^{-1}(\Sigma X'\Omega^{-1}e)|X)\newline
=\beta+(\Sigma X'\Omega^{-1}X)^{-1}(\Sigma X'\Omega^{-1}E(e|X))\newline
=\beta\; ; unbiased}
$$



Random Effect를 만족하는 상황에서 $ \hat\beta_{GLS}$의 분산은 Homoskedasticity를 통해 아래와 같이 유도된다.

#### Variance of  $\hat\beta_{GLS}$ at Random Effect Assumption



$$
\displaylines{Var(\hat\beta_{GLS}|X)=(\Sigma X'\Omega^{-1}X)^{-1}(\Sigma X'\Omega^{-1}\Omega \Omega^{-1}X)(\Sigma X'\Omega^{-1}X)^{-1}\newline
=(\Sigma X'\Omega^{-1}X)^{-1}}
$$





#### Comparison with a Pooled Estimator



$$
\displaylines{Var(\hat\beta_{pool}|X)=(\Sigma X'X)^{-1}(\Sigma X'Var(e|X)X)(\Sigma X'X)^{-1}\newline
=(\Sigma X'X)^{-1}(\Sigma X'\Omega X)(\Sigma X'X)^{-1}}
$$




$$
V_{GLS}\leq V_{pool}
$$



위 부등식의 증명은 숙제란다.

Error Term에서 u의 분산이 0이고, 이로 인해 $\Omega$가 $\epsilon$으로만 이루어진다면, GLS와 Pooled Estimator의 분산은 동일하다.


$$
\displaylines{if\quad \sigma_u^2=0,\,\quad \Omega=\sigma_\epsilon^2I_T\newline
then,\quad V_{GLS}=(\Sigma X'\Omega^{-1}X)^{-1}=\sigma^2_\epsilon(\Sigma X'X)^{-1}\newline
V_{pool}=(\Sigma X'X)^{-1}(\Sigma X'\Omega X)(\Sigma X'X)^{-1}=(\Sigma X'X)^{-1}\sigma^2}
$$





하지만 Pooled Regression에서 언급한 바와 마찬가지로 실제 상황에선 u와 $\epsilon$에 대해 주어진 정보가 제한적일 가능성이 높기 때문에, **feasible GLS estimator**가 replacing the unknown variance of u and $\epsilon$. 이에 대해선 너무 복잡해 다루지 않음.





### Fixed Effect

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



#### A. Within-Transformation) Individual Specific Mean & Demeaned Values

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
\displaylines{E(\hat\beta_{fe}|X)=\beta+(\Sigma X'M_TX)^{-1}(\Sigma X'M_TE(\epsilon|X))=0\quad with\;assumption\;of\;strict\;mean\;indep.}
$$

$$
E(\epsilon_i'\epsilon_i|X_i)=\Sigma_i
$$

$$
\displaylines{Var(\hat\beta_{fe}|X)=(\Sigma X'M_TX)^{-1}(\Sigma X'M_T\Sigma M_TX)(\Sigma X'M_TX)^{-1}\newline
=(\Sigma \dot X'\dot X)^{-1}(\Sigma \dot X'\Sigma \dot X)(\Sigma \dot X'\dot X)^{-1}\newline\newline
if\quad \Sigma=\sigma_\epsilon^2I_T\;(homoskedastic),\quad V_{fe}^0=\sigma_\epsilon^2(\Sigma \dot X'\dot X)^{-1}\newline
V_{fe}^0>= V_{pool}}
$$


Robust, but low efficiency



###  B) Differenced Estimator


$$
\displaylines{\Delta Y_{it}=Y_{it}-Y_{it-1} \quad for\;t=2,...,T\newline
then,\quad \hat\beta_\Delta=(\Sigma \Delta X'\Delta X)^{-1}(\Sigma \Delta X'\Delta y)\newline\newline
we\;can\;find\;out\;for\;T=2,\quad \hat\beta_{fe}=\hat\beta_\Delta}
$$


On can show that the differenced estimator is less efficient than within-transformation estimator.





### C) Dummy Variable Regression


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


### Cluster-Robust Covariance

allows $\epsilon$ to be heteroskedastic and serially correlated across t is the cluster-robust covariance matrix estimator


$$
\hat V_{fe}^{cluster}=(\dot X'\dot X)^{-1}(\Sigma\dot X'\epsilon'\epsilon\dot X)(\dot X'\dot X)^{-1}
$$




### D) Between Estimator


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
H_0:\;RE \quad \hat\beta_{RE}~=\hat\beta_{FE}\newline
H_1:\;FE \quad \hat\beta_{RE}!=\hat\beta_{FE}\newline
\newline
H=(\hat\beta_{FE}-\hat\beta_{RE})'(\hat V_{FE}-\hat V_{RE})(\hat\beta_{FE}-\hat\beta_{RE})
$$


Random Effect의 조건 중 강력한 가정은 $E[u|X]=0$이다.

Fixed Effect는 위 조건을 굳이 만족시키지 않아도 된다. 하지만 그 조건이 만족된다면 Random Effect가 효과적이면서도 robustness를 만족할 것이다.



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

