---
layout: single
title: "[Econometrics] 6. Matching"
categories: Econometrics
toc: true
toc_sticky: true
---

#propensity_score 



![match!](../../assets/images/2022-05-02-econometrics_6/match!.png)

아름다운 매칭의 순간이다.




# Matching

~~Angrist 교수는 Matching을 별로 안 좋아한다~~

Lalonde(1986, AER)에서 시작된 Matching은 연구 상황에서 흔히 발생하는, Control 그룹의 부재 (Treatment 그룹만 있을때) 속에서의 non-experimental estimators를 확인하고자 하는 것으로부터 시작했다.



## Strong Ignorability

***CIA + Overlap = Strong Ignorability***

X를 통제하면, 문제가 해결된다는 approach ~~또~~ CIA와 Overlap을 함께 가정한다. Overlap은 0과 1의 extremes들을 배제한다는 효과가 있다.



$$
\displaylines{\text{CIA : }\;\{Y_{0i},Y_{1i}\}\perp\!\!\!\perp C_i|X_i\\
\text{Overlap: }\; 0<Pr(D_i=1|X_i)<1}
$$


$$
\displaylines{\text{let} \quad \mu_0(x)=E[Y_{0i}|X_i=x], \quad \mu_1(x)=E[Y_{1i}|X_i=x]\\
\text{Then, }\quad \tau_{ate}(x)=E(Y_{1i}-Y_{0i}|X_i=x)\\
=\mu_1(x)-\mu_0(x)\\\\
\text{Then, }\quad ATE= \tau_{p}=E[\tau_{ate}(X_i)]\\
\text{and, }\quad ATT= \tau_{p}=E[\tau_{ate}(X_i)|D_i=1]
}
$$





Strong Ignorability는 아래와 같은 전개가 가능하게 한다.



$$
\mu_d(x)=E[Y_{di}|X_i=x]\\
=E[Y_{di}|D_i=d, X_i=x] \quad \text{by CIA}\\
=E[Y_{i}|D_i=d, X_i=x] \quad \text{by Overlap; *}\\\\


\text{*} \quad Y_i=Y_{1i}D_i+Y_{0i}(1-D_i)
$$



## Cattaneo. (2010). Smoking and Birthweight

![raw_scatter](../../assets/images/2022-05-02-econometrics_6/raw_scatter.png)



Matching에 대해 알아보기 위한 연구사례로 Cattaneo의 2010년 연구를 살펴보고자 한다. 

그는 위의 그래프처럼 산모의 나이와 출산한 아기의 birthweight을 scatter_plot 하였는데, 산모를 흡연자와 비흡연자로 나누어 확인하였다. 

두 manipulation은 그림에서처럼 각기 다른 색으로 구분되었다.

보다시피, 두 manipulated group 간에 가로축 밀도를 보면 흡연자의 경우에는 가로축 상의 좌측의 데이터들이 부족하고, 비흡연자의 산모들 같은 경우에는 가로축 밀도에 있어 우측의 밀도가 부족한 것을 볼 수 있다.



![potential_outcomes_plot](../../assets/images/2022-05-02-econometrics_6/potential_outcomes_plot.png)





## Regression Approach

![image-20220608210007807](../../assets/images/2022-05-02-econometrics_6/image-20220608210007807.png)







## Inverse Probability Weight (IPW)



































## Imbens & Wooldridge (2009)

Imbens, G.W., & Wooldridge, J.M. (2009). "Recent Developments in the Econometrics of Program Evaluation." Journal of Economic Literature, 47(1), 5-86











