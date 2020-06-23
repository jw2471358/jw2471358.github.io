---
layout: post
title: CGI 그리고 Servlet과 JSP와의 관계
subtitle: 
description: CGI 그리고 Servlet과 JSP와의 관계
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1592579222/pixabay/minimal-5000883_1920_syq9yg.jpg
category: CGI 그리고 Servlet과 JSP와의 관계
tags:
  - CGI
  - Servlet
  - JSP
author: jw2471358
---

CGI -> Servlet -> JSP  개념이 등장한 순서이다. 이러한 순서로 등장한 이유는 웹의 역사를 알면 이해할 수 있다. 지금부터 웹의 역사와 함께 각 개념들이 등장한 흐름과 정의를 살펴보자.

처음 웹이 등장하고 활성화 되지 않았을때는 정적인 데이터(HTML,XML,이미지 등) 를 전달하는 것 만으로도 충분했다. 그러나 웹이 발달하면서 이제 사용자의 입력을 받아 이를 처리하고 그 결과를 다시 화면에 보여주는 동적인 페이지가 필요하게 되었다. 기존의 웹서버는 정적인 페이지를 보여주는용으로 만들었기 때문에 사용자의 요청을 받아 정보를 동적으로 생성하고 이를 다시 클라이언트로 보내주는 것이 불가능 했다. 따라서 서버에서 다른 프로그램을 불러내고 그 프로그램의 처리결과를 클라이언트로 보내줄수 있는 인터페이스가 필요했고 이것이 CGI이다.

CGI
CGI는 환경변수나 표준입출력을 다룰 수 있는 프로그램언어라면 언어의 구별을 묻지 않고 확장하여 이용하는 것이 가능하다. 대표적으로 C,Java,Python, PHP,Ruby 등이 있다.
CGI 프로그램은 서버에서 프로세스 단위로 실행이 된다. 그러다보니 사용자의 요청이 많을때 서버에 부하가 크게 가게 되었고 프로세스 보다 더 작은 단위로 실행하는것이 필요했다. 그리고 웹 서버의 프로세스로서 인터프리터를 상주시키고, CGI로부터 프로그램을 호출해 (즉, 스레드 단위로 실행) 부하를 줄임으로써 성능을 개선한 Java Servlet이 등장했다.
※Servlet 외 mod perl, mode php, FastCGI 등이 있다.


Servlet
Servlet은 Tomcat이 이해할수 있는 순수 Java 코드로만 이루어진 웹서버용 클래스이다. Java에서는 Servlet을 이용하여 CGI 프로그래밍을 할 수 있으며 Servlet은 프로그램이 실행될 때 스레드 단위로 실행되어 서버의 부하를 줄이고 CGI프로그래밍시 직접 코드에 설정을 추가해 줘야했던것을 없애줘 CGI프로그래밍을 쉽게 만들었다.
하지만 Java를 사용하여 웹페이지를 동적으로 생성하기 위해 코드안에 HTML 이 포함하는데 HTML형태로 출력하기 위해서는 print() 메소드를 사용하여 일일이 String으로 태그들을 양식에 맞춰 써야하므로 다른 서버사이드 언어에 비해 불편 하다. 또한 Java클래스 이기 때문에 테스트 하기위해서는 항상 빌드를 다시 하여 확인하여야 했고 이런 단점을 보완하기 위해 등장한것이 아래에 설명할 jsp이다.


JSP(JavaServerPage)
jsp는 html안에 자바 코드가 포함된 것으로 서버사이드 스크립트를 말한다. jsp는 실행시에는 Java Servlet 으로 변환된 후 실행되므로 서블릿과 거의 유사하다고 볼 수 있다. 하지만, 서블릿과는 달리 HTML 표준에 따라 작성되므로 웹페이지 작성이 편리해졌다. 클라이언트에서 서비스가 요청되면, JSP의 실행을 요구하고, JSP는 웹어플리케이션 서버(Tomcat)의 서블릿 컨테이너에서 서블릿 원시코드로 변환된다, 그후에 서블릿 원시코드는 바로 컴파일된 후 실행되어 결과를 HTML 형태로 클라이언트에 돌려준다. 이렇게 서블릿과 달리 JSP는 코드를 변경할 때마다 WAS에서 자동으로 빌드하고 클라이언트에 화면을 동적으로 보여주기 때문에 개발이 많이 편리해 졌다.

### References
<https://m.blog.naver.com/PostView.nhn?blogId=goddlaek&logNo=220901890910&proxyReferer=https:%2F%2Fwww.google.com%2F>