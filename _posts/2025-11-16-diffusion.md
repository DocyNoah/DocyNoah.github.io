---
title: Diffusion Model을 여행하는 히치하이커를 위한 안내서 1편 - VAE
description: 
author: yohan
categories: [Draft]
tags: [diffusion, generative model, probabilistic model]
math: true
---

본 글은 VAE, Diffusion Model부터 Flow Matching과 Shortcut Model까지 확률 기반 생성 모델을 수학적으로 제대로 이해하기 위한 글로 긴 여정이 될 것으로 보인다.

우선 Diffusion Model을 공부하기 위해 무작정 Denoising Diffusion Probabilistic Models 논문을 보면 본문도 아닌 Background에서부터 다음과 같은 수식들이 나와 머리가 아파온다.

$$
p_{\theta}(\mathbf{x}_{0:T})
:= p(\mathbf{x}_T)\prod_{t=1}^{T} p_{\theta}(\mathbf{x}_{t-1}\mid \mathbf{x}_t),
\qquad
p_{\theta}(\mathbf{x}_{t-1}\mid \mathbf{x}_{t})
:= \mathcal{N}\!\left(\mathbf{x}_{t-1};\, \mu_{\theta}(\mathbf{x}_{t}, t),\, \Sigma_{\theta}(\mathbf{x}_{t}, t)\right)
$$

문제는 이게 Background라는 것이고 DDPM 논문은 Diffusion Model을 제안하는 것이 아니라 이미 존재하던 Diffusion Model을 개선한 논문이라는 점이다. 즉, 이 수식들을 당연히 아는 것으로 전제하고 시작한다는 것이다.

그렇다면 Diffusion Model의 기초부터 차근차근 쌓아올라가야 한다. 이 여정은 다음과 같은 순서로 진행될 것이다:

1. **확률 이론의 기초**: 확률 분포, 조건부 확률, Bayes' theorem 등
2. **Variational Autoencoder (VAE)**: latent variable model의 시작
3. **Diffusion Model의 기초**: forward process와 reverse process
4. **DDPM (Denoising Diffusion Probabilistic Models)**: 실용적인 diffusion model
5. **Score-based Models**: diffusion의 또 다른 관점
6. **Flow Matching**: continuous normalizing flows
7. **Shortcut Models**: 최신 기법들

사실 위 순서는 LLM이 작성해 준거고 순서 같은 거는 없다.
생각나는대로 진행할 거다.

확률 모델을 공부하기에 가장 만만한 게 VAE이니까 Diffusion Model을 보기 전에 먼저 VAE부터 살펴본다.

## Variational Autoencoder (VAE)

VAE 논문의 제목은 `Auto-Encoding Variational Bayes`로 2013년 12월에 처음으로 arXiv에 공개되었다.

VAE를 알려면 VAE의 목적을 먼저 알아야 한다.

VAE는 다음과 같은 목적에서 고안되었다.

어떤 데이터가 있을 때, 이 데이터들은 나름의 어떤 규칙을 가지고 있다고 생각할 수 있다. 그러면 그 규칙을 파악해서 수학적으로 잘 표현하여 **확률 분포를 만들면 이 확률 분포에서 새로운 데이터를 생성할 수 있을 것이다.**
하지만 단순히 likelihood를 최대화하는 것으로는 데이터를 모두 설명할 수 없다.
실제 데이터는 비선형적이고 가우시안 분포로는 표현하기 어려운 형태이고 매우 고차원 데이터이기 때문이다.

예를 들어 $x$가 고차원 이미지라면

- 픽셀 간 상관관계
- 구조, 형태, 질감, 조명
- 사람 사진이라면 포즈, 표정, 감정, 각도 등

너무 많은 요소가 있어서 확률 분포 $p_{\theta}(x)$를 직접 모델링하기 어려울 것이다.

그래서 등장하는 고전적인 아이디어가 잠재 변수(latent variable)를 도입하는 것이다.
잠재 변수 $z$를 도입하면 데이터 $x$의 확률 분포 $p_{\theta}(x)$를 다음과 같이 표현할 수 있다.

$$
p_{\theta}(x) = \int p_{\theta}(x \vert z) p(z) dz
$$

- $p_{\theta}(x)$는 데이터 $x$의 확률 분포
- $p_{\theta}(x \vert z)$는 잠재 변수 $z$를 조건으로 하는 $x$의 확률 분포
- $p(z)$는 잠재 변수 $z$의 확률 분포

(위 수식을 유식하게 말하면 $z$를 marginalization하여 얻은 $x$의 marginal likelihood를 표현한 것이다.)

여기에서 잠재 변수란 말 그대로 데이터 $x$의 본질적이고 함축적이고 추상적인 표현이라고 할 수 있다.
잠재 변수 $z$로 데이터 $x$를 설명하자면 어떤 함축적이고 추상적인 의미 $z$를 시각화한 것이 $x$가 되는 것이다.
어떻게 보면 $x$가 사진이나 풍경이 되고 $z$가 인상이나 느낌, 기억(기억이 사진으로 저장되지는 않으니)이라고 볼 수도 있겠다.

