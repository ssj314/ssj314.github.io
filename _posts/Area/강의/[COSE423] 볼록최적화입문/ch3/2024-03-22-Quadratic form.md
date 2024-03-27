---
title: Quadratic form
posted: YYYY-MM-DD hh:mm:ss +09:00
category: ["강의노트", "볼록최적화입문", "Chapter 3"]
---
지난 게시물에서 벡터 공간과 고유 벡터에 대해서 배웠다. 이번 포스팅에서는 Quadratic form(이차 형식)에 대해서 알아볼 것이다.

## Quadratic Form이란?
선형 대수학에서 이차 항만 존재하는 다항식을 Quadratic Form이라 한다. $x \in \mathbb{R}$일 때, 함수 $f(x) = ax^2$는 대표적인 이차 형식이다. 

이차 형식을 벡터 차원으로 확장할 수 있다. $x \in \mathbb{R}^n$인 벡터에 대해 이차 형식은 다음과 같이 정의한다.

$$
f(x)=x^TAx
$$

이 때, 행렬 $A$는 Symmetric이다. 왜 대칭 행렬을 쓰는 지는 뒤에서 배우겠다.

### 예시 1
---
벡터 $x=(x_1, x_2)$와 행렬 $$A=\begin{bmatrix} 4 & 0 \\ 0 & 3\end{bmatrix}$$를 가정해 보자. 그러면, 

$$
x^TAx=
\begin{bmatrix} x_1 & x_2 \end{bmatrix}
\begin{bmatrix} 4 & 0 \\ 0 & 3 \end{bmatrix}
\begin{bmatrix} x_1 \\ x_2 \end{bmatrix} 
=
\begin{bmatrix} x_1 & x_2 \end{bmatrix}
\begin{bmatrix} 4x_1 \\  3x_2 \end{bmatrix} 
$$

따라서, $f(x) = 4x_1^2+3x_2^2$이다.

### 예시 2
---
행렬 $$A=I=\begin{bmatrix} 1 & 0 \\ 0 & 1\end{bmatrix}$$를 가정해 보자. 그러면, $f(x)=x^Tx= ||x||^2$이다. 따라서, Norm도 Convex Function임을 알 수 있다.


## 대칭 행렬을 쓰는 이유
이차 형식에서 대칭 행렬만 쓰는 이유는 대칭이 아닌 행렬은 결국 대칭 행렬로 바꾸어 표현할 수 있기 때문이다. 어떤 이차 형식에서 행렬 $A$가 대칭이 아니라고 가정해 보자. 이차 형식의 값은 스칼라이므로 $f(x)=f(x)^T$가 성립한다. 따라서,

$$
\begin{align}
f(x) &= x^TAx=f(x)^T=x^TA^Tx \\ \\
f(x) &= \frac{x^TAx}{2} + \frac{x^TAx}{2} 
= \frac{x^TAx}{2} + \frac{x^TA^Tx}{2} 
= x^T \frac{(A^T + A)}{2} x 
\end{align}
$$

따라서, 이차 형식 $f(x)$는 $$Q=\frac{(A^T + A)}{2}$$인 대칭 행렬로 바꾸어 표현할 수 있다. 그렇기에 굳이 비대칭 행렬을 쓸 필요가 없는 것이다.


## 다양한 형태의 이차 형식
이차 형식은 크게 3가지 종류로 분류할 수 있다.
1. 한 점으로 모이는 형태
2. 한 쪽으로 무한히 뻗어나가는 형태
3. 위 아래로 무한히 발산하는 형태

![](https://i.imgur.com/laWbarv.png)*Figure 1. 다양한 형태의 이차 형식*

행렬의 부호에 따라 세 가지 형태로 분류되는데 다음 게시물에서 행렬의 부호를 구분하는 방법을 알아볼 것이다.
