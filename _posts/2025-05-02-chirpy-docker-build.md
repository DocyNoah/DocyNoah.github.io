---
title: Chirpy Theme Docker Build
description: VS Code Dev Containers를 활용한 Chirpy 테마 개발 환경 구성 가이드
author: yohan
categories: [Blogging, Tutorial]
tags: [jekyll, chirpy, blogging, docker, vscode, tutorial]
---

VS Code의 Dev Containers는 Docker를 활용하여 개발 도구와 설정을 격리된 컨테이너 안에 구성할 수 있는 강력한 도구이다.
이를 통해 로컬 시스템에 Ruby, Node.js, Jekyll 등을 직접 설치하지 않고도 즉시 개발을 시작할 수 있으며, 환경 충돌 없이 일관된 개발 환경을 구축할 수 있다.

---

## 1. 사전 설치 항목

- Docker
  - Windows/macOS: Docker Desktop
  - Linux: Docker Engine
- Visual Studio Code
- VS Code Extension: Dev Containers

---

## 2. Dev Container 구성

위치: `.devcontainer/devcontainer.json`

### 2.1 기본 설정

```json
{
  "name": "Jekyll",
  "image": "mcr.microsoft.com/devcontainers/jekyll:2-bullseye",
  "onCreateCommand": "git config --global --add safe.directory ${containerWorkspaceFolder}",
  "postCreateCommand": "bash .devcontainer/post-create.sh",
  "customizations": {},
}
```

- `image`: Jekyll이 사전 설치된 공식 Docker 이미지
- `onCreateCommand`:컨테이너가 처음 만들어질 때 실행되는 명령, Git 경고 방지용 디렉토리 등록
- `postCreateCommand`: 컨테이너 생성 직후 실행되는 명령

### 2.2 VS Code Extension 자동 설치 구성

```json
{
  "customizations": {
    "vscode": {
      "settings": {
        "terminal.integrated.defaultProfile.linux": "zsh"
      },
      "extensions": [
        "killalau.vscode-liquid-snippets",
        "Shopify.theme-check-vscode",
        "timonwong.shellcheck",
        "mkhl.shfmt",
        "EditorConfig.EditorConfig",
        "esbenp.prettier-vscode",
        "stylelint.vscode-stylelint",
        "yzhang.markdown-all-in-one",
        "mhutchie.git-graph"
      ]
    }
  }
}
```

- Liquid 템플릿 자동완성 및 문법 강조
  - `killalau.vscode-liquid-snippets`
  - `Shopify.theme-check-vscode`
- 쉘 스크립트 검사 및 정리 도구
  - `timonwong.shellcheck`
  - `mkhl.shfmt`
- Common formatter
  - `EditorConfig.EditorConfig`
  - `esbenp.prettier-vscode`
  - `stylelint.vscode-stylelint`
  - `yzhang.markdown-all-in-one`
- Git
  - `mhutchie.git-graph`

---

## 3. 초기 설정 스크립트

위치: `.devcontainer/post-create.sh`

`postCreateCommand`에 지정된 스크립트로, 컨테이너가 만들어진 후 실행된다.

Node.js 환경 구성 및 쉘 설정을 자동화한다.

### 3.1 동작 순서

1. Node.js 환경 설정
   - package.json 존재 시 Node.js LTS 설치
   - npm install 및 build 실행

2. 쉘 포매터 설치
   ```bash
   curl -sS https://webi.sh/shfmt | sh
   ```

3. oh-my-zsh 설정
   - 플러그인 추가: zsh-syntax-highlighting, zsh-autosuggestions
   - git log 페이저 비활성화

## 4. 실제 사용 흐름

1. VS Code에서 프로젝트 폴더 열기
2. 왼쪽 하단 녹색 `Reopen in Container` 버튼 클릭
   - 또는 Command Palette에서 `Dev Containers: Reopen in Container` 선택
3. Docker 컨테이너 자동 실행 및 개발환경 설정
4. 완료 후 터미널에서 Jekyll 서버 실행
   ```bash
   bundle exec jekyll serve
   ```

---

## 7. 참고

- chirpy theme guide: <https://chirpy.cotes.page/posts/getting-started/>
- dev container: <https://code.visualstudio.com/docs/devcontainers/containers>
- 쉘 포매터: <https://github.com/shfmt/shfmt>
