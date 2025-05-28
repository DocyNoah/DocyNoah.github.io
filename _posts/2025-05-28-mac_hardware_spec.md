---
title: Mac 시스템의 하드웨어 사양 확인하기
description: 터미널에서 CPU, 메모리, 저장장치, GPU 등 Mac 하드웨어 사양을 확인하는 다양한 명령어 모음
author: yohan
categories: [Dev]
tags: [mac, hardware, spec, cmd]
---

## CPU 정보

물리적 CPU 코어 수 및 논리적 CPU 코어 수 확인

```bash
sysctl hw.physicalcpu hw.logicalcpu
```

실행 결과:

```plaintext
hw.physicalcpu: 8
hw.logicalcpu: 16
```

CPU 모델명 및 상세 정보 확인:

```bash
sysctl -n machdep.cpu.brand_string
```

## 메모리 정보

전체 메모리 용량 및 현재 사용량 확인:

```bash
# 전체 메모리 용량 확인
sysctl hw.memsize

# 상세 메모리 사용량 확인
vm_stat
```

## 저장장치 정보

디스크 용량 및 사용량 확인:

```bash
# 디스크 사용량 확인
df -h

# 디스크 정보 상세 보기
diskutil list
```

## GPU 정보

그래픽 카드 정보 확인:

```bash
system_profiler SPDisplaysDataType
```

## 전체 시스템 정보

시스템 전반적인 하드웨어 정보 확인:

```bash
system_profiler SPHardwareDataType
```
