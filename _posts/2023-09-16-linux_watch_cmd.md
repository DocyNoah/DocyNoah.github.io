---
title: Linux watch 명령어 가이드
description: Linux watch 명령어의 기본 사용법부터 고급 옵션까지, 시스템 모니터링에 활용하는 실용적인 가이드
author: yohan
categories: [Dev]
tags: [linux, watch, cmd]
---

## 기본 사용법

```bash
watch COMMAND
```

기본적으로 `watch`는 지정된 명령어를 2초마다 실행하여 그 결과를 화면에 출력

---

## 1. 주요 옵션

### -d, --differences

```bash
watch -d COMMAND
```

- 이전 출력과 현재 출력의 차이점을 하이라이트하여 표시
- 변경된 부분을 더 쉽게 파악할 수 있음

### -n, --interval

```bash
watch -n SECONDS COMMAND
```

- 명령어 실행 간격을 초 단위로 지정
- 기본값은 2초
- 0.1초 단위까지 설정 가능

### -t, --no-title

```bash
watch -t COMMAND
```

- 상단의 헤더(시간, 명령어 정보)를 숨김

### -b, --beep

```bash
watch -b COMMAND
```

- 명령어가 0이 아닌 종료 코드를 반환할 때 비프음 발생

---

## 2. 실제 사용 예시

### GPU 모니터링

```bash
watch -d -n 1 nvidia-smi
```

- NVIDIA GPU의 상태를 1초마다 모니터링
- 변경사항이 있을 때마다 하이라이트

### 시스템 리소스 모니터링

```bash
watch -n 1 'free -h'
```

- 메모리 사용량을 1초마다 확인

### 디스크 사용량 모니터링

```bash
watch -d 'df -h'
```

- 디스크 사용량을 모니터링하며 변경사항 하이라이트

### 네트워크 연결 상태 확인

```bash
watch -n 1 'netstat -tuln'
```

- 네트워크 연결 상태를 1초마다 확인

---

## 3. 팁과 주의사항

1. 너무 짧은 간격(예: 0.1초)으로 설정하면 시스템에 부하가 발생할 수 있습니다.
2. `Ctrl + C`를 눌러 watch 명령어를 종료할 수 있습니다.
3. `Ctrl + L`을 눌러 화면을 새로고침할 수 있습니다.
4. 출력이 너무 길어질 경우 `-p` 옵션을 사용하여 정확한 위치에 출력할 수 있습니다.

---

## 4. 관련 명령어

- `top`: 시스템 프로세스 모니터링
- `htop`: 향상된 시스템 모니터링 도구
- `vmstat`: 가상 메모리 통계 확인
- `iostat`: CPU 및 디스크 I/O 통계 확인
