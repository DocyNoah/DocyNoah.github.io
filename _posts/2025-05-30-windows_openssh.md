---
title: Windows OpenSSH 설치 및 설정
description: Windows에 OpenSSH 설치 및 설정 방법
author: yohan
categories: [Dev]
tags: [ssh, cmd, windows]
---

사용 OS: Windows 11

## OpenSSH 설치 확인

1. PowerShell을 관리자 권한으로 실행
2. 다음 명령어로 OpenSSH 설치 여부 확인:
   ```powershell
   Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'
   ```

   예시 출력:
   ```powershell
   Name  : OpenSSH.Client~~~~0.0.1.0
   State : Installed
   Name  : OpenSSH.Server~~~~0.0.1.0
   State : NotPresent
   ```
   위 예시는 OpenSSH 클라이언트는 설치되어 있고, 서버는 설치되지 않은 상태를 나타냄

## OpenSSH 설치 방법

### A. PowerShell 이용 설치

OpenSSH 서버 설치:
```powershell
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

OpenSSH 클라이언트 설치:
```powershell
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
```

### B. Windows 설정 이용 설치

1. Windows 설정 > `앱` > `선택적 기능` 열기
2. `선택적 기능 추가`의 `기능 보기` 클릭
3. "OpenSSH 서버" 또는 "OpenSSH 클라이언트" 검색 후 설치

## OpenSSH 서버 설정

서비스 시작:
```powershell
Start-Service sshd
```

자동 실행 설정:
```powershell
Set-Service -Name sshd -StartupType 'Automatic'
```

서비스 상태 확인:
```powershell
Get-Service sshd | Select-Object Status, StartType
```

## (선택) 방화벽 규칙 설정

기본적으로 방화벽 규칙이 자동 생성되나, 없는 경우 다음 명령어로 생성
```powershell
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
```

## 참고 사항

- Windows 10 버전 1809 이상 필요
- PowerShell 5.1 이상 권장
- 기본 SSH 포트는 22번
