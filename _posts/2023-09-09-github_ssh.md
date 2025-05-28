---
title: ssh 키로 github 인증하기
description: GitHub SSH 키 생성부터 등록, HTTPS 포트를 통한 연결, 다중 키 관리까지 SSH 인증의 모든 것
author: yohan
categories: [Dev]
tags: [git, github, ssh]
---

## 1. SSH 키 생성 및 관리

### 1.1 SSH 키 생성하기

기본적인 SSH 키 생성:

```bash
$ ssh-keygen
```

권장하는 상세 옵션을 사용한 키 생성:

```bash
$ ssh-keygen -t ed25519 -C "your_email@example.com"
```

> RSA 대신 ED25519 권장. 더 안전하고 빠름.
{: .prompt-tip }

옵션 설명:

- `-t`: 키 타입 지정 (ed25519, rsa 등)
- `-b`: 키 길이 지정 (RSA의 경우 기본값 2048)
- `-C`: 주석 추가 (보통 이메일 주소 사용)

### 1.2 키 파일 위치

기본 저장 경로:

- 개인키: `/home/$USER_NAME/.ssh/id_ed25519`
- 공개키: `/home/$USER_NAME/.ssh/id_ed25519.pub`

### 1.3 암호 설정

- 암호 없이 사용: 엔터키 두 번 입력
- 암호 설정: 원하는 암호 입력 후 확인

---

## 2. GitHub에 SSH 키 등록하기

1. GitHub 웹사이트 접속
2. 우측 상단의 프로필 아이콘 클릭
3. `Settings` 메뉴 선택
4. 좌측 사이드바에서 `SSH and GPG keys` 선택
5. `New SSH key` 버튼 클릭
6. 키 정보 입력:
   - Title: 키 구분을 위한 이름 (예: "Personal MacBook")
   - Key: 공개키 내용 붙여넣기
   ```bash
   $ cat ~/.ssh/id_ed25519.pub
   ```

## 3. SSH 연결 테스트

기본 연결 테스트:

```bash
$ ssh -T git@github.com
```

상세 로그 확인:

```bash
$ ssh -vT git@github.com
```

성공 메시지:

```plaintext
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## 4. 방화벽 우회: HTTPS 포트로 SSH 사용하기

SSH 포트(22) 차단 시 HTTPS 포트(443)를 통한 SSH 연결 가능

### 4.1 SSH Config 설정

`~/.ssh/config` 파일 생성 또는 수정

```bash
Host github.com
    HostName ssh.github.com
    Port 443
    User git
```

> config 파일의 대소문자와 들여쓰기는 가독성을 위한 형식일 뿐, 기능에는 영향 없음
{: .prompt-tip }

### 4.2 연결 확인

설정 후 연결 테스트:

```bash
$ ssh -vT git@github.com
```

포트 443으로 연결되는 것 확인 가능

```plaintext
debug1: Connecting to ssh.github.com port 443.
```

---

## 5. 다중 SSH 키 관리하기

여러 GitHub 계정(회사/개인)을 구분하여 관리할 때 사용

### 5.1 키 파일 준비

각 계정별로 다른 이름의 키 파일 생성:

```bash
$ ssh-keygen -t ed25519 -f ~/.ssh/github_personal -C "personal@email.com"
$ ssh-keygen -t ed25519 -f ~/.ssh/github_work -C "work@email.com"
```

### 5.2 SSH Config 설정

`~/.ssh/config` 파일에 계정별 설정 추가:

```bash
# 개인 계정
Host github.com-personal
    HostName ssh.github.com
    Port 443
    User git
    IdentityFile ~/.ssh/github_personal

# 회사 계정
Host github.com-work
    HostName ssh.github.com
    Port 443
    User git
    IdentityFile ~/.ssh/github_work
```

### 5.3 저장소 클론 및 사용

개인 계정 저장소:

```bash
$ git clone git@github.com-personal:username/repo.git
```

회사 계정 저장소:

```bash
$ git clone git@github.com-work:company/repo.git
```

### 5.4 기존 저장소의 Remote URL 변경

```bash
$ git remote set-url origin git@github.com-personal:username/repo.git
```

---

## 6. 문제 해결

### 6.1 권한 문제

```bash
$ chmod 600 ~/.ssh/id_ed25519
$ chmod 644 ~/.ssh/id_ed25519.pub
```

### 6.2 SSH 에이전트 실행

```bash
$ eval "$(ssh-agent -s)"
$ ssh-add ~/.ssh/id_ed25519
```

### 6.3 연결 테스트

```bash
$ ssh -vT git@github.com
```

---

## References

- [GitHub SSH 키 가이드](https://docs.github.com/ko/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
- [SSH 연결 테스트](https://docs.github.com/ko/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection)
- [HTTPS 포트를 통한 SSH 사용](https://docs.github.com/ko/authentication/troubleshooting-ssh/using-ssh-over-the-https-port)
