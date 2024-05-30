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
* return 값이 버려지는 경우 경고 발생시킴.

### `[[nodiscard]]`
* 함수의 리턴 값을 버리지 말라고 함.

```c++
#include <iostream>

using namespace std;

[[ nodiscard ]] int add(int a, int b)
{
    return a + b;
}

int main(void)
{
    add(1, 2); // 함수를 호출하되, 함수의 반환 값을 버린다. 어디서 쓰지를 않기 때문.
    return 0;
}
```

위와 같은 코드를 컴파일 하는 경우, 다음과 같이 경고 메시지가 콘솔에서 확인된다.
```
nodiscard_002.cpp: In function ‘int main()’:
nodiscard_002.cpp:12:8: warning: ignoring return value of ‘int add(int, int)’, declared with attribute ‘nodiscard’ [-Wunused-result]
   12 |     add(1, 2);
      |     ~~~^~~~~~
nodiscard_002.cpp:5:21: note: declared here
    5 | [[ nodiscard ]] int add(int a, int b)
      |                     ^~~
```

### `[[maybe_unused]]`
* 어떤 변수를 선언하고 사용하지 않음으로 인해 컴파일러에서 내보내는 워닝을 발생하지 않게 해줌.

### `[[fallthrough]]`
