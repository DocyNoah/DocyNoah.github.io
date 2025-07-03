---
title: 확률론의 수학적 기초 - Kolmogorov 공리와 확률 공간
description: 표본공간, 사건, σ-대수, 확률 측도의 정의부터 확률 연산의 기본 원리까지, 확률론의 엄밀한 수학적 기초를 Kolmogorov 공리를 중심으로 체계적으로 정리한 포스트
author: yohan
categories: [Math]
tags: [math, probability]
math: true
---

## 표본공간 (Sample Space)

### 정의

- 표본공간(Sample Space, $\Omega$): 통계적 실험에서 발생 가능한 모든 결과들의 집합
- 표본(Sample): 표본공간 $\Omega$의 각 원소 $\omega \in \Omega$로 하나의 구체적인 결과(Outcome)

### 예시

1. 동전 던지기 (이산형 표본 공간)
   - $\Omega = \\{H, T\\}$
2. 주사위 던지기 (이산형 표본 공간)
   - $\Omega = \\{1, 2, 3, 4, 5, 6\\}$
3. 정규분포를 따르는 실수 측정 값 (연속형 표본 공간)
   - $\Omega = \mathbb{R}$

<div class="box-info" markdown="1">
<div class="title"> 표본 공간의 크기 </div>
표본 공간의 크기는 표본 공간의 원소의 개수로 정의된다. 이산형 표본 공간의 크기는 유한 또는 가산 무한이며, 연속형 표본 공간의 크기는 비가산 무한이다.
</div>

## 사건 (Event)

### 정의

- 사건(Event): 표본 공간 $\Omega$의 부분집합

### 설명

- 사건 $A$와 표본 공간 $\Omega$의 관계: $A \subseteq \Omega$

### 예시

1. 동전 두 번 던지기
   - $\Omega = \\{HH, HT, TH, TT\\}$
   - 동전을 두 번 던져 첫 번째가 앞면인 사건: $A = \\{HH, HT\\}$
   - 동전을 두 번 던져 두 번째가 뒷면인 사건: $B = \\{HT, TT\\}$
   - 동전을 두 번 던져 앞면도 뒷면도 나오지 않는 사건: $C = \emptyset$
2. 주사위 던지기
   - $\Omega = \\{1, 2, 3, 4, 5, 6\\}$
   - 주사위를 던져 홀수가 나오는 사건: $A = \\{1, 3, 5\\}$
   - 주사위를 던져 짝수가 나오는 사건: $B = \\{2, 4, 6\\}$

## 멱집합 (Power Set)

### 정의

- 멱집합(Power Set): 집합의 가능한 모든 부분집합들의 집합

### 설명

- 집합 $\Omega$의 멱집합 $2^\Omega$은 다음과 같다.

$$
2^\Omega := \{A \mid A \subseteq \Omega\}
$$

### 예시

1. $\Omega = \\{a, b\\}$
   - $2^\Omega = \\{\emptyset, \\{a\\}, \\{b\\}, \\{a, b\\}\\}$
2. $\Omega = \\{1, 2, 3\\}$
   - $2^\Omega = \\{\\emptyset, \\{1\\}, \\{2\\}, \\{3\\}, \\{1, 2\\}, \\{1, 3\\}, \\{2, 3\\}, \\{1, 2, 3\\}\\}$

## $\sigma$-대수 ($\sigma$-Algebra)

### 정의

- $\sigma$-대수(Sigma-Algebra): 다음 세 조건을 만족하는 표본 공간 $\Omega$의 부분집합들의 집합 $\mathcal{F}$
  1. 공집합 포함

     $$
     \emptyset \in \mathcal{F}
     $$

  2. 여집합에 대해 닫힘

     $$
     A \in \mathcal{F} \Rightarrow A^c \in \mathcal{F}
     $$

  3. 가산 합집합에 대해 닫힘

     $$
     A_1, A_2, \ldots \in \mathcal{F} \Rightarrow \bigcup_{i=1}^\infty A_i \in \mathcal{F}
     $$

### 설명

- 확률을 부여할 수 없는 사건들도 있기에 확률 공간을 정의하기 위해 확률을 부여할 수 있는 사건들의 집합에 대한 정의가 필요하다.

$$
\Omega \xrightarrow{\text{모든 부분집합}} 2^\Omega \xrightarrow{\text{확률 부여 가능 사건 집합}} \mathcal{F}
$$

### 예시

1. 이산 집합의 $\sigma$-대수
   - $\Omega = \\{a, b\\}$
   - $\mathcal{F} = \\{\emptyset, \\{a\\}, \\{b\\}, \\{a, b\\}\\}$ = $2^\Omega$
