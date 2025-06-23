---
title: Ubuntu 한글 입력기 설치 방법
description: Ubuntu에서 한글 입력기를 설치하고 설정하는 방법을 단계별로 알아본다.
author: yohan
categories: [Dev]
tags: [ubuntu, linux]
---

Ubuntu 환경에서 한글을 사용하기 위해서는 몇 가지 설정이 필요하다. 이 포스트에서는 한글 언어 팩을 설치하고, IBus 입력기를 설정하여 한글을 원활하게 입력할 수 있는 방법을 단계별로 설명한다.

## 1. 한글 언어 팩 설치

- `Settings` > `Region & Language`로 이동
- `Manage Installed Languages` 클릭
- `Language Support` 창에서 `Install` 클릭하여 패키지 설치
- `Install / Remove Languages...` 클릭
- `Korean` 체크, `English`를 포함하여 불필요한 언어 팩들은 체크 해제 후 `Apply`
  - `English`를 해제한다고 해서 영어를 사용하지 못하는 것은 아님
- 시스템 재부팅

## 2. IBus 입력기 설정

- 터미널에서 `ibus-setup` 실행
- `Input Method` 탭으로 이동
- `Add` 클릭
- 언어 목록에서 `Korean` 선택
- `Hangul` 선택 후 `Add`

## 3. 키보드 입력 소스 추가

- `Settings` > `Keyboard`로 이동
- `Input Sources`에서 `+` 버튼 클릭
- `Add an Input Source` 창에서 `Korean` 선택
- `Korean (Hangul)` 선택 후 `Add`
  - 다른 `Korean`이나 `Korean(101/104-key ...)`는 안 됨

## 4. 한/영 전환 키 설정

- `Input Sources` 목록에서 `Korean (Hangul)` 확인
- `Korean (Hangul)`을 제외한 모든 언어 제거
  - `English`도 제거해야 함
- `Korean (Hangul)`의 `Preferences` 클릭
- `Hangul Toggle Key`에서 `Add`를 누르고 원하는 한/영 전환 키(예: `Alt_R`) 등록
