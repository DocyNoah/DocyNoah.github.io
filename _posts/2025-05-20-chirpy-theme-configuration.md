---
title: Chirpy Theme Configuration
description: Jekyll 블로그의 Chirpy 테마 설정에 대한 가이드
author: yohan
date: 2025-05-20 00:00:00+0900
categories: [Blogging]
tags: [jekyll, chirpy, blogging]
---

## theme

- 사용하는 Jekyll 테마 지정
- Jekyll 테마를 로컬로 사용 중이라면 사용되지 않음 → 삭제 가능

---

## lang

- 사이트 언어 코드
- `_data/locales/` 내 파일명과 매칭되어 작동
- `en`으로 설정 시, `_data/locales/en.yml` 파일 사용
- 웹사이트의 기본 언어
- HTML `<html lang="...">` 태그 설정에 사용
- SEO 메타 데이터 `<meta property="og:locale" content="..." />`에 사용

---

## timezone

- 포스트의 시간대 기준 지정
- Jekyll이 Markdown 포스트의 날짜를 파싱할 때 기준 시간대로 사용
- 포스트의 작성 시간에 영향
- 설정 코드는 [Time Zone Picker](https://kevinnovak.github.io/Time-Zone-Picker) 참고

---

## title

- 사이트 이름
- 사이트 좌측 사이드바에 표시
- 브라우저 탭에 표시
- SEO 메타 데이터 `<meta property="og:site_name" content="..." />`에 사용

---

## tagline

- 사이트 부제목
- 사이트 좌측 사이드바에 표시
- 블로그를 한 문장으로 소개하는 문구로 설정

---

## description

- 사이트 전체 설명
- 사이트 내에서는 확인 불가
- 사이트 홈에서만 사용됨
- 검색 노출에 영향
- Google 등에서 사이트 미리보기에 사용
- 다음 SEO 메타 데이터에 사용
  - `<meta name="description" content="..." />`
  - `<meta property="og:description" content="..." />`

---

## url

- 사이트의 루트 URL (프로토콜 포함, 끝에 / 없이)
- GitHub Pages 사용 시, 일반적으로 `https://<github-username>.github.io` 로 설정

---

## github.username

- GitHub user name
- 사이트 좌측 사이드바 하단 GitHub 링크에 `https://github.com/...`에 사용

---

## twitter.username

- Twitter user name
- 사이트 좌측 사이드바 하단 Twitter 링크에 `https://twitter.com/...`에 사용
- SEO 메타 데이터 `<meta name="twitter:site" content="@..." />`에 사용

---

## social.name

- 사이트 작성자 이름
- 사이트 최하단 footer에 카피라이트 소유자 명으로 표시

---

## social.email

- 사이트 작성자 이메일
- 사이트 좌측 사이드바 하단 Email 링크에 파싱되어 사용
- `example@domain.com` 설정 시, `'mailto:' + ['example','domain.com'].join('@')`로 파싱

---

## social.links

- 사이트의 대표 SNS/프로필 링크 모음
- 첫번째 링크는 사이트 최하단 footer에 카피라이트 소유자명에 링크됨
- 첫번째 링크를 포함한 모든 링크는 사이트 홈에서만 SEO 메타 데이터로 사용
- 이외에 사용처 없음

---

## webmaster_verifications.*

- 사이트가 특정 검색 엔진이나 서비스에 등록된 소유자임을 증명하기 위한 인증 코드
- HTML `<head>` 내부 메타 태그로만 존재
- 사용 방법은 별도 참고

---

## analytics.*

- 사이트에 접속한 사용자 트래픽을 수집하고 분석하는 외부 웹 분석 도구
- 각 서비스의 ID만 입력하면 자동으로 추적 스크립트를 HTML에 삽입
- 사용 방법은 별도 참고

---

## pageviews.provider

- 조회수 표시 기능
- 현재 goatcounter만 지원
- 사용 방법은 별도 참고

---

## theme_mode

- 기본 색상 테마
- `light`, `dark`로 지정
- 비워두면 사용자 시스템 설정을 따름
- 사용자는 사이트 촤즉 사이드마 하단에서 색상 테마 변경 가능

---

## cdn

- `/`로 시작하는 모든 미디어 파일 경로 앞에 자동으로 붙는 CDN 주소
- 포스트 내부 이미지, 오디오, 비디오 등 미디어 파일에 적용됨

---

## avatar

- 프로필 이미지 경로
- 사이트 좌측 사이드바에 표시

---

## social_preview_image

- 사이트가 공유될 때 미리보기 카드에 사용되는 대표 이미지
- SEO 메타 데이터 `<meta property="og:image" content="..." />`에 사용됨
- 개별 포스트에서는 Front Matter에 `image` 값을 지정하면 덮어쓰기 가능

---

## tօc

- 사이트 전체에 적용되는 목차(Table of Contents) 표시 전역 설정
- 활성화하면 사이트 우측 사이드바에 목차가 표시됨
- 개별 포스트에서는 Front Matter에 toc 값을 지정하면 덮어쓰기됨

---

## comments.provider

- 사이트 전체에 적용되는 댓글 기능의 전역 설정
- 비워두면 댓글 기능은 비활성화
- 아래 중 하나의 provider를 선택해 설정
  - disqus
  - utterances
  - giscus
- 개별 포스트에서는 Front Matter에서 `comments` 값을 지정하면 덮어쓰기 가능
- provider 간단 비교

  | 구분 | Disqus | Utterances | Giscus |
  |:--|:--|:--|:--|
  | 기반 | 자체 플랫폼 | GitHub Issues | GitHub Discussions |
  | 설치 난이도 | 낮음 | 중간 | 중간~높음 |
  | GitHub 연동 필요 | ❌ 아님 | ✅ 필요 | ✅ 필요 |
  | 댓글 저장 위치 | Disqus 서버 | GitHub 저장소의 Issues | GitHub Discussions |
  | SSO 로그인 지원 | ✅ (Google, Twitter, 등) | ❌ (GitHub만) | ❌ (GitHub만) |
  | 익명 댓글 가능 여부 | ✅ 가능 | ❌ GitHub 계정 필수 | ❌ GitHub 계정 필수 |
  | 광고 노출 | ✅ 있음 (무료 사용 시) | ❌ 없음 | ❌ 없음 |
  | 다국어 지원 | ✅ (자동 언어 감지) | ❌ 제한적 | ✅ lang 옵션 지정 가능 |
  | 댓글 반응(이모지) | ✅ (좋아요 등) | ❌ 없음 | ✅ 있음 |
  | UI 커스터마이징 | ❌ 제한적 | ❌ 제한적 | ❌ 제한적 |
  | 페이지별 댓글 구분 | 자동 | issue_term 지정 필요 | mapping 지정 필요 |
  | 비용 | 무료 + 유료 (광고 제거) | 무료 | 무료 |
  | PWA 지원 | 제한적 | ✅ 빠름 | ✅ 빠름 |

---

## assets.self_host.enable

- Chirpy 테마에서 사용하는 외부 CDN 에셋(mermaid, mathjax 등)을 직접 로컬에서 제공하도록 전환하는 설정
- 필요한 정적 자산들은 [chirpy-static-assets](https://github.com/cotes2020/chirpy-static-assets) 저장소에서 제공하며, 프로젝트에 포함해 사용
- 비워두면 false로 설정
- 자세한 설정은 [chirpy-static-assets](https://github.com/cotes2020/chirpy-static-assets) 참고

---

## pwa.enabled

- PWA(Progressive Web App) 기능 활성화 여부
- 브라우저에서 설치 가능한 웹앱으로 동작하게 함
- 사이트를 모바일 또는 데스크탑에 설치해 앱처럼 사용 가능
- 설치 가능 여부는 브라우저 및 운영체제의 PWA 지원 여부에 따라 달라짐
- pwa.cache.enabled: PWA의 오프라인 캐시 기능 활성화 여부
- pwa.cache.deny_paths: PWA 캐시 대상에서 제외할 경로 목록

---

## paginate

- 한 페이지에 표시할 포스트 수를 지정
- 블로그 홈(index.html)과 아카이브 페이지에서 적용됨
- Jekyll의 jekyll-paginate 플러그인 기반으로 작동

---

## baseurl

- 사이트의 하위 경로 (Base Path)를 지정
- GitHub Pages에서 프로젝트 페이지(username.github.io/repo-name)처럼 루트가 아닌 경로에 배포할 때 설정
- 루트 도메인에 배포할 경우 비워둠("")

---

## kramdown

- Jekyll의 기본 마크다운 엔진 설정
- 수정하지 않는 것이 권장됨

---

## collections.*

- Jekyll의 collections 기능을 활용해 사이트 좌측에 탭을 설정
- `_tabs/` 폴더의 파일들이 collections이 됨
- 수정할 시 사이트 망가짐

---

## defaults

- posts 파일들의 기본값 설정
- drafts 파일들의 기본값 설정
- tabs 파일들의 기본값 설정
- 수정하지 않는 것이 권장됨

---

## sass.style

- 사이트에서 사용하는 Sass(CSS 전처리기)의 출력 방식 설정
- compressed로 설정 시, 최종 CSS가 공백 없이 압축된 형태로 출력
  - 예: 줄바꿈, 들여쓰기 없이 한 줄로 출력되어 용량 최소
- 다른 옵션으로는 expanded, nested, compact 등이 있지만, compressed는 배포용으로 가장 적합

---

## compress_html

- HTML 소스 코드 압축 설정

---

## exclude

- Jekyll 빌드 시 사이트 생성 대상에서 제외할 파일 또는 디렉토리 목록
- 여기에 명시된 항목은 _site/ 결과물에 포함되지 않음

---

## jekyll-archives

- 카테고리 및 태그별 아카이브 페이지를 자동으로 생성하는 Jekyll 플러그인 설정
- 수정하지 않는 것이 권장됨
