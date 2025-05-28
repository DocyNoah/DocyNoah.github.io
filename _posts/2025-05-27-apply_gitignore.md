---
title: .gitignore 파일 변경사항 적용하기
description: Git에서 이미 추적 중인 파일들에 대해 새로운 .gitignore 규칙을 적용하는 방법
author: yohan
categories: [Dev]
tags: [git, gitignore, cmd]
---

## 문제 상황

`.gitignore` 파일을 새로 만들거나 수정했는데 이미 Git에 추적되고 있는 파일들에는 변경사항이 적용되지 않는 경우가 있습니다. 이는 Git이 이미 추적 중인 파일들에 대해서는 `.gitignore` 규칙을 자동으로 적용하지 않기 때문입니다.

## 해결 방법

Git의 캐시를 삭제하고 모든 파일을 다시 추가하면 새로운 `.gitignore` 규칙이 적용됩니다.

```bash
# Git의 캐시를 모두 삭제합니다
git rm -r --cached .

# 모든 파일을 다시 추가합니다
git add .

# 변경사항을 커밋합니다
git commit -m "Apply .gitignore changes"
```

## 명령어 설명

- `git rm -r --cached .`
  - `rm`: 파일 삭제 명령어
  - `-r`: 재귀적으로 하위 디렉토리까지 모두 처리
  - `--cached`: Git 캐시에서만 삭제하고 실제 파일은 유지
  - `.`: 현재 디렉토리의 모든 파일을 대상으로 함

## 주의사항

1. 이 작업은 Git 저장소의 모든 캐시를 지우고 다시 추가하는 것이므로, 변경사항이 많은 경우 커밋 크기가 커질 수 있습니다.
2. 작업 전에 현재 변경사항을 모두 커밋하거나 스태시(stash)해두는 것이 좋습니다.
3. 팀 프로젝트의 경우, 이 변경사항을 팀원들에게 미리 공유하는 것이 좋습니다.

## Example

```bash
git rm -r --cached .
git add ...
git commit ...
```
