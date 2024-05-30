---
layout: post
title:  Chapter 7 - New Attributes and Attribute Features
date:   2024-05-30
image: /assets/images/blog/qt_sample.png
author: Marshall
tags:   [C++17]
---

## attribute
* 함수 혹은 변수 앞에 쓰여서 컴파일 시에 특정 메시지를 생성하거나 컴파일러가 특정 동작을 수행할 수 있도록 해주는 속성.
* return 값이 버려지는 경우 경고 발생시킴.

이번 글에서는 C++17에서 새로 생긴 attribute을 소개한다.

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
* 어떤 객체를 생성하고 사용하지 않는 경우, 컴파일러에서 워닝을 내보냄.

```c++
#include <iostream>
#include <string>

using namespace std;

[[maybe_unused]] struct Person {
    int age;
    string name;
    int income;
};

int main()
{
    Person p1{30, "John", 100000};
    cout << "==========" << endl;
    return 0;
}
```

위의 코드에서는 `Person` 구조체를 이용한 객체 p1을 생성하였으나, 사용하고 있지는 않다.

이를 컴파일 하는 경우, 다음과 같은 경고 메시지 출력.

```
maybe_unused_001.cpp:6:25: warning: attribute ignored in declaration of ‘struct Person’ [-Wattributes]
    6 | [[maybe_unused]] struct Person {
      |                         ^~~~~~
maybe_unused_001.cpp:6:25: note: attribute for ‘struct Person’ must follow the ‘struct’ keyword
```

`[[maybe_unused]]` 키워드를 제거한 후 컴파일을 해보면, 아무 경고 없이 컴파일 되는 것을 확인할 수 있다.

*객체가 아니라 원시 타입 앞에 [[maybe_unused]] 키워드를 붙이면 미사용시에도 경고 메시지가 뜨지 않는 것으로 확인.*

### `[[fallthrough]]`

