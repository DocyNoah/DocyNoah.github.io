---
title: Ubuntu 시스템의 하드웨어 사양 확인하기
description: Ubuntu 하드웨어 스펙 확인 방법 - CPU, 메모리, GPU, 디스크 등
author: yohan
categories: [Dev]
tags: [ubuntu, hardware, spec, cmd, linux]
---

## 1. 시스템 전체 정보

전체 하드웨어 정보를 한 번에 확인하려면:

```bash
sudo lshw
```

간단한 요약 정보만 보려면:

```bash
sudo lshw -short
```

## 2. CPU 정보

### 2.1 CPU 상세 정보 확인

```bash
lscpu
```

이 명령어는 CPU 아키텍처, 코어 수, 스레드 수, 캐시 크기 등 상세 정보를 보여줍니다.

### 2.2 프로세서 정보 파일 확인

```bash
cat /proc/cpuinfo
```

각 CPU 코어별 상세 정보를 확인할 수 있습니다.

### 2.3 CPU 코어 수 확인

```bash
grep -c processor /proc/cpuinfo
```
시스템의 총 CPU 코어 수를 보여줍니다.

## 3. 메모리(RAM) 정보

### 3.1 메모리 사용량 실시간 확인

```bash
free -h
```

### 3.2 상세 메모리 정보

```bash
sudo dmidecode --type memory
```

## 4. GPU 정보

### 4.1 NVIDIA GPU 정보

```bash
nvidia-smi
```

NVIDIA GPU의 상세 정보와 현재 사용량을 확인할 수 있습니다.

### 4.2 NVIDIA GPU 모델명 확인

```bash
nvidia-smi --query | fgrep 'Product Name'
```

### 4.3 통합/기타 GPU

```bash
lspci | grep -i vga
```

## 5. 디스크 정보

### 5.1 디스크 사용량

```bash
df -h
```

### 5.2 디스크 정보 상세 확인

```bash
sudo fdisk -l
```

## 6. 네트워크 장치 정보

```bash
ip addr show
```
