---
title: Chirpy 테마의 details 스타일 가이드
description: Chirpy 테마에서 details 스타일을 커스텀 하는 방법을 알아봅니다.
author: yohan
categories: [Chirpy]
tags: [chirpy, blogging]
---

## 1. 스타일 설정

`assets/css/detailsbox.scss` 파일에 다음 스타일 코드를 추가

```scss
details.details-block {
  border-radius: 0.25rem;
  border-left: 0.2rem solid var(--details-block-border-color);
  box-shadow: var(--language-border-color) 1px 1px 2px 1px; /* Using code block border color variable */
  margin-bottom: 1rem;
  padding: 0.6rem 1rem 0.6rem 1.5rem;

  > p:last-child {
    margin-bottom: 0;
  }
}

details.details-block > summary {
  padding: 0.5rem 1rem 0.5rem 1rem;
  margin: -0.6rem -1rem -0.6rem -1.5rem;
  font-weight: 600;
  background-color: var(--details-block-bg);
  color: var(--details-block-text-color);
  text-decoration: underline;
  position: relative;
  list-style: none; /* Hide default arrow */
}

details.details-block > summary::-webkit-details-marker {
  display: none; /* Hide default arrow for IOS */
}

details.details-block > summary::marker {
  content: none; /* Hide default arrow */
}

details.details-block > summary::before {
  font-family: 'Font Awesome 6 Free', sans-serif;
  content: '\f105'; /* Unicode for fa-angle-right */
  margin-right: 0.5rem;
  display: inline-block;
  transition: transform 0.2s ease;
}

details.details-block[open] > summary::before {
  transform: rotate(90deg);
}

details.details-block[open] > summary {
  margin-bottom: 0.6rem;
}

```

## 2. 색상 설정

`assets/css/colors/_light.scss` 파일에 다음 코드를 추가

```scss
@mixin styles {
  /* Details block */
  --details-block-bg: rgb(235, 240, 255, 0.5);
  --details-block-text-color: #1a1a1a;
  --details-block-border-color: #4a90e2;
}
```

`assets/css/colors/_dark.scss` 파일에 다음 코드를 추가

```scss
@mixin styles {
  /* Details block */
  --details-block-bg: rgb(30, 41, 59, 0.8);
  --details-block-text-color: #e5e9f0;
  --details-block-border-color: #60a5fa;
}
```

## 3. 적용 방법

`assets/css/jekyll-theme-chirpy.scss` 파일에 다음 코드를 추가

```scss
@use 'colors/light';
@use 'colors/dark';
@use 'detailsbox.scss';

html {
  @media (prefers-color-scheme: light) {
    &:not([data-mode]),
    &[data-mode='light'] {
      @include light.styles;
    }

    &[data-mode='dark'] {
      @include dark.styles;
    }
  }

  @media (prefers-color-scheme: dark) {
    &:not([data-mode]),
    &[data-mode='dark'] {
      @include dark.styles;
    }

    &[data-mode='light'] {
      @include light.styles;
    }
  }
}
```

## 4. 사용 방법

Example:

<details class="details-block" markdown="1">
<summary> Insert title here </summary>
Insert content here
</details>

Code:

```plaintext
<details class="details-block" markdown="1">
<summary>Insert title here </summary>
Insert content here
</details>
```
