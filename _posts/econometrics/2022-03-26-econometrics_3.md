---
layout: single
title: "[Econometrics] 3. Binary Choice"
categories: Econometrics
toc: true
toc_sticky: true

---

응용계량경제학 필기노트



# Binary Choice



## Limited Dependent Variables

종속변수에 limitation이 있음

제한된 값(ex. 0 or 1 / 1~4)

이번 챕터에서는 종속변수 Y가 0 또는 1의 값만 갖는 binary variable임을 밝힌다.

$P[Y=1|X] \;:\; Response\; Probability$

Response Probability의 X로의 Derivative를 **Marginal Effect**라고 부른다.



### Response Probability & Marginal Effect


$$
p(x)=P[y=1|X=x]=E[Y|X=x]
$$


then, the **Marginal Effect** is


$$
{\partial \over \partial x}p(x)={\partial \over \partial x}P[y=1|X=x]={\partial \over \partial x}E[Y|X=x]
$$


Marginal Effect는 곧, X가 1(단계) 증가할때, Y가 1일 확률이 얼마나 변화하는가. 라는 미시경제학의 marginal 개념과 같은 결이다.


$$
Y=P(X)+e
$$


$Var(e|X)=P(X)(1-P(X))$ 이므로, e는 heteroskedastic하며, 즉 classical error라고 할 수 없다.



## Binary Choice Models

위 Y와 P(X)의 관계를 설명하는 모델을 빌트해보자.



### Linear Probability Model

말그대로 OLS

한 줄로 요약하면, *무식하지만 깔끔하고, 그래서 무식하다* 라는 것이다.



장점: 돌리기 쉽고, 해석이 쉽다.

$marginal effect = \beta$



### Index Model

Linear 모델의 단점을 보완한 모델이다.

0과 1 사이의 값을 벗어나지 않도록 아래와 같은 transformation을 진행하는 것이다. 이를 **single index model**이라고도 불린다.





### Probit Model

Normal 분포의 CDF를 이용

항상 0과 1사이의 값만을 갖는 점을 활용한 모델이다.





### Logit Model

예전에 비해 컴퓨터 파워가 근심거리가 아닌 요즘은 Logit과 Probit 모두 적절히 혼용되고 있다.













