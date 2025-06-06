---
title: "RuntimeError: CUDA unknown error"
description:
author: yohan
categories: [Dev]
tags: [pytorch, cuda, error, ubuntu, linux]
---

NVIDIA Driver도 잘 설치되어있고, CUDA도 잘 설치되어있고, PyTorch도 잘 설치되어있는데, torch에서 cuda 사용시 `RuntimeError: CUDA unknown error`가 발생할 때

```bash
reboot
```

잘 되다가 갑자기 에러가 발생할 때는 보통 이 방법으로 다 해결된다.

---

그래도 안되면

```bash
sudo apt-get install nvidia-modprobe
```

위 명령어를 실행한다. 보통 다 해결된다.

## Reference

- [RuntimeError: CUDA unknown error · Issue #49081 · pytorch/pytorch](https://github.com/pytorch/pytorch/issues/49081)
