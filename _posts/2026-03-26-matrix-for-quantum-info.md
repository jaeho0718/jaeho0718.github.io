---
title: "양자정보이론을 위한 선형대수"
date: 2026-03-26
categories: [Quantum Information Theory]
pinned: false
excerpt: "양자정보이론을 다루는데 있어 필수적인 선형대수 개념을 정리합니다"
image: ""
---

## 개론
본 포스트에서는 양자역학 및 양자정보이론을 이해하기 위해 필요한 **선형대수**개념에 대해 정리한다. 선형대수 개념에 물리학자들은 양자역학용으로 **디락 표기법 (Dirac Notation)** 을 도입했는데 차후 다룰 양자역학공론 및 양자정보이론을 이해하는데 있어 반드시 익숙해져야할 표기법이다. 따라서 선형대수 개념과 함께 **디락 표기법** 도 같이 설명할 것이다.

## 1. 디락 표기법 (Dirac Notation)

선형대수의 기본 대상은 **벡터 공간 (Vector space)** 이며 이러한 벡터 공간들 중 집중할 부분은 복소수로 구성된 **복소 벡터 공간** 이다. 
$$
\mathbb{C}^n: \text{복소벡터 }\{z_1, z_2, ..., z_n\}\text{로 구성된 복소 벡터 공간}
$$

벡터 공간의 원소는 열 행렬 표기법 (Column Matrix Notation)을 통해 나타내며, 이는 디락 표기법에서 $\vert \cdot \rangle (ket)$로 나타낸다.

$$
\vert v \rangle =
\begin{pmatrix}
z_1 \\ z_2 \\ z_3 \\ \vdots \\z_n
\end{pmatrix}
$$

행 벡터의 경우 $\langle\cdot\vert (bra)$ 로 나타낸다. *(벡터 $v$의 쌍대벡터, dual-vector라 부르기도 한다)*

$$
\langle v \vert =
\begin{pmatrix}
z_1^* \ z_2^* \ z_3^* \ \cdots \ z_n^*
\end{pmatrix}
$$

> 벡터 공간의 정의 자체는 차후 힐베르트 공간에 대한 정의에 대한 포스트에서 다룰 예정이다.

## 2. 기저와 선형독립 (Basis and Linarly Independent)
**기저(Basis)** 를 설명하기 앞서 **생성 집합(Spanning set), 생성(Span), 선형종속(Linearly Dependent)** 개념을 알 필요가 있다. 

1. **생성 집합(Spanning set)** : 벡터 공간에 속한 벡터를 이용하여 해당 벡터 공간내 벡터를 표현할 수 있는 벡터 집합
$$
\{\vert v_1\rangle, \vert v_2\rangle, \cdots, \vert v_n\rangle \} \text{에 대하여 } \vert v \rangle = \sum_i a_i\vert v_i \rangle
$$

2. **생성(Span)** : 생성집합이 벡터 공간을 만드는 것

3. **선형 종속(Linearly Dependent)** 
$$
\begin{gather*}
\text{적어도 하나의 } a_i \neq 0 \text{ 일 때} \\
a_1 \vert v_1 \rangle + a_2 \vert v_2 \rangle + \cdots + a_n \vert v_n \rangle = 0 \\
\text{를 만족하는 } \text{복소수 집합} \{a_1, a_2, \cdots, a_n\} \text{은 선형 종속이다.}
\end{gather*}
$$

선형종속과 반대 $a_1 \vert v_1 \rangle + a_2 \vert v_2 \rangle + \cdots + a_n \vert v_n \rangle \neq 0$인 복소수 집합은 **선형 독립(Linearly Independent)** 라 한다. 선형 독립이며 벡터 공간을 생성하는 복소수 벡터 집합을 **기저 (Basis)** 라 부르며 기저의 원소 수가 해당 공간의 **차원**이 된다.

## 3. 선형연산자와 행렬
선형 연산자는 다른 벡터 공간으로 변환하는 연산이며 선형 연산자 $A$에 대해 $A: V \rightarrow W$ 로 정의된다.
$$
A(\sum_i a_i\vert v_i \rangle ) = \sum_i a_iA(\vert v_i \rangle)
$$

