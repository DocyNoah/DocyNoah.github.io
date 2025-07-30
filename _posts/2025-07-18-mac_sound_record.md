---
title: 맥에서 소리와 함께 화면 녹화하기
description: BlackHole 2ch를 사용해 가상 오디오 루프백을 구성하고 화면 녹화 시 소리를 함께 녹화하기
author: yohan
categories: [Mac]
tags: [mac, screen-recording, blackhole, audio, midi]
math: true
---

맥에서 기본 화면 녹화 기능을 사용할 때는 시스템 소리가 함께 녹화되지 않는다. BlackHole이라는 가상 오디오 장치를 사용하면 시스템 소리와 함께 화면을 녹화할 수 있다.

## 설치 및 설정

### 1. BlackHole 설치

```bash
brew install --cask blackhole-2ch
reboot
```

### 2. 오디오 MIDI 설정

1. <kbd>오디오 MIDI 설정</kbd> 실행
2. 좌측 하단 <kbd>+</kbd> 버튼 > <kbd>다중 출력 기기 생성</kbd> 선택
3. 다중 출력 기기에서 다음 항목 체크:
   - <kbd>MacBook Pro 스피커</kbd> (내장 출력)
   - <kbd>BlackHole 2ch</kbd> (녹화용 가상 오디오 루프백)
4. 오디오 출력 장치를 <kbd>다중 출력 기기</kbd>로 변경
   - <kbd>제어 센터</kbd> > <kbd>사운드</kbd> > <kbd>출력</kbd> > <kbd>다중 출력 기기</kbd> 선택
   - 또는 <kbd>시스템 설정</kbd> > <kbd>사운드</kbd> > <kbd>출력</kbd> > <kbd>다중 출력 기기</kbd> 선택

### 3. 화면 녹화 설정

- <kbd>Command</kbd> + <kbd>Shift</kbd> + <kbd>5</kbd> 로 화면 녹화 메뉴 열기
- <kbd>옵션</kbd> > <kbd>마이크</kbd> > <kbd>BlackHole 2ch</kbd> 선택
- 화면 녹화 시작

## 주의사항

- 녹화 완료 후 오디오 출력을 다시 <kbd>MacBook Pro 스피커</kbd>으로 변경 권장
