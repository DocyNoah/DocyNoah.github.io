---
title: git 날짜 및 시간 변경하기
description: git commit의 날짜와 시간을 변경하는 다양한 방법과 주의사항
author: yohan
categories: [Dev]
tags: [git, cmd]
---

Git에서 커밋의 날짜와 시간을 변경하는 방법에 대해 알아보겠습니다. 이 기능은 주로 다음과 같은 상황에서 유용합니다:

- 과거의 작업을 현재에 커밋할 때
- 커밋 히스토리를 정리할 때
- 실수로 잘못된 시간에 커밋했을 때

## 1. 새로운 커밋 생성하기

### 1.1 기본 커밋

가장 기본적인 커밋 방법입니다. 현재 시간이 자동으로 적용됩니다.

```bash
$ git commit -m "커밋 메시지"
```

### 1.2 상대적 시간으로 커밋

`--date` 옵션을 사용하여 상대적인 시간을 지정할 수 있습니다.

```bash
# 1일 전
$ git commit --date "1 day ago" -m "커밋 메시지"

# 2시간 전
$ git commit --date "2 hours ago" -m "커밋 메시지"

# 1주일 전
$ git commit --date "1 week ago" -m "커밋 메시지"
```

### 1.3 특정 날짜와 시간으로 커밋

정확한 날짜와 시간을 지정하여 커밋할 수 있습니다.

```bash
# 한국 시간대(KST) 기준
$ git commit --date "Mon 25 Dec 2023 10:10:35 KST" -m "커밋 메시지"

# UTC 기준
$ git commit --date "Mon 25 Dec 2023 01:10:35 UTC" -m "커밋 메시지"
```

## 2. 기존 커밋 수정하기

### 2.1 가장 최근 커밋 수정

`--amend` 옵션을 사용하여 가장 최근 커밋을 수정할 수 있습니다.

```bash
# 현재 시간으로 수정
$ git commit --amend --no-edit

# 커밋 메시지도 함께 수정
$ git commit --amend -m "새로운 커밋 메시지"
```

### 2.2 최근 커밋의 날짜/시간 수정

`--amend`와 `--date` 옵션을 함께 사용하여 최근 커밋의 날짜와 시간을 수정할 수 있습니다.

```bash
# 1일 전 시간으로 수정
$ git commit --amend --no-edit --date "1 day ago"

# 특정 시간으로 수정
$ git commit --amend --no-edit --date "Mon 25 Dec 2023 10:10:35 KST"
```

## 3. 작성자 날짜 변경하기

Git 커밋에는 두 가지 날짜가 있습니다:

- `AuthorDate`: 코드를 작성한 시점의 날짜
- `CommitDate`: 커밋을 생성한 시점의 날짜

### 3.1 새로운 커밋의 작성자 날짜 변경

```bash
# 작성자 날짜만 변경
$ git commit --date="Mon 25 Dec 2023 10:10:35 KST" -m "커밋 메시지"

# 작성자 날짜와 커밋 날짜 모두 변경
$ GIT_AUTHOR_DATE="Mon 25 Dec 2023 10:10:35 KST" git commit -m "커밋 메시지"
```

### 3.2 기존 커밋의 작성자 날짜 변경

```bash
# 가장 최근 커밋의 작성자 날짜 변경
$ git commit --amend --no-edit --date="Mon 25 Dec 2023 10:10:35 KST"

# 환경 변수를 사용하여 작성자 날짜 변경
$ GIT_AUTHOR_DATE="Mon 25 Dec 2023 10:10:35 KST" git commit --amend --no-edit
```

### 3.3 여러 커밋의 작성자 날짜 변경

여러 커밋의 작성자 날짜를 변경하려면 `git rebase`를 사용해야 합니다:

```bash
# 최근 3개의 커밋을 대화형으로 수정
$ git rebase -i HEAD~3

# 각 커밋에서 다음 명령어 실행
$ git commit --amend --no-edit --date="Mon 25 Dec 2023 10:10:35 KST"
$ git rebase --continue
```

### 3.4 작성자 날짜 확인하기

```bash
# 상세한 커밋 정보 확인
$ git log --pretty=fuller

# 특정 커밋의 상세 정보 확인
$ git show --pretty=fuller <commit-hash>
```

## 주의사항

1. 이미 원격 저장소에 푸시된 커밋의 날짜를 변경하면 히스토리가 꼬일 수 있습니다.
2. 팀 프로젝트에서는 커밋 날짜 변경을 신중하게 결정해야 합니다.
3. `--amend`는 가장 최근 커밋에만 적용됩니다.
4. 날짜 형식은 시스템의 로케일 설정에 따라 다를 수 있습니다.

## 유용한 팁

- `git log --pretty=fuller` 명령어로 커밋의 작성자 날짜와 커밋 날짜를 모두 확인할 수 있습니다.
- 날짜 형식이 맞지 않을 경우 다음 형식들을 사용할 수 있습니다:
  ```bash
  # ISO 8601 형식
  git commit --date="2023-12-25 10:10:35 +0900" -m "커밋 메시지"

  # RFC 2822 형식
  git commit --date="Mon, 25 Dec 2023 10:10:35 +0900" -m "커밋 메시지"

  # Unix 타임스탬프
  git commit --date="@1703470235" -m "커밋 메시지"
  ```
- 여러 커밋의 날짜를 한 번에 변경하려면 `git rebase`를 사용해야 합니다.
- 날짜 형식에 문제가 있을 경우 `git commit --date="now"`를 사용하여 현재 시간을 적용할 수 있습니다.
