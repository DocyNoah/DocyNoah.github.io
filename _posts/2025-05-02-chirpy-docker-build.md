---
title: Chirpy Theme Docker Build
description: VS Code Dev Containers를 활용한 Chirpy 테마 개발 환경 구성 가이드
author: yohan
date: 2025-05-02 00:00:00+0900
categories: [Blogging, Tutorial]
tags: [jekyll, chirpy, blogging, docker, vscode, tutorial]
---

## 1. Dev Containers (VS Code + Docker 기반 개발 환경)

VS Code의 Dev Containers는 Docker를 이용해 개발 도구와 설정을 격리된 컨테이너 안에 구성할 수 있게 해줍니다.
로컬 시스템에 Ruby, Node.js, Jekyll 등을 설치하지 않아도 곧바로 개발을 시작할 수 있으며, 환경 충돌 없이 일관된 개발 환경을 제공합니다.

---

## 2. 사전 설치 항목

Dev Containers를 사용하기 위해서는 다음 도구가 필요합니다.

- Docker
- Windows/macOS: Docker Desktop
- Linux: Docker Engine
- Visual Studio Code
- VS Code Extension: Dev Containers

---

## 3. Dev Container 구성 파일: .devcontainer/devcontainer.json

이 파일은 Dev Container의 전체 환경을 정의합니다. 주요 항목은 다음과 같습니다.

```json
{
  "name": "Jekyll",
  "image": "mcr.microsoft.com/devcontainers/jekyll:2-bullseye",
  "onCreateCommand": "git config --global --add safe.directory ${containerWorkspaceFolder}",
  "postCreateCommand": "bash .devcontainer/post-create.sh",
  "customizations": {},
}
```

- `image`: Jekyll이 사전 설치된 공식 Docker 이미지입니다.
- `onCreateCommand`: 컨테이너가 처음 만들어질 때 실행되는 명령입니다. Git 경고 방지를 위해 프로젝트 디렉토리를 안전한 디렉토리로 등록합니다.
- `postCreateCommand`: 컨테이너 생성 직후 실행되는 셋업 스크립트입니다.

---

## 4. VS Code 확장 자동 설치

devcontainer.json 안에는 다음과 같은 확장 목록이 포함되어 있어 컨테이너 환경에서도 개발 효율을 높여줍니다.

- Liquid 템플릿 자동완성 및 문법 강조:
  - `killalau.vscode-liquid-snippets`
  - `Shopify.theme-check-vscode`
- 쉘 스크립트 검사 및 정리 도구:
  - `timonwong.shellcheck`
  - `mkhl.shfmt`
- Common formatter:
  - `EditorConfig.EditorConfig`
  - `esbenp.prettier-vscode`
  - `stylelint.vscode-stylelint`
  - `yzhang.markdown-all-in-one`
- Git:
  - `mhutchie.git-graph`

---

## 5. 초기 설정 스크립트: .devcontainer/post-create.sh

컨테이너가 만들어진 후 실행되는 스크립트로, Node.js 환경 구성 및 쉘 설정을 자동화합니다.

### 동작 순서

1. package.json이 존재할 경우:
   - Node.js LTS 설치 (nvm)
   - npm install, npm run build 실행

2. 쉘 포매터 설치:

   ```bash
   curl -sS https://webi.sh/shfmt | sh
   ```

3. oh-my-zsh 플러그인 추가:
   - zsh-syntax-highlighting
   - zsh-autosuggestions
   - git log 실행 시 less 페이지 사용 비활성화

## 6. 실제 사용 흐름

1. VS Code에서 프로젝트 폴더 열기
2. 왼쪽 하단 녹색 아이콘 클릭 → `Reopen in Container`
   - 또는 Command Palette에서 `Dev Containers: Reopen in Container` 선택
3. Docker 컨테이너 자동 실행 및 개발환경 설정
4. 완료 후 터미널에서 Jekyll 서버 실행:

```bash
bundle exec jekyll serve
```

---

## 7. 참고

- chirpy theme guide: <https://chirpy.cotes.page/posts/getting-started/>
- dev container: <https://code.visualstudio.com/docs/devcontainers/containers>
- 쉘 포매터: <https://github.com/shfmt/shfmt>
