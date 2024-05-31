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