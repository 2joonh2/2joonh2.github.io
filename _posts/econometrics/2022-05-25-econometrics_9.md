---
layout: single
title: "[Econometrics] 9. Regression Discontinuity"
categories: Econometrics
toc: true
toc_sticky: true
---

응용계량경제학 필기노트



![image-20220608200211007](../../assets/images/2022-05-25-econometrics_9/image-20220608200211007.png)

술로 인한 불연속성




# Regression Discontinuity

~~???: 결이 다르다~~

*RD designs take advantage of the fact that, for some treatments, access to the treatment is a discontinuous function of one or more forcing variables.*

*RD comes in two styles, fuzzy and sharp.*





## Sharp Regression Discontinuity Design (SRD)


$$
Y_i=(1-W_i)Y_{0i}+W_iY_{1i}
$$


여기서 W는 일종의 deterministic function이다. 이는 곧 아래와 같다.


$$
W+i=1\{X_i\geq c\}
$$


c라는 기준을 전후로 W가 다른 값을 갖는 것이며, prob이 아래 그림처럼 c를 기준으로 0과 1로 극단적으로 나뉘는 것을 볼 수 있다.

(이 도식에서 세로축은 W이다.)

![image-20220609010612121](../../assets/images/2022-05-25-econometrics_9/image-20220609010612121.png)





이때 가로축을 X, 세로축을 Y로 하는 도식화는 아래와 같을 것이다. 위의 점선은 $E[Y_1\|X=x]$이고, 아래의 점선은 $E[Y_0\|X=x]$이라고 볼 수 있다.

![image-20220609010651394](../../assets/images/2022-05-25-econometrics_9/image-20220609010651394.png)


$$
E[Y|X=x]=E[Y|W=0, X=x]Pr(W=0|X=x)+E[Y|W=1, X=x]Pr(W=1|X=x)
$$


c 포인트로 서로 다른 방향으로 접근하는 극한값의 차이가 곧 treatment effect가 되는 것이라고 할 수 있다.



### Interpretation of $\tau_{SRD}





추정(extrapolate)이 필요하다.



























예시를 살펴보자!

## Matsudaira. (2007)

Matsudaira. J.D. (2007) "Mandatory Summer School and Student Achievement" Journal of Econometrics 142:829-850.

미국에는 직전 봄학기 성적을 기준으로 여름 보충수업을 강제로 듣는 제도가 있는데, 이러한 기준을 전후로 발생하는 discontinuity를 통해 RD 를 활용한 연구를 진행하였다.