2. 연속 집합의 $\sigma$-대수

<details class="details-block" markdown="1">
<summary>굳이 알 필요 없음</summary>
- $\Omega = \mathbb{R}$
- 연속 공간의 경우 $2^\Omega$ 전체에 확률을 정의하는 것이 불가능
  - 비탈리 집합이라고 이상한 비가측 집합이 존재 (비탈리에게 따져야 함)
  - 비탈리 집합에는 확률을 부여할 수 없는 사건들이 존재
- 그래서 정의된 것이 보렐 $\sigma$-대수 $B(\mathbb{R})$

  $$B(\mathbb{R}) := \sigma(\{(a, b) \mid a < b, \; a, b \in \mathbb{R}\})$$

    - 열린구간에 대해서만 정의해도 $(a, b), [a, b], (a, b]$ 등이 자연스럽게 포함됨
    - 우리가 직관적으로 생각할 수 있는 실수의 모든 구간을 포함하는 집합
    - 즉, 우리가 실수에 대해 "측정 가능한 사건"들을 다룰 수 있도록 만들어진 표준적인 $\sigma$-대수
</details>

## 확률 측도 (Probability Measure)

### 정의

- 확률 측도(Probability Measure): 표본 공간 $\Omega$의 측정 가능한 사건 $A \in \mathcal{F}$에 대해 확률 $P(A)$를 부여하는 함수

$$
P: \mathcal{F} \to [0, 1]
$$

- 확률 측도 $P$는 다음 세 조건(Kolmogorov 공리)을 만족한다.
  1. 비음수성 (Non-negativity): 확률은 0 이상 1 이하의 수이다.

     $$
     P(A) \geq 0 \quad \forall A \in \mathcal{F}
     $$

  2. 정규화 (Normalization): 전체 공간의 확률은 항상 1이다.

     $$
     P(\Omega) = 1
     $$

  3. 가산 가법성 (Countable Additivity): 서로소인 사건들의 가산 합집합에 대해 확률이 각각의 합과 같다.

     $$
     A_i \cap A_j = \emptyset \quad (i \ne j) \Rightarrow P\left(\bigcup_{i=1}^\infty A_i\right) = \sum_{i=1}^\infty P(A_i)
     $$

## 확률 공간 (Probability Space)

### 정의

- 확률 공간(Probability Space): 표본 공간 $\Omega$, $\sigma$-대수 $\mathcal{F}$, 확률 측도 $P$로 구성된 묶음(tuple)

$$
(\Omega, \mathcal{F}, P)
$$

## 확률 (Probability)

- 확률(Probability): 확률 공간 $(\Omega, \mathcal{F}, P)$에서 사건 $A \in \mathcal{F}$에 대해 확률 측도 $P$가 부여한 값 $P(A)$

### 설명

- 이산 확률 공간의 경우 사건 $A$의 확률은 다음과 같이 계산한다.

  $$
  P(A) = \sum_{\omega \in A} P(\{\omega\})
  $$

- 이산 확률 공간에서도 균등 분폴일 경우 다음이 성립한다.

  $$
  P(\{\omega\}) = \frac{1}{|\Omega|} \; \forall \omega \in \Omega \Rightarrow P(A) = \frac{|A|}{|\Omega|}
  $$

## 확률의 연산

### 덧셈 규칙 (Addition Rule)

- 임의의 두 사건 $A, B$에 대하여 다음이 성립한다.

  $$
  P(A \cup B) = P(A) + P(B) - P(A \cap B)
  $$

- 두 사건 $A, B$가 독립일 때, 다음이 성립한다.

  $$
  P(A \cup B) = P(A) + P(B)
  $$

### 조건부 확률 (Conditional Probability)

- 사건 $A$가 주어졌을 때, 사건 $B$의 확률은 다음과 같이 계산한다.

  $$
  P(B \mid A) = \frac{P(A \cap B)}{P(A)}, \quad P(A) > 0
  $$

- 두 사건 $A, B$가 독립일 때, 다음이 성립한다.

  $$
  P(B \mid A) = P(B)
  $$

### 곱셈 규칙 (Multiplication Rule)

곱셈 규칙은 조건부 확률에서 유도된다.

- 임의의 두 사건 $A, B \subseteq \Omega$에 대하여 다음이 성립한다.

  $$
  P(A \cap B) = P(A) \; P(B \mid A) = P(B) \; P(A \mid B)
  $$

- 두 사건 $A, B \subseteq \Omega$가 독립일 때, 다음이 성립한다.

  $$
  P(A \cap B) = P(A) \; P(B)
  $$
