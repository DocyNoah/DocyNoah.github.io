---
title: 확률 기반 생성 모델의 역사적 발전과 핵심 개념 정리
description: Score Matching부터 VAE, Diffusion Model을 거쳐 Flow Matching까지, 확률 기반 생성 모델의 주요 논문들과 핵심 개념을 시간순으로 정리
author: yohan
categories: [Machine Learning, Generative Models]
tags: [Deep Learning, Generative AI, Score Matching, Autoencoder, VAE, Diffusion Model, Flow Matching, Probabilistic Models, Neural Networks, Mathematics]
math: true
---

## 2005 — Score Matching

### Estimation of Non-Normalized Statistical Models by Score Matching

- Aapo Hyvärinen, and Peter Dayan.
- JMLR 2005
- 2,000++ citations
- [JMLR](https://jmlr.org/papers/v6/hyvarinen05a.html)

### 정규화 불가능한 분포 학습을 위한 대안

- 기존 MLE은 정규화 상수 $Z(\theta)$ 계산이 불가능한 경우 사용 불가
- Score Matching은 $\nabla_x \log p_\theta(x)$만을 사용하여 학습 가능
- 손실 함수:

  $$
  J(\theta) = \mathbb{E}_x\left[\frac{1}{2} \left\| \nabla_x \log p_\theta(x) \right\|^2 + \nabla_x^2 \log p_\theta(x)\right]
  $$

- 정규화 항 제거로 계산 효율성과 수치적 안정성 확보
- Energy-based model 및 후속 score-based generative model의 이론적 기반 마련

---

## 2006 — Autoencoder

### Reducing the Dimensionality of Data with Neural Networks

- Geoffrey E. Hinton, and Ruslan R. Salakhutdinov.
- Science 2006
- 10,000++ citations
- [Science](https://www.science.org/doi/10.1126/science.1127647)

### 비선형 차원 축소를 위한 신경망 기반 접근

- 기존 PCA는 선형 구조만 모델링 가능하여 복잡한 데이터의 저차 표현에 한계 존재
- 신경망 기반 autoencoder를 통해 입력 $x$를 잠재변수 $z$로 압축하고 재구성하는 비선형 차원 축소 방식 제안
- 인코더: $z = f(x)$, 디코더: $\hat{x} = g(z)$로 구성되며 재구성 오차 $\left\| x - \hat{x} \right\|^2$를 최소화
- 확률 분포나 정규화 상수에 대한 가정 없이 end-to-end 학습 가능
- 이후 확률적 latent 모델(VAE) 및 representation learning 발전의 기반이 됨

---

## 2008 — Denoising Autoencoder

### Extracting and Composing Robust Features with Denoising Autoencoders

- Pascal Vincent, Hugo Larochelle, Yoshua Bengio, and Pierre-Antoine Manzagol.
- ICML 2008
- 10,000++ citations
- [Toronto](https://www.cs.toronto.edu/~larocheh/publications/icml-2008-denoising-autoencoders.pdf)
- [ACM - ICML](https://dl.acm.org/doi/10.1145/1390156.1390294)

### 노이즈 복원을 통한 견고한 표현 학습

- 일반 autoencoder는 입력을 거의 그대로 복사하는 방식으로 의미 있는 표현을 학습하지 못하는 한계 존재
- 입력 $x$에 노이즈를 추가한 $\tilde{x}$에서 원래 입력 $x$를 복원하도록 학습하는 denoising autoencoder 제안
- 손실 함수는 $\left\| x - g(f(\tilde{x})) \right\|^2$로 정의되며, $f$는 인코더, $g$는 디코더
- 입력 공간의 주변 분포 구조를 반영한 표현을 학습하며, 특징의 일반화와 견고성 향상
- 이후 representation learning, pretraining, semi-supervised learning 등에 널리 응용됨

---

## 2013 — Variational Autoencoder (VAE)

### Auto-Encoding Variational Bayes

- Diederik P. Kingma, and Max Welling.
- ICLR 2014
- 45,000++ citations
- [arXiv](https://arxiv.org/abs/1312.6114) (Released in 2013.12.20.)
- [OpenReview - ICLR](https://openreview.net/forum?id=33X9fd2-9FyZd)

### 확률적 인코딩을 통한 생성 모델 학습

- 기존 autoencoder는 잠재 공간에 대한 확률적 해석이 불가능하고 생성 능력이 제한적
- 입력 $x$에 대한 잠재 변수 $z$의 사후 분포 $q_\phi(z \vert x)$를 추정하고, 이를 이용해 생성 모델 $p_\theta(x \vert z)$를 학습하는 variational autoencoder 제안  
- 학습 목적은 ELBO 최대화이며, 식은 다음과 같음:

  $$
  \mathbb{E}_{q_\phi(z \vert x)} [\log p_\theta(x \vert z)] - D_{KL}(q_\phi(z \vert x) \Vert p(z))
  $$

- reparameterization trick을 통해 미분 가능하게 구현
- 확률적 latent space와 end-to-end 학습이 결합된 대표적 생성 모델로, 이후 확률 생성모델 연구의 중심이 됨

---

## 2020 — Diffusion Model (Stochastic, Discrete Time)

### Denoising Diffusion Probabilistic Models

- Jonathan Ho, Ajay Jain, and Pieter Abbeel.
- NeurIPS 2020
- 22,000++ citations
- [arXiv](https://arxiv.org/abs/2006.11239) (Released in 2020.06.19.)
- [NeurIPS](https://proceedings.neurips.cc/paper/2020/hash/4c5bcfec8584af0d967f1ab10179ca4b-Abstract.html)

### 확률적 노이즈 제거를 통한 고품질 샘플 생성

- 기존 likelihood 기반 생성 모델은 고품질 이미지 생성에서 한계를 보임
- 데이터를 점진적으로 노이즈화하는 Forward Diffusion Process $q(x_t \vert x_{t-1})$와, 이를 역으로 제거하는 생성 모델 $p_\theta(x_{t-1} \vert x_t)$를 정의
- 각 단계는 조건부 가우시안 분포로 설정되며, 전체 학습은 ELBO 최대화로 구성됨
- 손실 함수는 시간별 예측된 노이즈 $\epsilon_\theta(x_t, t)$와 실제 노이즈 $\epsilon$ 간의 MSE로 근사:

  $$
  \mathbb{E}_{x, \epsilon, t}\left[ \left\| \epsilon - \epsilon_\theta(x_t, t) \right\|^2 \right]
  $$

- 매우 높은 샘플 품질을 보이며 이후 score-based 모델 및 diffusion 발전의 핵심 기반이 됨

---

## 2021 — SDE-based Diffusion Model (Stochastic, Continuous Time)

### Score-based Generative Modeling through Stochastic Differential Equations

- Yang Song, Jascha Sohl-Dickstein, Diederik P. Kingma, Abhishek Kumar, Stefano Ermon, and Ben Poole
- ICLR 2021
- 7,000++ citations
- [arXiv](https://arxiv.org/abs/2011.13456) (Released in 2020.11.26.)
- [OpenReview - ICLR](https://openreview.net/forum?id=PxTIG12RRHS)

### Continuous-time Diffusion과 Score 기반 샘플링 통합

- 기존 Diffusion Model은 정해진 time-step에 의존해 샘플링 속도가 느리고 유연성이 제한됨
- Stochastic Differential Equations(SDE)과 Score Function $\nabla_x \log p_t(x)$를 결합해 Score-based Generative Modeling을 제안
- Forward Process은 노이즈 SDE로 정의되고, Reverse SDE를 통해 샘플 복원
- 학습은 다수의 시간 $t$에 대해 score network $s_\theta(x, t) \approx \nabla_x \log p_t(x)$를 예측하도록 score matching loss로 수행
- 샘플링은 Reverse SDE를 수치적 방법(Heun, Euler 등)으로 적분하여 수행
- Diffusion Model의 샘플 품질을 유지하면서 시간 해상도 자유도와 score 기반 이론을 결합한 구조로, 이후 ODE-based Diffusion Model, flow matching 등으로 확장됨

---

## 2021 — Diffusion Model (Deterministic, Discrete Time)

### Denoising Diffusion Implicit Models

- Jiaming Song, Chenlin Meng, Stefano Ermon
- ICLR 2021
- 8,000++ citations
- [arXiv](https://arxiv.org/abs/2010.02502) (Released in 2020.10.06.)
- [OpenReview - ICLR](https://openreview.net/forum?id=St1giarCHLP)

### 확률적 역과정을 암시적 모델로 근사

- 기존 DDPM은 reverse process의 조건부 분포 $p_\theta(x_{t-1} \vert x_t)$를 명시적으로 정의하며 계산 비용이 큼
- Score Function을 기반으로 reverse process의 implicit parameterization을 제안하여 샘플링 효율을 개선
- noise prediction 대신 직접 $x_0$을 예측하고, 이를 통해 reverse 조건부 분포를 구성
- 샘플링은 DDIM 공식에 따라 deterministic하게 수행되며, fewer steps로 빠르게 고품질 샘플 생성 가능
- DDPM과 동일한 학습 절차를 유지하면서 inference time만 효율화한 구조
- Diffusion Model의 품질과 속도 간 균형을 이루는 핵심 기법으로, 이후 다양한 hybrid 모델에 응용됨

---

## 2023 — Flow Matching (Deterministic, Continuous Time)

### Flow Matching for Generative Modeling

- Yaron Lipman, Ricky T. Q. Chen, Heli Ben-Hamu, Maximilian Nickel, and Matt Le
- ICLR 2023
- 1,400++ citations
- [arXiv](https://arxiv.org/abs/2210.02747) (Released in 2022.10.06.)
- [OpenReview - ICLR](https://openreview.net/forum?id=PqvMRDCJT9t)
- [NeurIPS - Tutorial](https://neurips.cc/virtual/2024/tutorial/99531)

### Continuous-time Deterministic 생성 흐름 정합

- 기존 score-based 및 diffusion 모델은 stochastic 샘플링과 느린 reverse process가 한계
- 본 논문은 초기 분포 $p_0(x)$에서 데이터 분포 $p_1(x)$로의 deterministic 경로를 정의하는 vector field 학습을 제안
- optimal transport의 Continuous Normalizing Flow를 기반으로 하며, 학습 목표는 흐름 벡터 $v_\theta(x, t)$가 다음 조건을 만족하도록 학습하는 것:

  $$
  v_\theta(x, t) \approx \nabla_x \log p_t(x) - \nabla_x \log \pi_t(x)
  $$

- 손실 함수는 flow matching loss로 정의되며, closed-form noise sampling과 빠른 deterministic 샘플링 가능
- diffusion의 느린 샘플링과 score 기반 학습의 어려움을 해소하며, ODE 기반 생성 모델의 새로운 패러다임 제시
