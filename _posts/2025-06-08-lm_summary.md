---
title: Language Models 정리
description: OpenAI, Anthropic, Google, Meta, Mistral, Alibaba, NVIDIA 등 주요 기업이 발표한 최신 인공지능 모델부터 온디바이스 모델, VLA까지 정리
author: yohan
categories: [LLM]
tags: [LLM, VLA, Open-source, On-device]
math: true
---

## Closed-source Models

### OpenAI: GPT-4o

- 공개 일자: 2024‑05‑13
- 성능/용도: GPT-4급 멀티모달 대응 범용 모델로 실시간 음성·텍스트·이미지 처리에 최적화됨
- 모델 공개 여부: X
- Checkpoint 공개 여부: X
- 파라미터 수: 200B (추정), MoE 기반 구조로 활성 파라미터는 이보다 적음
- 특이사항: 128K 토큰 컨텍스트, 무료·Plus 사용자 모두 사용 가능, 후속 버전인 GPT‑4o mini 등장

### OpenAI: GPT-4.1

- 공개 일자: 2025‑04‑14
- 성능/용도: GPT‑4급 오버all 성능 향상, 1백만 토큰 컨텍스트, 코딩·추론·다국어 작동 빠르고 안정적으로 처리함
- 모델 공개 여부: X
- Checkpoint 공개 여부: X
- 파라미터 수: 1.8T (추정)
- 특이사항: mini/nano 버전 포함, SWE‑Bench 등 코딩 벤치에서 GPT‑4o보다 40% 빠르고 80% 저렴

### OpenAI: GPT-4.5

- 공개 일자: 2025‑02‑27
- 성능/용도: “거대·전문가급” 모델로 환각률 감소 및 패턴 인식 향상, 창작·추론 유연성 강화
- 모델 공개 여부: X
- Checkpoint 공개 여부: X
- 파라미터 수: 5~12T (추정)
- 특이사항: 2025년 중순 API 단계적 철수 예정, 실험적 기능 중심 사용됨

### OpenAI: GPT-o3

- 공개 일자: 2025‑04‑16
- 성능/용도: 고정밀 추론·코딩·과학 문제 해결에 최적화된 범용 모델
- 모델 공개 여부: X
- Checkpoint 공개 여부: X
- 파라미터 수: 200B (추정)
- 특이사항: 200K 컨텍스트, chain-of-thought 강화 학습 기반

### OpenAI: GPT-o4‑mini

- 공개 일자: 2025‑04‑16
- 성능/용도: 경량 reasoning 모델로 이미지 포함 수리·코딩 작업에 강함
- 모델 공개 여부: X
- Checkpoint 공개 여부: X
- 파라미터 수: 수십 B (추정)
- 특이사항: AIME 2025에서 99.5% pass@1 달성, o3 대비 빠르며 비용 효율적

### Anthropic: Claude Opus 4

- 공개 일자: 2025‑05‑22
- 성능/용도: 엔터프라이즈급 코딩·추론·장기워크플로우에 최적화된 최고급 모델
- 모델 공개 여부: X
- Checkpoint 공개 여부: X
- 파라미터 수: 수백 B~1T (추정)
- 특이사항: SWE‑bench 72.5%로 GPT‑4.1(54.6%) 훌쩍 넘으며, 7시간 연속 작업 지속 가능

### Anthropic: Claude Sonnet 4

- 공개 일자: 2025‑05‑22
- 성능/용도: 고성능+고속 균형형 모델로 코드 생산, 데이터분석, 고객지원에 적합
- 모델 공개 여부: X
- Checkpoint 공개 여부: X
- 파라미터 수: 수십~수백 B (추정)

### Anthropic: Claude Haiku 3.5

