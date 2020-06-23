---
layout: post
title: JSP/Servlet sendRedirect방식과 forward방식의 차이
subtitle: 
description: JSP/Servlet sendRedirect방식과 forward방식의 차이
# image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1592579222/me/%EA%B0%80%EC%A1%B1%EA%B4%80%EA%B3%84%EB%93%B1%EB%A1%9D%EB%B6%80_vrqfox.jpg
category: JSP/Servlet
tags:
  - CGI
  - Servlet
  - JSP
author: jw2471358
---

서블릿에서 특정 URL이나 페이지로 이동하게 하는 방식은 Redirect방식 , forward 방식 이렇게 두가지가 있다.  둘은 각각 어떤 성격을 가지고 있는지 알아보자.

1. Redirect 방식
Redirect방식은 서블릿에서 response.sendRedirect("주소"); 로 사용한다.(Redirect방식은 웹애플리케이션 외부url 로도 이동가능하다. )  Redirect 는 아래 그림의 과정을 따라가며 이해할 수있다.

![placeholder](http://www.javajigi.net/pages/viewpage.action?pageId=77)

ⓐ a.jsp에 Redirect 가 있고 클라이언트가 a.jsp를 서버에 요청 했을때 ⓑ 서버에서는  a.jsp가 이러한 페이지를 요청했다고 클라이언트에게 응답을 돌려준다. ⓒ 응답을 받은  클라이언트는 a.jsp에서 이동하려한 주소의 페이지를 서버에 새로 요청한다. ⓓ 서버는 해당하는 페이지에 대한 응답을 다시 클라이언트에 보내준다. 

결론적으로 Redirect 방식은 페이지 이동을 위해 왔다갔다 2번의 요청을 해야하며 새로운 페이지를 요청하기때문에 url 주소가 바뀌고 최종적으로 ⓓ의 응답이 왔을때 ⓐ의 요청은 더이상 유효하지 않으므로 페이지간 데이터 전달이 어렵다. 
페이지 간에 데이터 전달의 경우 session을 사용할수 있었지만 session을 이용하면 시스템에 메모리 과부하가 발생할 수 있으므로 이런경우 RequestDispatcher를 이용한 forward를 한다.

2. forward 방식
forward 방식은 내부자원으로의 이동만 가능하며 forward에 의해 호출될 페이지는 현재의 request와 response를 공유하므로 페이지간 데이터 전달이 가능하다.  서블릿에서는 
RequestDispatcher dispatcher = request.getRequestDispatcher(url);
dispatcher.forward(request, response);   
로 forward를 사용한다.  (jsp는 action태그로도 사용가능)
RequestDispatcher와 함께 forward를 사용하는데  RequestDispatcher 클래스에 현재 request,response를 담아 공유한다.
forward 방식 역시 그림의 과정을 보자

![placeholder](http://www.javajigi.net/pages/viewpage.action?pageId=77)

ⓐ a.jsp에 forward가 있고 클라이언트가 a.jsp를 서버에 요청한다. ⓑ 서버는 a.jsp 실행도중 forward에 의해 b.jsp를 요청받은뒤 ⓒ b.jsp에 대한 응답을 클라이언트에게 보낸다. 처음 브라우저는 a.jsp를 요청한뒤 서버에서 b.jsp로 이동된 줄 모르는 상태로 결과만 받기 때문에 돌아온 결과가 마치 a.jsp에 대한 응답인것처럼 a.jsp url로 b.jsp의 결과를 출력한다.

결론적으로 forward방식은 (서버)웹 컨테이너 차원에서만 페이지 이동이 있다. 그래서 웹브라우저는 다른페이지로 이동했음을 알수없고  url 정보가 변경되지 않는다. 따라서 최초의 요청정보는 ⓒ에서도 유효하고 ⓐ에서의 데이터를 사용할수 있다. 그렇기 때문에 만약 ⓒ화면에서 새로고침을 계속 한다면 ⓐ의 요청에 ⓒ의 결과가 반복적으로 나타나게된다. 
한번의 요청으로 페이지 이동이 가능해서 Redirect방식보다 응답이 빠르지만 시스템(DB,세션 등..)에 변화가 생기는 요청(로그인 , 회원가입 , 글쓰기 등) 의 경우 새로고침만으로 똑같은 정보를 계속 요청하는 에러가 발생할 수 있다. 따라서 이 경우는 Redirect방식으로 사용하고 시스템에 변화가 생기지 않는 단순 조회 요청(글 조회 검색 등..)의 경우 forward방식을 사용하는것이 좋다.

### References
<https://m.blog.naver.com/goddlaek/220911115320>