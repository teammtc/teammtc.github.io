---
layout: post
title:  Chapter 7 - New Attributes and Attribute Features
date:   2024-05-30
image: /assets/images/blog/qt_sample.png
author: Marshall
tags:   [C++]
---

## attribute
* 함수 혹은 변수 앞에 쓰여서 컴파일 시에 특정 메시지를 생성하거나 컴파일러가 특정 동작을 수행할 수 있도록 해주는 속성.

### `[[nodiscard]]`
* 함수의 리턴 값을 버리지 말라고 함.

### `[[maybe_unused]]`
* 어떤 변수를 선언하고 사용하지 않음으로 인해 컴파일러에서 내보내는 워닝을 발생하지 않게 해줌.

### `[[fallthrough]]`