- 공개 일자: 2024-10-22
- 성능/용도: 응답 속도 최적화된 경량 모델, 실시간 챗봇·라벨링·코드 보조에 특화
- 모델 공개 여부: X
- Checkpoint 공개 여부: X
- 파라미터 수: 수십 B (추정)
- 특이사항: 툴 사용, 툴링, 라벨링 등 속도∙비용 최적화 용도에 강함

### Google: Gemini 2.5 Pro

- 공개 일자: 2025‑03‑25
- 성능/용도: GPT‑4급 reasoning·코딩·멀티모달 처리를 Deep Think 모드와 100만 토큰 컨텍스트로 수행함
- 모델 공개 여부: X
- Checkpoint 공개 여부: X
- 파라미터 수: 수백 B~1T (추정)
- 특이사항: SWE‑Bench Verified 63.8%, Humanity's Last Exam 18.8%, MRCR co‑reference 91.5%, Deep Think 기능 지원

### Google: Gemini 2.5 Flash

- 공개 일자: 2025‑04‑17
- 성능/용도: 중저지연·저비용 환경에서 thinking budget 설정으로 균형 잡힌 reasoning·멀티모달 처리
- 모델 공개 여부: X
- Checkpoint 공개 여부: X
- 파라미터 수: 수십~수백 B (추정)
- 특이사항: 2.5 Flash는 가격 대비 지능 지표에서 우수하며, 24576 tokens thinking 지원

## Open-source Models

### Meta: LLaMA 3.3‑70B

- 공개 일자: 2024‑12‑06
- 성능/용도: 70B 파라미터로 GPT‑3.5~4 수준의 다국어 챗/코딩/요약 작업에 최적화됨
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 70B
- 특이사항: 128K 토큰 컨텍스트, 15T+ 토큰으로 사전학습, 다국어 지원(8+ 개 언어)

### Meta: LLaMA 4 Scout

- 공개 일자: 2025‑04‑05
- 성능/용도: 멀티모달 포함, 10M 토큰 컨텍스트로 대규모 문맥 지원하는 컴팩트 모델
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 총 109B (활성 17B)
- 특이사항: MoE 구조(16 experts), H100 GPU 단일 실행 가능

### Meta: LLaMA 4 Maverick

- 공개 일자: 2025‑04-05
- 성능/용도: GPT‑4o 수준의 코딩·추론 능력, 고효율 MoE 기반 멀티모달 모델
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 총 400B (활성 17B)
- 특이사항: 128 experts MoE, 경량화된 고성능 구조

### Mistral AI: Magistral Small

- 공개 일자: 2025‑06‑10
- 성능/용도: 추론 논리 중심의 reasoning 특화 모델
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 24B
- 특이사항: Apache 2.0 공개, Hugging Face 배포, MoE 아님

### Alibaba: Qwen3‑235B‑A22B (MoE)

- 공개 일자: 2025‑04‑29
- 성능/용도: 235B 총 파라미터, 22B 활성 MoE 구조로 복잡한 추론·코딩·다국어·툴 연동에 뛰어난 flagship 모델
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 총 235B, 활성 22B
- 특이사항: “thinking mode”/“non‑thinking mode” 전환, 100+ 언어 지원, agent툴 연동 최적화

### Alibaba: Qwen3‑30B‑A3B (MoE)

- 공개 일자: 2025‑04‑29
- 성능/용도: 30B 총 파라미터, 활성 3B MoE 구조로 복잡한 추론·코딩·다국어·Agent 작업에 적합
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 총 30B, 활성 3B
- 특이사항: thinking/non‑thinking 모드 전환, 128K 토큰 컨텍스트 지원, Qwen3 시리즈 중 속도와 성능 균형 우수, CPU/WG GPU에서도 가벼운 실행 가능

### Alibaba: Qwen3 Dense 시리즈

