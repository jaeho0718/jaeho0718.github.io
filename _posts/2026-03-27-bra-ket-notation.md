---
title: "왜 양자역학에서는 디락표기법(Dirac-Notation)을 사용하는가?!"
date: 2026-03-27
categories: [Quantum Information Theory]
pinned: true
excerpt: "양자역학에서 왜 디락 표기법을 사용하는지 알아봅시다."
---

필자는 양자정보이론에 대해 학습하던 중 왜 양자역학에서는 우리가 알고있는 $\vec{v}$, 벡터 표기법을 사용하지 않고 디락 표기법이라 불리는 $\ket{k}, \bra{b}$를 사용하는지 궁금했다. 이에 대해 찾아보면서 깨닫게된 놀라운(?!) 사실을 포스트로 남긴다.

## 디락 표기법이란
양자역학에서는 벡터를 다룰 때 우리가 일반적으로 알고 있는 $\vec{v}$와는 다른 표기법을 사용한다. 일명 **브라-켓 (bra-ket)** 이라 부르며 $\bra{\psi}, \ket{\phi}$로 표기한다. 간단히 말하자면 브라 벡터($\bra{\phi}$)는 행 벡터이며, 켓 벡터($\ket{\psi}$)는 열 벡터이다.

$$
\begin{align*}
\ket{\phi} &= 
\begin{pmatrix}
a_1 \\ a_2 \\ a_3 \\ \vdots \\ a_n
\end{pmatrix} \\

\bra{\psi} &= 
\begin{pmatrix}
b_1 & b_2 & b_3 & \dots & b_n
\end{pmatrix}
\end{align*}
$$

## 양자 상태
양자역학에서 양자 상태 $\ket{\psi}$는 정규직교기저들(Orthonormal basis)의 선형 조합으로 나타낸다. 이때 $c_i$는 복소수이다.

$$
\ket{\psi} = \sum_i^{\infty}c_i\ket{E_i}
$$

> 양자정보이론에서는 유한개의 상태로 다루며 위의 식을 보고 "무한 합으로 구성하면 발산할 수 있지 않나?"라고 생각할 수 있다. 그러나 양자 상태 벡터는 힐베르트 공간의 원소이므로 항상 공간 내로 수렴한다. 이에 관해서는 ["왜 양자상태벡터는 힐베르트공간에서 정의되는가?"](2026-03-28-hilbert-space.md)에서 다룬다.

## 내적에 관하여
분명 해당 포스트는 **"디락 표기법을 왜 사용하는가?"** 에 관한 것인데 뜬금없이 내적이 나와 당황스러울 수 있다. 하지만 이후 디락 표기법의 놀라운 점을 얘기하기 위해서 반드시 언급해야하는 개념이므로 알아두자.

내적은 추상화된 벡터의 **크기** 와 벡터 간의 **각도** 를 알 수 있게해준다. 자기 자신과의 내적은 해당 벡터의 크기가 나오며, 다른 벡터와의 내적을 통해 두 벡터 사이의 각도를 알 수 있다. *(고등학교 때 배웠던 개념이다.)*

$$
\vec{v}\cdot\vec{w} = \|v\|\|w\|cos(\theta) \\
\vec{v}\cdot\vec{v} = \|v\|^2
$$
> 두 벡터의 내적은 스칼라곱(dot-product)으로 구할 수 있으며 왜 그러한지는 이 섹션의 끝부분에 정리하였다.

즉 내적은 **두개의 벡터를 입력으로 받아 복소수를 출력으로 하는 함수** 로 볼 수 있다.

$$
InProd(\vec{v}, \vec{w}) = c
$$

디락표기법으로 넘어가서 $\ket{\psi}, \ket{\phi}$의 내적은 $\braket{\psi\vert\phi}$로 표기하며 다음 성질을 만족한다.
1. $\braket{\psi\vert \phi+\delta} = \braket{\psi\vert\phi}+\braket{\psi\vert\delta}$
2. $\braket{\psi\vert a\phi} = a\braket{\psi\vert\phi}$
3. $\braket{\psi\vert\psi} \ge 0$

오른쪽 $\ket{\cdot}$에 대하여 우리의 기본 상식과 같게 동작하는 것을 알 수 있다. 그렇다면 왼쪽 $\bra{\psi}$에 대해서는 어떻게 동작할까?
예시로 $\braket{i\phi\vert i\phi}$에서 $\bra{i\phi}$에 대해서 위와 같은 성질을 만족한다 하면

$$
\begin{align*}
\braket{i\phi\vert i\phi} &= ii\braket{\phi\vert\phi} \\
&= -1\braket{\phi\vert\phi} \lt 0
\end{align*}
$$

자기자신과의 내적은 벡터 크기의 제곱이며 양수여야하는데 음수가 나온다.. 그렇다면 $\bra{\cdot}$는 다른 성질이 적용된다고 볼 수 있으며 그 성질은 다음과 같다.

1. $\braket{a\psi\vert \phi} = a^*\braket{\psi\vert\phi}$
2. $\overline{\braket{\psi\vert\phi}} = \braket{\phi\vert\psi} $

