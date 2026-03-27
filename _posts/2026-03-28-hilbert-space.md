---
title: "왜 양자상태벡터는 힐베르트공간에서 정의되는가?"
date: 2026-03-28
categories: [Quantum Information Theory]
pinned: false
excerpt: "힐베르트 공간이 무엇이며 왜 양자상태는 힐베르트공간내에서 다뤄지는지 알아봅시다."
---

양자역학에서의 양자상태는 힐베르트 공간내의 벡터이다. 그렇다면 힐베르트 공간이 무엇이며 왜 양자역학은 힐베르트 공간을 사용하는 것일까? 이번 포스트에서는 이에 대해 다뤄보고자 한다.

## 힐베르트 공간이란?
힐베르트 공간은 **완비 내적 공간 (Completeness inner product space)** 이다. 처음 책에서 이 정의를 접했을 때 상당히 당혹스러웠다. 내적이 정의된 공간이라는 것은 이해가 가는데 완비성이 무엇인지 몰랐고 따라서 완비 내적 공간이 무엇을 의미하는지 왜 양자역학에서 이를 사용하는지 이해할 수 있을리가 없었다. 

완비성, 내적 공간에 대한 정의를 설명하기 위해서는 공간에 대한 정의가 필요하며 단계별로 설명한 뒤 최종적으로 힐베르트 공간에 대한 해석을 제시하고자 한다.

## 위상 공간
우선 공간에 대해 대표적인 위상 공간에 대한 정의는 다음과 같다.

$$
\boxed{
\begin{aligned}
& \textbf{위상 (Topology)} \\[6pt]
& \text{다음 공리(Axiom)을 만족시키는 } X \text{의 부분집합들의 모임 } \tau \text{를} \\
& \text{집합 } X \text{ 위에서의 }\textbf{위상(Topology)}\text{이라 한다.} \\[6pt]
& \quad 1. \quad X, \varnothing \in \tau \\
& \quad 2. \quad \bigcup_{\alpha \in A} O_\alpha \in \tau \quad (\forall O_\alpha \in \tau) \quad \cdots \text{ 임의의 합집합에 닫혀있다} \\
& \quad 3. \quad O_1 \cap O_2 \in \tau \quad (\forall O_1, O_2 \in \tau) \quad \cdots \text{ 유한 교집합에 닫혀있다} \\[6pt]
& \text{이때 } \tau \text{와 } X \text{를 묶은 쌍 } (X, \tau) \text{을 }\textbf{위상 공간(Topological space)}\text{이라 한다.}
\end{aligned}
}
$$


## 거리 공간

## 내적 공간

## 완비성

## 완비 내적 공간