- 공개 일자: 2025‑04‑29
- 성능/용도: GPT‑3.5~4 수준 dense 아키텍처로, 스템 코딩·추론·멀티턴 대화·다국어 작업에 고르게 강함
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 0.6B, 1.7B, 4B, 8B, 14B, 32B
- 특이사항: 32B·14B·8B 모델은 128K 토큰 컨텍스트 지원, 4B·1.7B·0.6B는 32K 토큰; thinking/non‑thinking 모드 토글 가능; 오픈소스 챗/코딩/agent 작업에서 Qwen2.5보다 우수한 성능

### Alibaba: Qwen2.5‑Omni 시리즈

- 공개 일자: 2025‑03‑26
- 성능/용도: 이미지·음성·비디오·텍스트 입력 지원, 생성 가능한 멀티모달 인터랙션
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 3B, 7B

### Alibaba: Qwen2.5‑VL 시리즈 (멀티모달)

- 공개 일자: 2025‑01‑28
- 성능/용도: 이미지·텍스트 입력 통합, 정밀 객체 인식 및 JSON 출력, 문서·다이어그램 이해, 장시간 비디오 reasoning에 최적화됨
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 3B, 7B, 32B, 72B
- 특이사항:
  - 32B Instruct는 GPT‑4o mini/Mistral‑Small급 성능, multi-step reasoning 특화
  - bounding box/point 기반 object grounding, JSON 구조화 출력 지원
  - 장시간 동영상 처리, dynamic-FPS 및 mRoPE positional encoding 사용
  - 3B/7B 버전은 edge AI 및 GUI agent 활용 가능하며, Qwen2.5‑VL‑7B은 GPT‑4o‑mini보다 우수

### Alibaba: Qwen2.5‑1M 시리즈

- 공개 일자: 2025‑01‑27
- 성능/용도: 최대 1,000,000 토큰 장문 처리에 최적화되어 Passkey Retrieval, 문서 요약, 장기 대화 유지에 탁월하며 단문 성능도 유지됨
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 7B, 14B
- 특이사항: Dual Chunk Attention과 sparse attention으로 1M 토큰 컨텍스트 지원, vLLM 기반 inference 도구 함께 제공, 7B는 최소 120GB VRAM 필요, 14B는 320GB VRAM 권장

## On-device Models

### Google: Gemma 3

- 공개 일자: 2025‑03‑10
- 성능/용도: 멀티모달·다국어·128K 컨텍스트·function calling 지원 on-device 경량 LLM
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 1B, 4B, 12B, 27B
- 특이사항: 싱글 GPU·TPU 최적화, ShieldGemma 이미지 필터 내장, quantized 버전 지원

### Google: Gemma 3 Nano

- 공개 일자: 2025‑05‑22 (preview)
- 성능/용도: Per‑Layer Embeddings 기반 모바일 최적화 모델, 초경량 멀티모달 on-device LLM
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 5B, 8B (활성 2B, 4B)
- 특이사항: 저전력 환경 대응, Flutter SDK 및 MediaPipe 통합, 오디오·비디오 처리 예정

### Meta: MobileLLM

- 공개 일자: 2024‑02‑22 (ICML 2024 발표), weights 2024‑10‑31 공개
- 성능/용도: on-device common-sense reasoning, Q&A, 문서 이해 등 모바일 최적화 경량 아키텍처
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 125M, 350M, 600M, 1B, 1.5B
- 특이사항: SwiGLU, grouped-query attention, weight-sharing 등 경량화기술 채택, 125M/350M에서 sanity check 기준 +2.7%/+4.3% 향상

### Hugging Face: SmolVLM

- 공개 일자: 2024‑11‑26
- 성능/용도: 2B 파라미터로 이미지+텍스트 입력 처리, 이미지 캡션·비주얼 QA·멀티이미지 챗 등 on-device 및 에지 환경에 최적화됨
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 256M, 500M, 2B
- 특이사항: Idefics3 기반 비전 토큰 압축, video 프레임 처리 기능, VLM benchmarks에서 메모리 및 처리 효율 최상위

## Vision-Language-Action Models

### Google DeepMind: RT‑2

