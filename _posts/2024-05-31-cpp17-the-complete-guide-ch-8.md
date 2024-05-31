---
layout: post
title:  Chapter 8 - Other Language Features
date:   2024-05-31
image: /assets/images/blog/qt_sample.png
author: Marshall
tags:   [C++17]
---

#### Nested Namespaces

```c++
namespace A {
    namespace B {
        namespace C {
            ...
        }
    }
}
```

위와 같은 네임스페이스 선언을 다음과 같이 단순화 할 수 있음.

```c++
namespace A::B::C {
    ...
}
```

#### 

```c++
string s = "I heard it even works if you don't believe";
s.replace(0, 8, "").replace(s.find("even"), 4, "sometimes").replace(s.find("you don't"), 9, "I");
```

C++17 이전에는 위와 같은 코드의 실행 결과가 반드시 `it sometimes works if I believe`가 되는 것을 보장하지 않는다.
* find() 함수 호출이 replace 함수 호출 전에 실행이 되어서 예상치 못하게 다음과 같은 결과를 가져올 수 있음.

```
it sometimes workIdon’t believe
it even worsometiIdon’t believe
it even worsometimesf youIlieve
```