선형 연산자($A: V\rightarrow W$)는 다음과 같이 행렬로 나타낼 수 있다. *($\vert v_i \rangle, \vert w_j \rangle$는 기저벡터다.)*
$$
A\vert v_j \rangle =
\begin{pmatrix}
A_{1j} \\ A_{2j} \\ \vdots \\ A_{nj}
\end{pmatrix}
= \sum_i A_{ij}\vert w_i \rangle
$$
> 위 식을 직관적으로 설명하자면 벡터 $\vert v_j \rangle$의 선형 연산은 출력기저의 합으로 나타낼 수 있음을 보인 것이다.

### 파울리 행렬 (Pauli Matrix)
선형 연산자들 중 유용한 연산자 (파울리 연산자)는 양자정보이론에서 많이 사용되므로 소개한다.

| 연산자 | 기호 | 행렬 표현 |
|:---:|:---:|:---:|
| 파울리 $X$ | $\sigma_x$ | $\begin{bmatrix} 0 & 1 \\ 1 & 0 \end{bmatrix}$ |
| 파울리 $Y$ | $\sigma_y$ | $\begin{bmatrix} 0 & -i \\ i & 0 \end{bmatrix}$ |
| 파울리 $Z$ | $\sigma_z$ | $\begin{bmatrix} 1 & 0 \\ 0 & -1 \end{bmatrix}$ |
| 항등 연산자 $I$ | $\sigma_0$ | $\begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$ |

## 4. 내적 (Inner Product)
내적이란 어떤 벡터공간의 두 벡터를 입력으로 받아 복소수를 출력하는 함수로 $\langle v \vert w \rangle$로 나타낸다. 이때 벡터 공간은 내적공간이어야 하며 다음 조건 만족 시 내적이 된다.
1. 선형성: $\langle x+z \vert y \rangle = \langle x \vert y \rangle+\langle z \vert y\rangle$, $\langle v|\lambda w\rangle = \lambda\langle v|w\rangle$,  $\langle \lambda v|w\rangle = \lambda^*\langle v|w\rangle$
2. 켤레 대칭: $\overline{\langle v \vert w \rangle} = \langle w \vert v \rangle$
3. $\langle v \vert v \rangle \ge 0$ 이며 등호를 만족시키는 필요충분조건은 $\vert v \rangle = 0$이다.


> 내적공간에 관해서는 힐베르트 공간에 대한 포스트에서 다룰 예정이다.


- $\langle v \vert w \rangle=0$ 일때 두 벡터는 **직교**한다.
- 벡터의 노름(Norm): $\| \vert v \rangle \| = \sqrt{\langle v \vert v \rangle}$
- 단위 벡터(Unit vector): 벡터의 노름이 1인 벡터

