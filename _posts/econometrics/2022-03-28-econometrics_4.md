---
layout: single
title: "[Econometrics] 4. Multiple Choice"
categories: Econometrics
toc: true
toc_sticky: true
---

응용계량경제학 필기노트



# Multiple Choice

## Multinomial Response

Y takes values in a finites set,


$$
Y\in \{1,2,...,j\}
$$


선택가능한 옵션들은 **alternatives**라고 부른다.

예를 들어, 한 개인이 서울에서 부산으로 가고자 할 때, 고를 수 있는 옵션은 1: 비행기, 2: 기차, 3: 자가용, 4: 도보(?) 등이 있을 것이다.



The utility of alternative j is assumed to equal


$$
U_j^*=X'\beta_j+\epsilon_j
$$


여기서 $\epsilon_j$는 individual-specific, and contains unobserved factors 들을 포함하는 에러텀이다.

이렇게 정의된 각 alternative의 utility를 기반으로 사용자의 선택을 예측하는 것은 곧,


$$
Y=j,\;if\;U^*_j \geq U^*_l\;(for\;all\;l)
$$


다른 어떤 alternative의 utility보다 j의 utility가 높음을 의미한다.



### Location of $\beta_j% cannot be identified

앞서 multinomial choice의 alternative가 선택되는 것은 다른 alternatives와의 상대적인 비교를 통해 가장 높은 utility의 alter가 선택되는 것임을 알 수 있었다. 

그렇기 때문에, 곧, $\beta_j$의 절대적인 위치 (location)는 알 수 없다는 것을 뜻하기도 한다.

또 다른 의미로는, 개개인의 특성계수값을 모아놓은 X에 대하여 어떤 상수 $\gamma$를 곱해 더하거나 빼는 것(혹은 전체 utility에 상수를 곱하거나)은 모든 alternative에 동일하게 적용된다 할 때에, 선택에 영향을 줄 수 없음을 뜻한다.



따라서, 우리는 모델을 초기 생성하여 디자인하는데에 있어선, locations들을 normalization 시켜줄 필요성을 느낀다.

첫번째 내지 마지막 번째 등, 특정 alternative의 location을 0으로 함에 따라 normalization을 할 수 있을 것이다.



## Models



### Multinomial Logit


$$
P_j(x)=\frac{exp(x'\beta_j)}{\Sigma \,exp(x'\beta_l)}
$$


alternatives가 두 개 뿐일때, 위의 식은 다시금 binary model의 logit model의 식과 동일하다는 것을 알 수 있다.





#### Likelihood

곧바로 likelihood에 대해서도 derive를 해보자.

Y의 prob mass function은 아래와 같다.


$$
\displaylines{\pi(Y|X,\beta)=\Pi\, P_j(X|\beta)^{1\{Y=j\}}\newline
l_n(\beta)=\Sigma\Sigma\, 1\{Y_i=j\}\,log\,P_j(X_i|\beta)\newline
\hat\beta=arg\,max\,l_n(\beta)}
$$


본 $\beta$ estimator는 손으로 구할 수 없기 때문에, Stata 상에서는 numerical 한 방법으로 $\hat\beta$를 구해준다. 



#### Marginal Effect


$$
marginal\; effect\; :\;\frac{\partial}{\partial x}P_j(x)=P_j(x)\,(\beta_j-\Sigma\,\beta_lP_l(x))
$$


Derivation)


$$
\displaylines{P_j(x)=\frac{exp(x'\beta_j)}{\Sigma \,exp(x'\beta_l)}=\frac{exp(x'\beta_j)}{A}\newline
\frac{\partial P_j(x)}{\partial x}=\beta_j exp(x'\beta_j)A^{-1}-exp(x'\beta_j)A^{-1}\Sigma exp(x'\beta_l)\beta_l A^{-1}\newline
=\beta_jP_j-P_j\Sigma P_l\beta_l\newline
=P_j(\beta_j-\Sigma \beta_l P_l)}
$$


### Conditional Logit

교통수단의 비용, 소요시간 등 각각의 alternative 별로 또 다른 attributes들은 어떻게 처리할 것인가? (기존의 multinomial logit의 X는 개개인의 attributes들로 이루어진 벡터였음을 상기하자)

새로이 우리는 alternative-specific regressors를 적용시켜보며, 이를 Conditional Logit Model의 이름으로 발전되어왔다 (McFadden, 1970).