- 공개 일자: 2023‑07‑28
- 성능/용도: Vision–Language–Action (VLA) 모델로, 이미지와 자연어 명령을 받아 로봇의 동작(action)을 텍스트 토큰으로 직접 생성
- 모델 공개 여부: X
- Checkpoint 공개 여부: X
- 파라미터 수: PaLM‑E 기반 약 12B, PaLI‑X 기반 약 55B
- 특이사항: 웹 기반 시각·언어 사전학습과 로봇 동작 데이터 동시 fine-tuning 수행; 6,000개 실험에서 emergent reasoning 및 행동 제어 시연

### Google DeepMind: RT‑X (RT‑1‑X / RT‑2‑X)

- 공개 일자: 2023‑10‑03 (Open X‑Embodiment 발표 시점)
- 성능/용도: 로봇 비전 + 언어 기반 행동 생성 VLA 모델, 다양한 로봇들 간 지식 전이와 emergent skill 수행 가능
- 모델 공개 여부: O (연구용 공개)
- Checkpoint 공개 여부: O (RT‑1‑X 및 RT‑2‑X 일부 체크포인트 공개)
- 파라미터 수: RT‑1‑X ≈ 35M, RT‑2‑X ≈ 55B
- 특이사항:
  - Open X‑Embodiment 데이터셋(22개 로봇, 60개 데이터셋, 1M+ 에피소드) 공개
  - RT‑1‑X: 기존 RT‑1 대비 평균 50% 성공률 향상, 실험실 5곳 이상 검증
  - RT‑2‑X: emergent spatial reasoning 포함, 기존 RT‑2 대비 3배 성능 향상

### Physical Intelligence: π₀ (pi-zero)

- 공개 일자: 2024‑10‑31
- 성능/용도: Vision‑Language‑Action 모델로 다양한 로봇 플랫폼에서 dexterous task 수행 가능 (빨래 개기, 식사 정리 등)
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 약 3B (VLM) + 300M diffusion action 모듈
- 특이사항: flow-matching 기반 action chunking으로 최대 50Hz real-time 제어, 7개 플랫폼·68개 태스크 mix-training

### Physical Intelligence: π₀.₅ (pi-zero point five)

- 공개 일자: 2025‑04‑22
- 성능/용도: 개·신규 환경 대응 잘하는 general VLA, home assistant chores (청소, 물건 정리 등) 수행
- 모델 공개 여부: O
- Checkpoint 공개 여부: X (논문 발표 시점)
- 파라미터 수: 비공개 (VLM 기반의 action model 구조)
- 특이사항: 이종 robot 및 web video로 co-training, semantic prediction 포함하여 long-horizon generalization 달성

### NVIDIA: GR00T N1

- 공개 일자: 2025‑03‑18
- 성능/용도: Vision‑Language‑Action 모델로 humanoid robot 제어, simulation + real trajectory mix 훈련
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 2.2B
- 특이사항: dual-system architecture (System 2 reasoning + System 1 diffusion action), humanoid robot에 적용됨

### NVIDIA: GR00T N1.5

- 공개 일자: 2025‑06‑12
- 성능/용도: GR00T N1 업그레이드 버전으로 더 높은 language grounding 및 task generalization
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 3B (System) + action 모듈
- 특이사항: Eagle‑2.5 VLM frozen, FLARE + DreamGen 통한 synthetic trajectory training, 93% 언어 지시 정확도 개선

### Hugging Face: SmolVLA

- 공개 일자: 2025‑06‑02
- 성능/용도: 450M 크기의 경량 VLA로 시각+언어 기반 로봇 제어를 저전력 환경에서 수행 가능
- 모델 공개 여부: O
- Checkpoint 공개 여부: O
- 파라미터 수: 450M
- 특이사항: flow-matching 기반 행동 생성, consumer GPU/CPU에서 실시간 실행 가능, 23K 로봇 trajectory 데이터 기반 학습
