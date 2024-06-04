---
layout: post
title:  (교재 내용 정리) C++17 the Complete Guide Ch. 9 - Class Template Argument Deduction
date:   2024-06-03
image: /assets/images/blog/qt_sample.png
author: Marshall
tags:   [C++17]
---

#### CTAD (Class Template Argument Deduction)

'클래스 템플릿 인자 추론' 정도로 옮길 수 있을 것 같다.

```c++
#include <iostream>

using namespace std;

template<typename T>
class Foo
{
public:
    Foo(const T& data): data(data) {}
    T data;
};

int main(void)
{
    Foo a = 42;
    auto f = Foo{ a.data };
    cout << f.data << endl;
    return 0;
}
```

위와 같은 코드가 있을 때, `g++ -std=c++14 filename.cpp`와 같이 C++14 기준으로 컴파일을 하라고 콘솔에 입력 하면, 다음과 같은 답을 얻게 된다.

```
ctad_001.cpp: In function ‘int main()’:
ctad_001.cpp:15:9: error: missing template arguments before ‘a’
   15 |     Foo a = 42;
      |         ^
ctad_001.cpp:16:17: error: missing template arguments before ‘{’ token
   16 |     auto f = Foo{ a.data };
      |                 ^
```

C++14 및 그 이전 버전에서는 위와 같은 코드가 작동하기 위해서는 Foo의 템플릿 인자 타입을 반드시 명시해 주어야 했다. 위의 경우에는 `Foo<int>`와 같이 해줘야 했다.

하지만 C++17 이후에는 템플릿 인자 타입을 컴파일러가 추론할 수 있게 되면서, 위와 같은 코드도 컴파일이 가능해진 것이다.

