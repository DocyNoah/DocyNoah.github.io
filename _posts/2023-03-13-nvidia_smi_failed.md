---
title: "nvidia-smi - Failed to initialize NVML: Driver/library version mismatch"
description: Ubuntu 환경에서 nvidia-smi 실행 시 발생하는 드라이버 버전 불일치 문제를 해결하는 방법을 설명한다. NVIDIA 드라이버 커널 모듈을 언로드하고 재로드하는 과정을 통해 문제를 해결할 수 있다.
author: yohan
categories: [Dev]
tags: [nvidia, driver, ubuntu, linux, error]
---

Ubuntu에서 `nvidia-smi` 명령어를 실행하면 `Failed to initialize NVML: Driver/library version mismatch` 에러가 발생하는 경우가 있다.
여러가지 원인과 그에 따른 해결 방법들이 있겠지만, 해결된 경험이 있어 기록해본다.

## 요약

```bash
systemctl isolate multi-user.target
sudo apt --fix-broken install
sudo rmmod nvidia_drm
sudo rmmod nvidia_modeset
sudo rmmod nvidia_uvm
sudo rmmod nvidia
sudo modprobe nvidia
systemctl start graphical.target
nvidia-smi
```

## 1. 로드 되어있는 NVIDIA Driver Kernel Module 확인

```bash
lsmod | grep nvidia
```

아마 `nvidia_uvm`, `nvidia_drm`, `nvidia_modeset`, `nvidia`가 확인 될 것이다.
이들을 모두 unload 해야 한다.

## 2. Unload NVIDIA Driver Kernel Module

```bash
sudo rmmod nvidia_uvm
sudo rmmod nvidia_drm
sudo rmmod nvidia_modeset
sudo rmmod nvidia
```

### 2.1 Troubleshooting

#### Error 1

```bash
rmmod: ERROR: Module nvidia_modeset is in use by: nvidia_drm`
```

위 에러가 발생하면 nvidia_drm가 nvidia_modeset를 사용중이어서 nvidia_modeset를 언로드할 수 없으니 nvidia_drm를 먼저 언로드하면 된다.

#### Error 2

```bash
rmmod: ERROR: Module nvidia_drm is in use
```

`sudo rmmod nvidia_drm` 실행 중 위 에러가 발생하면 다음 명령어를 실행해본다.

```bash
su root
systemctl isolate multi-user.target
modprobe -r nvidia-drm
systemctl start graphical.target
su user
```

## 3. 확인

```bash
lsmod | grep nvidia
```

전부 unload 되었다면 성공이다. 이제 `nvidia-smi` 명령어를 실행해보자.
안되면 이젠 모른다.
