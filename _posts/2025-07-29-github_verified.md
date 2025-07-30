---
title: Github commit에 verified 표시하기
description: GitHub에서 SSH 키를 사용하여 커밋에 서명하고 verified 배지를 표시하는 방법
author: yohan
categories: [Dev]
tags: [github, verified, commit, ssh, signing]
math: true
---

GitHub에서 커밋을 push할 때 인증은 성공했지만 커밋에 verified 배지가 나타나지 않는 경우가 있다. 이는 인증과 서명이 별개의 기능이기 때문이다. 커밋에 verified 배지를 표시하려면 별도의 서명 설정이 필요하며, GPG 키 방식과 SSH 키 방식 중 더 간편하고 최신 방식인 SSH 키를 사용한 서명 방법을 설명한다.

## 요약

1. ssh 공개키를 github에 signing key로 등록
2. git config에서 서명 활성화
   ```bash
   git config --global gpg.format ssh
   git config --global user.signingkey ~/.ssh/id_ed25519.pub
   git config --global commit.gpgsign true
   ```
   `id_ed25519`는 기본 키 이름이므로 실제 키 이름으로 변경 필요
3. 커밋 시 자동으로 서명되어 github에 verified 배지 표시

## 0. Git 버전 확인

SSH 키를 통한 커밋 서명은 **Git 2.34.0 이상**에서만 지원됨. 버전이 낮다면 업데이트 필요.

현재 Git 버전 확인:

```bash
git --version
```

> Git 2.34.0은 2021년 11월에 릴리스되었으므로 대부분의 최신 환경에서는 지원됨
{: .prompt-info }

## 1. SSH 서명 키 등록

### 1.1 기존 SSH 키 확인

현재 사용 중인 SSH 키 확인:

```bash
ls -la ~/.ssh/
```

기존 SSH 키가 있다면 해당 키를 서명용으로도 사용 가능

### 1.2 SSH 키 생성 (없는 경우)

SSH 키가 없거나 새로 생성하려면:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

> ED25519 알고리즘은 RSA보다 안전하고 빠르므로 권장됨
{: .prompt-tip }

### 1.3 GitHub에 서명용 SSH 키 등록

1. GitHub 웹사이트 접속
2. <kbd>Settings</kbd> > <kbd>SSH and GPG keys</kbd> 이동
3. <kbd>New SSH key</kbd> 클릭
4. <kbd>Key type</kbd>을 <kbd>Signing Key</kbd>로 선택 (중요)
5. 키 정보 입력 및 등록
   - <kbd>Title</kbd>: 구분을 위한 이름
   - <kbd>Key</kbd>: 공개키 내용 붙여넣기
     ```bash
     cat ~/.ssh/id_ed25519.pub
     ```

> Authentication key와 Signing key는 별도로 관리됨.
> 같은 SSH 키를 두 용도로 모두 등록 가능
{: .prompt-tip }

## 2. Git 서명 설정

### 2.1 서명 형식 설정

SSH 키를 사용한 서명 활성화:

```bash
git config --global gpg.format ssh
```

### 2.2 서명 키 지정

사용할 SSH 키 지정:

```bash
git config --global user.signingkey ~/.ssh/id_ed25519.pub
```

`id_ed25519`는 기본 키 이름이므로 실제 키 이름으로 변경 필요.

### 2.3 자동 서명 활성화

모든 커밋에 자동으로 서명 적용:

```bash
git config --global commit.gpgsign true
```

### 2.4 서명 설정 확인

현재 Git 서명 설정 확인:

```bash
git config --list | grep -E "(gpg|sign)"
```

출력 예시:
```plaintext
gpg.format=ssh
user.signingkey=/home/user/.ssh/id_ed25519.pub
commit.gpgsign=true
```

---

## 키 타입 구분

- **Authentication Key**: Git 저장소에 접근하기 위한 인증용 키
- **Signing Key**: 커밋에 서명하기 위한 키
- 같은 SSH 키를 두 용도로 모두 사용 가능하지만 GitHub에 각각 등록 필요

## References

- [GitHub SSH Commit Signature Verification](https://docs.github.com/ko/authentication/managing-commit-signature-verification/about-commit-signature-verification#ssh-commit-signature-verification)
