---
layout: post
title: spring MVC pattern
subtitle: 
description: spring MVC pattern
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_760/v1591001871/pixabay/strawberries-5210753_1920_tzfpb9.jpg
category: spring
tags:
  - MVC
author: jw2471358
---

![placeholder](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile9.uf.tistory.com%2Fimage%2F2247684E565C0219136F9D "spring MVC 흐름")

`웹브라우저`→ `디스패쳐서블릿`→ `컨트롤러`→ `모델앤뷰`→ `컨트롤러`→ `디스패쳐서블릿`→ `웹브라우저`로 절차를 밟게 되고 화면에 출력하기 위해 View와 ViewRewolver가 있다고 생각하면 되겠습니다.

①  `웹브라우저`에게 정보요청을 받은 `디스패쳐서블릿`은 어느 컨트롤러에 해당 요청을 전송할지 결정 

② `디스패쳐서블릿`은 핸들러 매핑에 어느 `컨트롤러`를 사용할건지 물어봄. (URL로 링크)

③ 결정된 `컨트롤러`는 해당요청을 수행하게 됨

④ 해당요청을 처리한 `컨트롤러`는 `디스패쳐서블릿`에 결과를 보냄. 이 과정에서 `Model`이 생성되어 `View(JSP)`에서 같이 사용됨 

⑤ `ModelAndView`는 실제 JSP정보를 갖고 있지 않기 때문에 뷰리졸버가 실제 JSP이름으로 변환하여 해당 view를 검색함.

⑥ 검색한 결과를 `View`에 전송

⑦ `View`는 모든 과정에서 처리된 결과를 화면으로 표현함

⑧ 마지막으로 `디스패쳐서블릿`이 `웹브라우저`에 최종결과를 출력

### References
출처: <https://hunit.tistory.com/189> [Ara Blog]

