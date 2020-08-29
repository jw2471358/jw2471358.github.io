---
layout: post
title: gcc vs g++, g++ 옵션
subtitle: 
description: gcc vs g++, g++ 옵션
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/pixabay/dog-4988985_1920_bijzea.jpg
category: linux
tags:
  - gcc
  - g++
author: jw2471358
---

#### gcc / g++ 컴파일러에서 자주 쓸 옵션

-Wall : 모든 warning을 보여준다.

-Werror : 모든 warning을 error로 처리한다. (-Wall -Werror 처럼 warning 옵션을 켠 다음에 적어줘야 한다.)

-O1 : 크기가 최소가 되도록 최적화.

-O2 : 속도가 최대가 되도록 코드 최적화.

-Ob : 인라인 함수 확장을 막는다.

-Og : 전역 최적화 수행 (로컬/전역 공통 부분식 제거, 루프 내의 불변 부분식 제거. O1와 O2에 포함된다.)

-Od : 최적화를 아예 안 한다. (컴파일 속도 개선.)

-Os : 크기 우선 최적화 (O1에 포함된다.)

-O3 : loop unrolling과 inlining을 aggressive하게 한다. => (1) 프로그램 크기가 클 때에는 컴파일된 결과물이 instruction cache에 다 들어가지 않아서 오히려 느려질 수 있고, (2) 가끔씩 틀리기도 한다. 웬만하면 O2를 사용할 것을 권장.


-D : #ifdef TEST \ (...) \  #endif 와 같이 정의된 매크로를 -DTEST 옵션으로 발동시켜준다.

-E : preprocessing한 결과를 내보내준다. gcc -E a.cpp > a.pre 라고 적을 수도 있다.


#### gcc와 g++의 차이

1) gcc는 .c를 C로, .cpp를 C++로 컴파일해주는 반면, g++는 .c와 .cpp 둘 다 C++로 컴파일한다.

2) g++은 link할 때 std C++ library들을 link해준다. gcc는 안 그런다. 예를 들어, 코드에 #include <iostream>이 들어있으면 gcc는 자동으로 컴파일하지 못한다.

-------------------------------------------------------------------

#### GCC VS G++

| GCC           | G++              |
| :------------ | :--------------- |
| .C파일과 .CPP 파일을 각각 C언어와 C++ 언어로 컴파일 | .C파일과 .CPP 파일 모두 C++ 언어로 컴파일 |
| C라이브러리와 링크됨 | C++ 라이브러리에 링크됨 | 
| 미리 정의된 매크로가 거의 없음 | 몇 가지 추가 매크로 존재 |

출처: https://hsunnystory.tistory.com/112

-------------------------------------------------------------------

### References

https://littlepenguin.tistory.com/6

