---
title: Chirpy Theme Structure Guide
description: Chirpy 테마의 디렉토리 구조에 대한 가이드. 각 구성 요소의 목적과 구조 설명
author: yohan
categories: [Blogging]
tags: [jekyll, chirpy, blogging]
---

## Theme Structure

```bash
.
├── _config.yml
├── _data/
├── _includes/
├── _javascript/
├── _layouts/
├── _plugins/
├── _posts/
├── _sass/
├── _tabs/
├── .devcontainer/
├── .editorconfig
├── .git/
├── .gitattributes
├── .github/
├── .gitignore
├── .gitmodules
├── .husky/
├── .markdownlint.json
├── .nojekyll
├── .stylelintrc.json
├── .vscode/
├── assets/
├── docs/
├── eslint.config.js
├── Gemfile
├── index.html
├── jekyll-theme-chirpy.gemspec
├── LICENSE
├── package.json
├── purgecss.js
├── README.md
├── rollup.config.js
└── tools/
```

---

## 1. 빌드 필수 구성 (Jekyll 자체 빌드에 꼭 필요한 항목)

사이트 HTML을 생성하는 데 Jekyll이 직접 사용하는 핵심 폴더와 설정 파일

| 항목 | 설명 |
|:--|:--|
| _config.yml | 전체 설정 파일 (사이트 제목, URL, 플러그인, 경로 등) |
| _data/ | YAML 기반 설정 데이터 (저자, 연락처, 공유 옵션 등) |
| _includes/ | 레이아웃 구성 요소 (header, footer, sidebar 등) |
| _layouts/ | 레이아웃 템플릿 (post.html, page.html 등) |
| _posts/ | 블로그 글 (Markdown) 저장 폴더 |
| _tabs/ | About, Tags, Categories 등 탭 정의 |
| index.html | 홈 페이지 진입점 |
| assets/ | 정적 자산(CSS, JS, 이미지 등) |
| Gemfile | Ruby 의존성 관리 (Jekyll, 플러그인 등) |

---

## 2. JS/CSS 빌드 도구 구성 (자바스크립트 번들 및 최적화)

사이트 성능 최적화를 위한 JS, CSS 번들링 관련 항목
필요 시 npm run build를 통해 CSS/JS 생성

| 항목 | 설명 |
|:--|:--|
| _sass/ | SCSS 스타일 정의 (분할 파일 구조) |
| _javascript/ | 모듈형 JS 소스 코드 |
| package.json | npm 의존성 정의 및 고정 |
| rollup.config.js | JS 번들 설정 (Rollup 사용) |
| purgecss.js | 사용되지 않는 CSS 제거 설정 (PurgeCSS) |

---

## 3. 유틸리티/자동화/보조 스크립트 구성

배포, 테스트, 초기화 등을 돕는 스크립트 및 설정 파일

| 항목 | 설명 |
|:--|:--|
| tools/ | init.sh, test.sh 등 환경 초기화 및 테스트 자동화 |
| .editorconfig | 코드 스타일 통일 설정 |
| .husky/ | Git hook 설정 (커밋 메시지 검사 등) |
| .stylelintrc.json, .markdownlint.json | 스타일 검사 도구 설정 |
| eslint.config.js | JS 코드 스타일 검사 설정 |

---

## 4. 개발 환경 구성 (DevContainer / VSCode)

개발자 편의 환경 설정

| 항목 | 설명 |
|:--|:--|
| .devcontainer/ | VS Code Dev Container 구성 (Docker 기반 개발환경) |
| .vscode/ | VS Code 전용 에디터 설정 (확장 추천, 테마 등) |

---

## 5. 버전 관리 및 문서

| 항목 | 설명 |
|:--|:--|
| .git, .gitignore, .gitattributes, .gitmodules | Git 저장소 및 서브모듈 설정 |
| .github/ | GitHub Actions 워크플로우, PR 템플릿 등 |
| README.md | 프로젝트 설명서 |
| LICENSE | 오픈소스 라이선스 명세 |
| docs/ | 기여 가이드, 보안 문서 등 (공개 프로젝트용) |
