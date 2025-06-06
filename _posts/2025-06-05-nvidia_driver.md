---
title: NVIDIA Driver 설치 및 업데이트 방법
description: Ubuntu 22.04에서 Nouveau 비활성화부터 NVIDIA 드라이버 설치까지 전체 과정 가이드
author: yohan
categories: [Dev]
tags: [nvidia, driver, ubuntu, linux]
---

Ubuntu 22.04에 NVIDIA Driver를 설치하고 업데이트하는 방법을 알아본다.

## 1. Nouveau 비활성화

NVIDIA Driver를 설치하기 전에 Nouveau를 비활성화해야 한다.

<details class="details-block">
<summary>Nouveau란?</summary>
리눅스에서 NVIDIA GPU를 위한 오픈 소스 그래픽 드라이버입니다. NVIDIA가 공식적으로 제공하는 드라이버(NVIDIA proprietary driver)와는 별개로, 리눅스 커뮤니티에서 개발한 드라이버이다.
</details>

### 1.1 Nouveau 확인

```bash
lsmod | grep nouveau
```

출력된 결과가 없다면 Nouveau가 이미 비활성화되어 있는 것이다.

### 1.2 Nouveau 비활성화

1. `/etc/modprobe.d/blacklist-nouveau.conf` 파일을 생성한다.
   - 사실 경로만 중요하고 파일명은 상관없다.
2. 다음 내용을 추가한다.
   ```plaintext
   blacklist nouveau  # nouveau load 차단
   options nouveau modeset=0  # nouveau Kernel Module 비활성화
   ```
3. 작성 사항 반영
   ```bash
   sudo update-initramfs -c
   ```

## 2. NVIDIA Driver 제거

업데이트하는 것이라면 따로 방법이 있는 것이 아니고 제거 후 업데이트 버전을 설치하면 된다.

> 제거하지 않으면 설치가 되지 않음. 반드시 제거 해야함.
{: .prompt-warning }

### 2.1 NVIDIA Driver 제거

```bash
sudo apt-get remove --purge *nvidia*
sudo apt autoremove
sudo apt-get autoclean
```

### 2.2 NVIDIA Driver 제거 확인

```bash
dpkg -l | grep nvidia
```

출력된 결과가 없다면 NVIDIA Driver가 제거된 것이다.

## 3. NVIDIA Driver 설치

### 3.1 Graphics Driver Repository 추가

```bash
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
```

### 3.2 설치 가능한 NVIDIA Driver 확인

```bash
ubuntu-drivers devices
```

### 3.3 NVIDIA Driver 설치

특정 버전 설치 (예: 570 버전)

```bash
sudo apt install nvidia-driver-570
```

자동 설치

```bash
sudo ubuntu-drivers autoinstall
```

### 3.4 재부팅 및 설치 확인

```bash
sudo reboot
nvidia-smi
```