잠재 변수 $z$의 확률 분포 $p(z)$는 $p_{\theta}(x)$와 달리 매우 단순한 형태의 확률 분포가 될 수 있다.
이는 우리가 직접 설정할 수도 있는데 가장 단순하고 만만한 가우시안 분포로 설정하며 그만이다.
그리고 잠재 변수 $z$에 기반한 데이터 $x$의 확률 분포 $p_{\theta}(x \vert z)$는 $p_{\theta}(x)$에 비해 모델링하기 용이하다.
단순히 엄청난 다양성과 복잡성을 갖고 있는 $x$를 전부 아우르는 $p_{\theta}(x)$를 모델링하기는 어렵지만, 특정 잠재 변수가 주어진 상태에서의 $x$의 확률 분포 $p_{\theta}(x \vert z)$는 특정 잠재 변수에 대한 국소적인 확률 분포이므로 모델링하기 매우 용이하다.

그리하여 표현하기 어려운 복잡한 $x$를 바로 생성하지 말고, 먼저 잠재 변수 $z$를 찾고(샘플링하고) 그 잠재 변수 $z$를 이용해 $x$를 생성하는 것이 VAE의 기본 아이디어이다.

즉,

1. 먼저 잠재 변수 $z$를 샘플링한다.
2. 그 잠재 변수 $z$를 이용해 $x$를 생성한다.

$$
p_{\theta}(x) = \int p_{\theta}(x \vert z) p(z) dz
$$

가 완성되는 것이다.

$p_{\theta}(x) = \int p_{\theta}(x \vert z) p(z) dz$
에서 $p_{\theta}(x \vert z)$를 모델링하는 것은 직관적이고 $p(z)$는 가우시안 분포로 설정하면 된다.

그런데 $p_{\theta}(z)$를 단순히 가우시안 분포로 두고 $z$를 샘플링하면 $p_{\theta}(x \vert z)$는 잠재 변수 $z$에서 데이터 $x$를 생성하는 것이 아니라 그냥 노이즈 $z$를 보고 데이터 $x$를 생성하는 모습이 되니 잠재 변수 $z$의 의미를 잃어버리게 된다.

$p(z)$를 가우시안 분포로 설정하더라도 잠재 변수로써의 의미를 가지기 위해 데이터 $x$를 가우시안 분포 $p(z)$로 모델링하는 posterior $p(z \vert x)$를 모델링하는 것이 필요하다.

다시 말해, 추론할 때는 가우시안 분포에서 샘플링한 노이즈 $z$를 $p_{\theta}(x \vert z)$에 넣어서 데이터를 생성할 수 있지만 학습할 때는 $z$가 잠재 변수로써의 역할을 해야하니 $p_{\theta}(z \vert x)$애서 샘플링돼야 하는 것이다.

그런데 다시 문제가 생기는 게 $p_{\theta}(z \vert x)$도 결국 $z$를 출력으로 하기 때문에 데이터 $x$가 가지는 잠재 변수 $z$를 알아야 이를 정답으로 학습할 수 있다는 것이다.

$p_{\theta}(z \vert x)$가 무엇을 따라야 하는지는 사실 확률 분포의 수학적 일관성을 유지하는 과정에서 자연스럽게 결정되는데 잠재 변수 $z$를 도입하는 과정에서 다음 수식이 성립해야만 한다.

$$
p_{\theta}(z \vert x) = \frac{p_{\theta}(x \vert z) p(z)}{p_{\theta}(x)}
$$

이 수식을 Bayes' theorem을 이용하여 유도할 수 있다.
사실 별 건 아니고 다음 수식으로 직관적으로 쉽게 유도될 수 있다.

$$
p(x, z) = p_{\theta}(x \vert z) p(z) = p_{\theta}(z \vert x) p(x)
$$

위 Bayes' theorem 수식을 보니 $p_{\theta}(x)$를 모델링하기 위해 고군분투 헤쳐왔건만 다시 분모에 $p_{\theta}(x)$가 나타나는 것을 보니 무언가 잘못된 것 같다.

안되겠다. 구할 수 없는 posterior $p_{\theta}(z \vert x)$ 말고 근사 posterior $q_{\phi}(z \vert x)$를 모델링하고 이를 posterior $p_{\theta}(z \vert x)$로 근사한다. 즉, $q_{\phi}(z \vert x) \approx p_{\theta}(z \vert x)$으로 $\text{KL}(q_{\phi}(z \vert x) \Vert p_{\theta}(z \vert x)) \to 0$이 되도록 한다.

그런데 posterior $p_{\theta}(z \vert x)$를 구할 수 없다면서 $\text{KL}(q_{\phi}(z \vert x) \Vert p_{\theta}(z \vert x))$는 어떻게 구하는 걸까? 여기에서 등장하는 게 ELBO(Evidence Lower BOund)이다.

...

### VAE 요약

요약하면 VAE는 다음과 같은 사고 과정을 거쳐 설계되었다.

1. 데이터 $x$의 확률 분포 $p_{\theta}(x)$를 모델링하여 데이터를 생성해내자!
2. $p_{\theta}(x)$를 모델링하기 어려우니 잠재 변수 $z$를 도입하여 $p_{\theta}(x)$를 $\int p_{\theta}(x \vert z) p(z) dz$로 모델링하자!
3. $p(z)$는 잠재 변수로써 의미를 가지기 위해 posterior $p_{\theta}(z \vert x)$를 모델링하자!
4. $p_{\theta}(z \vert x)$은 $\frac{p_{\theta}(x \vert z) p(z)}{p_{\theta}(x)}$을 따르도록 하자!
5. posterior를 구하는 과정에서 $p_{\theta}(x)$가 나오니 근사 posterior $q_{\phi}(z \vert x)$를 모델링하자!
