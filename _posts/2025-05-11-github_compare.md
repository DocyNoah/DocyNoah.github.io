---
title: GitHub에서 두 커밋 간의 변경사항 비교하기
description: GitHub에서 커밋, 브랜치, 태그 간의 변경사항을 쉽게 비교하는 방법
author: yohan
categories: [Dev]
tags: [git, github, cmd]
---

## 1. GitHub Compare 기능 소개

GitHub의 Compare 기능 사용 시 다음 항목들 간의 변경사항 비교 가능

- 서로 다른 커밋
- 브랜치
- 태그
- 릴리스 버전

## 2. 비교 URL 형식

### 2.1 기본 형식

```bash
https://github.com/[username]/[repository]/compare/[base]...[compare]
```

- `[username]`: GitHub 사용자명 또는 조직명
- `[repository]`: 저장소 이름
- `[base]`: 비교의 기준이 되는 커밋/브랜치/태그
- `[compare]`: 비교 대상이 되는 커밋/브랜치/태그

### 2.2 주의사항

- `...`(점 3개)를 사용하면 두 지점의 차이를 비교
- `..`(점 2개)를 사용하면 직접적인 변경사항만 비교

## 3. 사용 예시

### 3.1 커밋 해시로 비교

stable-baseline3 v2.1.0에서 v2.2.0 사이의 변경사항 비교

```bash
https://github.com/DLR-RM/stable-baselines3/compare/f4ec0f6afa1a23b0e0b746174cd0074471cc0b89...e1eac844afd86e241f2bc1c06a2633e35e7e138e
```

### 3.2 브랜치 간 비교

```bash
https://github.com/[username]/[repository]/compare/main...develop
```

### 3.3 태그 간 비교

```bash
https://github.com/[username]/[repository]/compare/v1.0.0...v2.0.0
```

## 4. 유용한 팁

### 4.1 시간 범위로 비교하기

특정 기간의 변경사항 확인 가능

```bash
https://github.com/[username]/[repository]/compare/main@{1.month.ago}...main
```

### 4.2 포크된 저장소와 비교하기

```bash
https://github.com/[username]/[repository]/compare/main...username:feature
```
