---
layout: single
title: "[Mostly Harmless Econometrics] Theorem 3.1.1~6"
categories: learn
toc: true

---



# [Mostly Harmless Econometrics] Theorem 3.1.1~6



### 3.1.1

$$
\displaylines{The\;CEF-Decomposition\;Property\newline
Y_i=E[Y_i|X_i]+\epsilon_i \newline
i)\; \epsilon_i\;is\;mean\;independent\;of\;X_i\,;\;E[\epsilon|X]=0 \newline
ii)\; \epsilon_i\; is\;uncorrelated\;with\;any\;function\;of\;X_i}
$$



pf.


$$
\displaylines{i)\quad For\quad Y=E[Y|X]+\epsilon \newline
Note,\quad E[\epsilon|X]=0 \newline
Then,\quad E[\epsilon|X]=E[Y-E[Y|X]|X]=E[Y|X]-E[Y|X]=0 \newline \newline
ii)\quad let\;h(X_i)\;is\;a\;function\;of\;X_i\newline
E[h(X)\,\epsilon]=E\{h(X)\,E[\epsilon|X]\}=0,\;since\;E[\epsilon|X]=0}
$$







### 3.1.2

$$
\displaylines{The\;CEF-Prediction\;Property\newline
E[Y|X]=arg\,min\,E[(Y-m(X))^2]}
$$





pf.


$$
\displaylines{(Y-m(X))^2=((Y-E[Y|X])+(E[Y|X]-m(X)))^2\newline
=(Y-E[Y|X])^2+2(Y-E[Y|X])(E[Y|X]-m(X))+(E[Y|X]-m(X))^2\newline\newline
The\;first\;and\;second\;term\;do\;not\;affect;\;while\;the\;last\;term\;be\;minimzed\;where\;Y\;equals\;m(X)}
$$







### 3.1.3

$$
\displaylines{The\; ANOVA\; Theorem\newline
V(Y_i)=V(E[Y_i|X_i])+E[V(Y_i|X_i)]}
$$



pf.


$$
\displaylines{V(Y)=V(E[Y|X]+\epsilon)=V(E[Y|X])+V(\epsilon)\newline
Note,\;E[Y|X]\;and\;\epsilon\;are\;not\;correlated.\newline\newline
Then,\;the\; variance\; of\; \epsilon\; is\newline
E[\epsilon^2]=E[E[\epsilon^2|X]]=E[V[Y|X]]\newline
Note,\;E[\epsilon]\newline
Thus,\;V(Y)=V(E[Y|X])+E[V[Y|X]]}
$$







### 3.1.4

$$
\displaylines{The\; Linear\; CEF\; Theorem\; (Regression-justification\; I)\newline
Suppose\; the\; CEF\; is\; linear;\; then\; the\; population\; regression\; function\; is\; it.}
$$



pf.


$$
\displaylines{Suppose\; E[Y|X]=X'\beta^*;\newline
Since,\; E[X(Y-E[Y|X])]=0\;by\;CEF-Decomposition\;property\;(3.1.1)\newline
Then,\;by\;substitution,\;E[X(Y-E[Y|X])]=E[X(Y-X'\beta^*)]=E[XY-XX'\beta^*]=0\newline
Thus,\;\beta^*=E[XX']^{-1}E[XY],\;which\;refers\;\beta\;(the\;estimator\;for\;the\;population)}
$$







### 3.1.5

$$
\displaylines{The\; Best\;Linear\;Predictor\; Theorem\; (Regression-justification\; II)\newline
The\; function\; X'\beta\; is\; the\; best\; linear\; predictor\; of\; Y\; given\; X\; in\; a\; MMSE\; Sense.}
$$



pf.


$$
\displaylines{\beta\;is\;being\; defined \;for\; solving\newline
\beta=arg\,\underset b min\,E[(Y-X'b)^2]\newline\newline
\beta=E[XX']^{-1}E[XY]\newline
Derivation\; of\; the\; \hat\beta\; at\;the\; population\; regression\; would\; not\; be\; necessary.}
$$







### 3.1.6

$$
\displaylines{The\; Regression-CEF\; Theorem\; (Regression-justification\; III)\newline
The\; function\; X'\beta\; provides\; the\; MMSE\;linear\;approximation\;to\;E[Y|X],\;that\;is,\newline
\beta=arg\,\underset b min\,E\{(E[Y|X]-X'b)^2\}}
$$



pf.


$$
\displaylines{(Y-X'b)^2=\{(Y-E[Y|X])+(E[Y|X]-X'b)\}^2\newline
=(Y-E[Y|X])^2+(E[Y|X]-X'b)^2+2(Y-E[Y|X])(E[Y|X]-X'b)\newline\newline}
$$

$$
\displaylines{The\;first\; term\; does\; not\; involve\; b,\; and\; the\; last\; term\; has\; expectation\; zero\; by\; CEF-decomposition\; property \;(3.1.2).\newline
Thus,\; only\; second\; term\; has\; left,\; and\; the\; solution\; is\; same\; as\; the\; population\; least\; squares\; problem,\;which\;is,\newline
\beta=E[XX']^{-1}E[XY]\newline
}
$$