[선형 연산자와 행렬](#3-선형연산자와-행렬)에서 연산자를 내적을 이용해서 표현할 수 있는데, 연산자 $A: V\rightarrow W$는 각 벡터공간 $V,W$에 속한 벡터 $\vert v \rangle, \vert w \rangle$에 대해 $\vert w \rangle \langle v \vert$로 나타낸다.
$$
(\vert w \rangle \langle v \vert) \vert v' \rangle = \langle v \vert v' \rangle \vert w \rangle
$$
이는 벡터 $\vert w \rangle$에 복소수 $\langle v \vert v' \rangle$를 곱한 것이라 본다. 

### 완비성 관계 (Completness Relation)
벡터 공간 $V$에 대한 정규직교 기저 $\vert i \rangle $에 대해 $\vert v \rangle = \sum_i v_i\vert i \rangle$인 벡터에 연산자 $\sum_i\vert i \rangle \langle i \vert$를 적용하면 
$$
\sum_i\vert i \rangle \langle i \vert v \rangle = \sum_i v_i\vert i \rangle = \vert v \rangle
$$
가 되며 따라서 $\sum_i\vert i \rangle \langle i \vert = I$를 만족한다. 이떄 $\sum_i\vert i \rangle \langle i \vert = I$를 **완비성 관계** 라 한다. 

이를 응용하여 어떠한 [선형연산자](#3-선형연산자와-행렬)를 외적으로 나타낼 수 있다.
$$
\begin{align*}
A&: V \rightarrow W \\
A &= I_WAI_V \\
&= \sum_{i,j} \vert w_i \rangle \langle w_i \vert A \vert v_j \rangle \langle v_j \vert \\
&= \sum_{i,j} \langle w_i \vert A \vert v_j \rangle \vert w_i \rangle \langle v_j \vert 
\end{align*}
$$s
*(선형 연산자를 외적으로 나타내는 예시)*

## 5. 고유벡터와 고유값 (Eigen vector, Eigen value)
$$
A\vert v \rangle = \lambda \vert v \rangle
$$
위의 식을 만족하는 $\lambda$를 $A$의 고유값(Eigen value), $\vert v \rangle$를 $A$의 고유벡터라 하며 고유공간(Eigen space)은 $\lambda$ 고유값을 갖는 벡터 집합이다.

고유값을 찾는 방법에 대해 다시 복기해보자. 고유값이 존재하기 위해서는 $(A-\lambda I )\vert v \rangle = 0$을 만족하는 $\vert v \rangle$가 존재해야하며 이는 $(A-\lambda I)$의 역행렬이 존재하면 안됨을 말한다. 즉 $det(A-\lambda I)=0$인 $\lambda$를 구하면 고유값을 찾을 수 있다.

하나의 고유값 $\lambda$에 대하여 선형 독립인 고유벡터가 여러개 존재할 경우 축퇴(Degenerate)되었다고 얘기한다. 축퇴가 도리 경우 기저 선택의 자유도가 달라지는데 하나의 고유값에 대한 여러개의 선형독립 고유벡터가 생성한 고유공간내에서 기저선택이 가능하기 떄문이다. *(고유공간내 어떠한 벡터들도 고유벡터가 된다.)* 반면 비축퇴(Non degenerate)의 경우 하나의 고유값에 대해 하나의 고유벡터만 있기 때문에 측정값 하나당 기저가 하나씩 선택된다.

## 6. 에르미트 켤레와 에르미트 연산자 (Hermitian conjugate and Hermition operator)
힐베르트 공간 $V$에서 임의의 선형연산자 $A$에 대하여 $(\vert v \rangle,A\vert w \rangle)=(A^\dagger \vert v \rangle, \vert w \rangle)$을 만족하는 유일한 선형 연산자 $A^\dagger$가 존재하며 이를 $A$연산자의 **에르미트 켤레(Hermitian conjugate)** 라 부른다. 이때 $A^\dagger = (A^T)^*$이다.

연산자 $A$가 $A^\dagger$와 같을 떄 이를 **에르미트 연산자(Hermitian operator)** 라 부른다.
$$ 
A = A^\dagger
$$

### 사영 연산자 (Projector)
에르미트 연산자 중 중요한 것은 사영연산자다. 벡터공간 $V, W$에 대해 연산자 $P: V \rightarrow W$는 다음과 같이 정의할 수 있다.
$$
P \equiv \sum_i \vert i \rangle \langle i \vert
$$
($\vert i \rangle$은 벡터공간 $W$의 정규직교기저이다.)

위의 식을 분석하자면 벡터 공간 $V$의 벡터 $\vert v \rangle$에서 벡터공간 $W$의 성분값을 추출 ($\langle i \vert v \rangle$, 복소값)이를 다시 벡터공간 $W$의 벡터로 맵핑 ($\langle i \vert v \rangle \vert i \rangle$) 하는 것으로 볼 수 있다.

직교여연산자$Q$는 $Q \equiv I-P$로 정의한다.
> $m$ 차원 벡터 공간 $V$의 기저 $\{\vert v_1 \rangle, \vert v_2 \rangle, \cdots, \vert v_m \rangle \}$, 벡터공간 $V$의 부분공간이자 $n$차원인 벡터 공간 $W$의 기저 $\{\vert v_1 \rangle, \vert v_2 \rangle, \cdots, \vert v_n \rangle \}$ 에 대해 사영연산자 $P: V \rightarrow W$의 직교여연산 $Q$는 $\{\vert v_{n+1} \rangle, \vert v_{n+2} \rangle, \cdots, \vert v_m \rangle \}$로의 투영이다.

## 7. 스펙트럼 분해 (Spectral Decomposition)
에르미트 연산자 $A$는 고유값 $\lambda_i$와 고유벡터 $\vert v_i \rangle$에 대해 항상 $A=\sum_i \lambda_i\vert v_i\rangle\langle v_i\vert$로 분해된다. 이를 스펙트럼 분해(Spectral Decomposition)이라 부른다. 

이는 양자 역학에서 관측과 연결되며 특정 기저로의 관측값 즉 고유값을 얻는데 사용된다. 예를 들어 측정연산자 $M_i = \sum_i \lambda_i \vert i \rangle \langle i \vert$로 측정을 한다고하자. *(측정연산자에 대한 것은 추후 양자측정에서 자세히 설명할 것이니 여기서는 예시로 넘어가면된다.)*
이때 $\lambda_i$가 측정될 확률은 해당 고유값의 고유벡터 $\vert i \rangle$을 통해 $P(\lambda_i) = \vert\langle i \vert \psi \rangle \vert^2$로 나타낸다.

$$
\begin{align*}
\langle \psi \vert M\vert \psi \rangle &= \sum_i\lambda_i\langle\psi\vert i \rangle \langle i\vert\psi\rangle \\
&= \sum_i \lambda_i \overline{\langle i \vert\psi\rangle} \langle i \vert \psi \rangle \\ 
&= \sum_i \lambda_i P(\lambda_i) \\
&= \mathbb{E}(\lambda_i)
\end{align*}
$$

## 8. 텐서곱 (Tensor product)
텐서곱은 벡터공간을 더 큰 벡터공간으로 표현하는 방식이다. 이는 단일 양자계뿐 아닌 다입자계를 설명하는데 사용된다. 텐서곱 표현은 아래와 같다.

$$
\begin{align*}
&\vert v \rangle \otimes \vert w\rangle \\
&= \vert v \rangle \vert w \rangle \\
&= \vert vw \rangle
\end{align*}
$$

텐서곱의 성질은 다음과 같다.
1. $z(\vert v \rangle \otimes \vert w \rangle) = (z\vert v \rangle)\otimes\vert w \rangle = \vert v \rangle \otimes (z\vert w \rangle)$
2. $(\vert v_1 \rangle + \vert v_2 \rangle)\otimes \vert z \rangle = \vert v_1 z \rangle + \vert v_2 z \rangle$
3. $\vert v \rangle \otimes (\vert w_1 \rangle + \vert w_2\rangle) = \vert vw_1\rangle+\vert vw_2\rangle$

동일한 상태의 반복적인 텐서곱 $\vert \psi \rangle \vert\psi\rangle\cdots\vert\psi\rangle = \vert\psi\rangle^{\otimes k}$로 나타낼 수 있다. 

연산자가 텐서곱 공간에 적용시 선형성이 보장하는 방식으로 $V\otimes W$ 모든 원소로 확장된다. 
$$
(A_v\otimes B_w)(\vert v \rangle \otimes \vert w \rangle) \equiv A\vert v \rangle \otimes B \vert w \rangle
$$

이러한 텐서곱은 크로네커 곱 (Kroneker product)를 통해 나타낼 수 있다. (연산자 $A$는 $m\times n$행렬)
$$
A \otimes B = 
\begin{pmatrix}
A_{11}B & A_{12}B & \cdots & A_{1n} \\
A_{21}B & \cdots & & A_{2n} \\
\vdots & \ddots \\
A_{m1}B & A_{m2}B & \cdots & A_{mn}
\end{pmatrix}
$$

## 9. 연산자 함수 

## 9. 극 분해 (Polar decomposition)

