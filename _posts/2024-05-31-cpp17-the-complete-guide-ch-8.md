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

#### Defined expression evaluation order (수식 평가 순서 확정)

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
**아직 확실치 않음** C++17에서는 evaluation order를 다음과 같이 확정.

아래의 조건에서는 e1이 e2보다 앞선다.
```
e1 [ e2 ]
e1 . e2
e1 .* e2
e1 ->* e2
e1 << e2
e1 >> e2
```

아래의 할당연산에서는 e1이 e2보다 앞선다.
```
e2 = e1
e2 += e1
e2 *= e1
...
```

new Type(e)와 같은 동적 메모리 할당시에는, 할당이 e의 평가에 앞서서 수행된다.

##### Backward incompatibilities 

평가 순서 확정으로 인해 앞선 버전에서의 연산 결과와 맞지 않는 수행 결과가 나오는 경우가 있다.

교재 60 페이지의 예제 `lang/evalexcept.cpp`를 참조.

C++17 이전에는 at 함수가 `"value: "`가 출력되기 전에 먼저 평가가 되므로, 잘못된 인덱스를 가리키고 출력하는 라인 전체가 스킵이 된다.

C++17 이후에는 `"value: "` 부분이 at 함수보다 먼저 평가되므로 `value: EXCEPTION ...` 이라는 결과가 출력된다.

