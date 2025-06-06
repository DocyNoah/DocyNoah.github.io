---
title: Chirpy 테마의 고급 프롬프트 스타일 가이드
description: Chirpy 테마에서 제공하는 기본 프롬프트와 커스텀 컬러박스 스타일링 방법을 알아봅니다.
author: yohan
categories: [Chirpy]
tags: [chirpy, blogging]
---

## 1. 스타일 설정

`assets/css/colorbox.scss` 파일에 다음 스타일 코드를 추가

```scss
@mixin colorbox($border-color, $icon-color, $icon-content, $bg-color, $fa-style: 'solid') {
  border-left: .2rem solid $border-color;
  border-radius: 0.25rem;
  color: var(--text-color);
  padding: .6rem 1rem .6rem 1.5rem;
  box-shadow: var(--language-border-color) 1px 1px 2px 1px;
  position: relative;
  margin-bottom: 1rem;

  > div.title::before {
    content: $icon-content;
    color: $icon-color;
    font: var(--fa-font-#{$fa-style});
    text-align: center;
    width: 3rem;
    position: absolute;
    left: .2rem;
    margin-top: .4rem;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
  }

  > div.title {
    background-color: $bg-color;
    color: $icon-color;
    padding: .5rem .6rem .5rem 3rem;
    margin: -.6rem -1rem .6rem -1.5rem;
    font-weight: 600;
  }

  > p:last-child{
      margin-bottom: 0;
  }
}

.box-info {
  @include colorbox(
    var(--prompt-info-icon-color),
    var(--prompt-info-icon-color),
    "\f06a",
    var(--prompt-info-bg)
  );
}

.box-tip {
  @include colorbox(
    var(--prompt-tip-icon-color),
    var(--prompt-tip-icon-color),
    "\f0eb",
    var(--prompt-tip-bg),
    'regular'
  );
}

.box-warning {
  @include colorbox(
    var(--prompt-warning-icon-color),
    var(--prompt-warning-icon-color),
    "\f06a",
    var(--prompt-warning-bg)
  );
}

.box-danger {
  @include colorbox(
    var(--prompt-danger-icon-color),
    var(--prompt-danger-icon-color),
    "\f071",
    var(--prompt-danger-bg)
  );
}
```

## 2. 적용 방법

`assets/css/jekyll-theme-chirpy.scss` 파일에 다음 코드를 추가

```scss
@use 'colorbox.scss';
```

## 3. 사용 방법

### 제목이 있는 컬러박스

컬러박스의 가장 큰 장점은 제목을 추가할 수 있다는 점이다.

Example:

<div class="box-tip" markdown="1">
<div class="title"> Insert title here </div>
Insert content here
</div>

Code:

```plaintext
<div class="box-tip" markdown="1">
<div class="title"> Insert title here </div>
Insert content here
</div>
```

### 제목이 없는 컬러 박스

제목 없이도 사용할 수 있다.

제목이 없는 컬러박스는 두 가지 방식으로 사용할 수 있다.

Example:

<div class="box-tip" markdown="1">
Insert box-tip here
</div>

Code:

```plaintext
<div class="box-tip" markdown="1">
Insert box-tip here
</div>
```

or

```plaintext
> Insert box-tip here
{: .box-tip }
```
