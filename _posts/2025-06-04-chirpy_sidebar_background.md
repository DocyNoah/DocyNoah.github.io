---
title: Chirpy 테마 사이드바 배경 이미지 추가
description: Chirpy 테마에서 사이드바 배경 이미지를 추가하고 텍스트 색상을 변경하는 방법을 알아봅니다.
author: yohan
categories: [Chirpy]
tags: [chirpy, blogging]
---

## 1. 이미지 추가

`assets/css/sidebar.scss` 파일에 다음 스타일 코드를 추가

```scss
#sidebar {
  background-image: url("IMAGE_URL");  // change background image
  background-size: cover;  // customize the image size
  background-repeat: no-repeat;  // no-repeat
  background-position: top;  // image position
}
```

## 2. 사이드바 텍스트 색상 변경

배경 이미지가 너무 밝거나 어두울 경우 텍스트가 잘 안 보일 수 있다.
텍스트 색상을 변경하여 더 잘 보이게 할 수 있다.

`assets/css/sidebar.scss` 파일에 다음 스타일 코드를 추가

```scss
#sidebar .site-title {
    color: #ffffff; 
    text-shadow: 5px 5px 10px rgba(0,0,0,0.5);
}
#sidebar .site-subtitle {
    color: #ffffff;
    text-shadow: 2px 2px 3px rgba(0,0,0, 0.7);
}
#sidebar ul li.nav-item a.nav-link span{
    font-size: 100%;
}
#sidebar ul li.nav-item a.nav-link {
    color: #ffffff;
}
```

## 3. 적용 방법

`assets/css/jekyll-theme-chirpy.scss` 파일에 다음 코드를 추가

```scss
@use 'sidebar.scss';
```
