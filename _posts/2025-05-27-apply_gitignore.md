---
title: .gitignore 파일 변경사항 적용하기
description: Git에서 이미 추적 중인 파일들에 대해 새로운 .gitignore 규칙을 적용하는 방법
author: yohan
categories: [Dev]
tags: [git, gitignore, cmd]
---

## 문제 상황

`.gitignore` 파일을 새로 만들거나 수정했을 때 이미 Git에 추적되고 있는 파일들에는 변경사항이 적용되지 않는 경우가 있다. 이는 Git이 이미 추적 중인 파일들에 대해서는 `.gitignore` 규칙을 자동으로 적용하지 않기 때문이다.

## 해결 방법

Git 캐시 삭제 후 모든 파일 재추가로 새로운 `.gitignore` 규칙 적용

```bash
# Git의 캐시를 모두 삭제
git rm -r --cached .

# 모든 파일을 다시 추가
git add .

# 변경사항을 커밋
git commit -m "Apply .gitignore changes"
```

## 명령어 설명

- `git rm -r --cached .`
  - `rm`: 파일 삭제 명령어
  - `-r`: 재귀적으로 하위 디렉토리까지 모두 처리
  - `--cached`: Git 캐시에서만 삭제하고 실제 파일은 유지
  - `.`: 현재 디렉토리의 모든 파일을 대상으로 함

## 참고 사항

- Git 저장소의 모든 캐시를 지우고 다시 추가하는 작업으로, 변경사항이 많은 경우 커밋 크기가 커질 수 있음
- 작업 전 현재 변경사항을 모두 커밋하거나 스태시(stash)로 보관 권장
- 팀 프로젝트의 경우 변경사항을 팀원들과 사전 공유 필요