위의 성질을 앞선 예제 $\braket{i\phi\vert i\phi}$에 적용하면 문제없다.

$$
\begin{align*}
\braket{i\phi\vert i\phi} &= i\braket{i\phi\vert\phi} \\
&= i\braket{\phi\vert i\phi}^* \\
&= i(i)^*\braket{\phi\vert\phi}\\
&= i(-i)\braket{\phi\vert\phi}\\
&= 1\braket{\phi\vert\phi}
\end{align*}
$$

앞서 내적은 스칼라곱과 같다고 하였는데 왜 그러한지는 아래 증명을 보면 알 수 있다. 

$$
\begin{align*}
\text{동일 벡터공간 내 두 벡터}\ket{\psi} &= \sum_i a_i\ket{E_i},\ \ket{\phi}=\sum_j b_j\ket{E_j} \text{에 대하여} \\
\braket{\psi\vert\phi} &= \sum_i\sum_j \braket{a_iE_i\vert b_jE_j}\\
&= \sum_i\sum_j a_i^*b_j\braket{E_i\vert E_j} \\
&= \sum_i\sum_j a_i^*b_j\delta_{ij} & (\because\ket{E_i}\text{는 정규직교기저다.}) \\
&= \sum_i a_i^*b_i = Dot-product & (\because \text{여기서 a와 b는 실수인 경우다.})
\end{align*}
$$

## 선형 함수에 대하여
선형함수란 벡터를 받아 스칼라 값으로 변환해주는 함수다.

$$
L\vec{v} \rightarrow c
$$ 

실수 공간으로 보자면 $\mathbb{R}^n\rightarrow\mathbb{R}^1$으로 볼 수 있다. 이는 행 벡터로 나타낼 수 있으며 이를 **쌍대벡터 (Dual vector)** 라 부른다. 벡터가 벡터공간을 생성하는 것 처럼 쌍대벡터들도 쌍대공간(Dual space)을 생성한다. 쌍대공간은 벡터공간의 벡터들의 모든 선형함수 공간이다.

$$
L= \begin{bmatrix} a_1 & a_2 & \cdots & a_n\end{bmatrix}
$$

선형함수가 양자역학과 무슨 관련이 있는가? 양자상태에서 확률이나 기댓값등 값(value)을 얻기 위해서는 반드시 스칼라로 변환해야한다. 이 점을 보면 양자역학에 선형함수가 필요함을 납득할 수 있다.

## 선형 함수와 내적

드디어 디락표기법의 놀라운 점을 말할 때가 됐다. 선형함수와 내적간의 관계를 보자. 선형함수는 $\bra{L}\ket{\phi}$로 ,내적은 $\braket{\psi\vert\phi}$로 나타내는 것을 앞 섹션에서 살펴봤다.

간단한 선형 함수의 예시를 보자

$$
\begin{bmatrix} a & b\end{bmatrix} \begin{bmatrix} c \\ d \end{bmatrix} = a\cdot c+b\cdot d
$$

어디서 많이 본 것 않은가? 우리가 알고 있는 내적과 같다.

$$
\begin{bmatrix} a \\ b \end{bmatrix} \cdot \begin{bmatrix} c \\ d \end{bmatrix} = a\cdot c+b\cdot d
$$

**즉 선형함수는 대응하는 열벡터와의 내적으로 표현할 수 있다!**

$$
\begin{bmatrix} a & b\end{bmatrix} \vec{v} = \begin{bmatrix} a \\ b \end{bmatrix} \cdot \vec{v}
$$

이를 디락표기법을 이용해 나타내면 $\bra{\psi}\ket{\phi} = \braket{\psi\vert\phi}$이다.

$$
\bra{\psi}\ket{\phi} = \braket{\psi\vert\phi}
$$

**브라 ($\bra{\cdot}$)와 내적은 다른 개념이지만 디락표기법에서는 이 둘이 자연스럽게 연결된다.** 
덕분에 다음과 같은 놀라운 완비성 관계도 이끌어 낼 수 있다.
$$
\begin{align*}
\ket{\psi} = \sum_i c_i \ket{A_i}&, \ c_i = \braket{A_i\vert\psi} \text{에 대해} & (\because \ket{A_i}\text{는 정규직교 기저다.}) \\
\ket{\psi} &= \sum_i c_i \ket{A_i} \\
&= \sum_i \braket{A_i\vert\psi} \ket{A_i} \\
&= \sum_i \ket{A_i}\braket{A_i\vert\psi}  \\
&= \sum_i \ket{A_i}\bra{A_i}\ket{\psi}  & (\because \braket{\psi\vert\phi} = \bra{\psi}\ket{\phi})\\
&= (\sum_i \ket{A_i}\bra{A_i})\ket{\psi} \\
\text{즉} \sum_i \ket{A_i}\bra{A_i} &= I \text{ 임을 알 수 있다.}
\end{align*}
$$

> 이는 Riesz representation theorem (리즈의 표현 정리)에 근간을 두고 있으며 필자는 아직 해당 정리에 대한 공부를 하지 않아 해당 포스트에서는 다루지 않는다. 나중에 다뤄볼 예정이다.