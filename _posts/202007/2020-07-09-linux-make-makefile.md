---
layout: post
title: 리눅스 make와 Makefile
subtitle: 
description: 리눅스 make와 Makefile
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/pixabay/seascape-5236865_1920_cetbqt.jpg
category: 리눅스
tags:
  - 리눅스
  - make
  - MakeFile
author: jw2471358
---

<p><b>* Make, Makefile</b></p>

<p style="" _foo="text-align: center; " align="center"><span class="_img  fx" thumburl="https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMTAy/MDAxNTI5ODIzNjMzNjkw.h9ojChWC4UIIA0xpI3d2h3rhn99JzHbxZ8YxcjgOfZIg.ouprjLFVByfl7y1jCjQp85WcBpMCzg9doHJcsGS9LoEg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_3.51.53.png?type="><img src="https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMTAy/MDAxNTI5ODIzNjMzNjkw.h9ojChWC4UIIA0xpI3d2h3rhn99JzHbxZ8YxcjgOfZIg.ouprjLFVByfl7y1jCjQp85WcBpMCzg9doHJcsGS9LoEg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_3.51.53.png?type=w2" largesrc="javascript:location.href='https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMTAy/MDAxNTI5ODIzNjMzNjkw.h9ojChWC4UIIA0xpI3d2h3rhn99JzHbxZ8YxcjgOfZIg.ouprjLFVByfl7y1jCjQp85WcBpMCzg9doHJcsGS9LoEg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_3.51.53.png?type=w2'" id="img_1" data-top="401.66668701171875"></span>&nbsp;</p>

<p style="" _foo="text-align: left;" align="left">개발 프로젝트를 하는데 있어서 <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">규모에 상관없이 소스코드에 대한 관리는 중요</span>하다. <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">리눅스 환경에서는 소스 관리를 위해서 make 명령어를 사용</span>한다. <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">make는 소프트웨어 개발을 위해 유닉스, 리눅스 계열 운영 체제에서 주로 사용되는 프로그램 빌드 도구</span> 이다. 여러 파일들끼리의 의존성과 각 파일에 필요한 명령을 정의함으로써 프로그램을 컴파일 할 수 있으며 최종 프로그램을 만들 수 있는 과정을 서술할 수 있는 표준적인 문법을 가지고 있다. <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">특정 형식의 파일은 Makefile이고 make가 해석하여 프로그램 빌드를 수행</span>하게 된다. 아래는 make로 빌드 자동화를 하였을 경우 장점을 나타낸것이다.</p>

<p style="" _foo="text-align: center;" align="center"><span class="_img  fx" thumburl="https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfNTYg/MDAxNTI5ODI0NDE3MTM2.z0lvAOMwbsp0zYF-cOYUDb0MNLVVsRDqd8Hnd6VRcgEg.cNZUyjB_I7EB5l7W5nWBXUl7wOKRu3ZuhWYmBnLX1aIg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.13.03.png?type="><img src="https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfNTYg/MDAxNTI5ODI0NDE3MTM2.z0lvAOMwbsp0zYF-cOYUDb0MNLVVsRDqd8Hnd6VRcgEg.cNZUyjB_I7EB5l7W5nWBXUl7wOKRu3ZuhWYmBnLX1aIg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.13.03.png?type=w2" largesrc="javascript:location.href='https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfNTYg/MDAxNTI5ODI0NDE3MTM2.z0lvAOMwbsp0zYF-cOYUDb0MNLVVsRDqd8Hnd6VRcgEg.cNZUyjB_I7EB5l7W5nWBXUl7wOKRu3ZuhWYmBnLX1aIg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.13.03.png?type=w2'" id="img_2" data-top="862.7083740234375" style="visibility: visible;"></span>&nbsp;</p>

<p style="" _foo="text-align: left;" align="left"><span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">make는 소스의 일부가 변경된 경우에는 변경된 부분만 다시 컴파일하고 링크하여 컴파일 시간을 단축</span>한다. 따라서 <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">개발에 필요한 소스 관리가 상당히 편리하고 효율적</span>이다. 특히 방대한 양의 대형 프로젝트를 진행할 경우 <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">make 명령어의 모듈별 관리 기능은 상당한 장점</span>이다. C/C++의 경우 프로그램을 개발 시 헤더파일(.h)과 소스파일(.c/.cpp)을 분리해서 작업하는 것이 일반적이다. 이러한 경우에서 파일이 많을 경우 하나하나 컴파일을 하는 것은 비효율적이다. <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">따라서 make를 이용해서 효율적으로 컴파일 관리</span>를 해야한다.</p>


<p style="" _foo="text-align: left;" align="left"><b>* Makefile 구조</b></p>

<p style="" _foo="text-align: left;" align="left"><span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">Makefile은 make 명령으로 실행할 수 있도록 일련의 규칙을 가지고 작성되어지는 파일</span>이다. 본 포스팅에서는 C++ 프로젝트에 관련하여 예시로 사용하겠다.</p>

<p style="" _foo="text-align: left;" align="left"><span class="_img  fx" thumburl="https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMjk4/MDAxNTI5ODI1NDQ4NjE3.8TPWYrfQeDzO7Jv8q619x09k_1BoU5ElatbRc0XgXfEg.80F_W1bSekG9U9LatcHS0CEV2xlSk21-3erWGMQ1omIg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_2.51.46.png?type="><img src="https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMjk4/MDAxNTI5ODI1NDQ4NjE3.8TPWYrfQeDzO7Jv8q619x09k_1BoU5ElatbRc0XgXfEg.80F_W1bSekG9U9LatcHS0CEV2xlSk21-3erWGMQ1omIg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_2.51.46.png?type=w2" largesrc="javascript:location.href='https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMjk4/MDAxNTI5ODI1NDQ4NjE3.8TPWYrfQeDzO7Jv8q619x09k_1BoU5ElatbRc0XgXfEg.80F_W1bSekG9U9LatcHS0CEV2xlSk21-3erWGMQ1omIg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_2.51.46.png?type=w2'" id="img_3" data-top="1248.041748046875"></span>&nbsp;</p>

<p style="" _foo="text-align: left;" align="left">위와 같이 하나의 디렉터리에 소스파일들을 만들고 아래와 같이 컴파일을 하게 된다.</p>

<p style="" _foo="text-align: center;" align="center"><span class="_img  fx" thumburl="https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMjk2/MDAxNTI5ODI1NzE0OTQw.n4jWjPYo4kE1H4tDIOo7yCQROJ5A_gmKpwabYpepVpgg.mLYXssVU-9w_PLaBGPtzhcBvMwq5IVTqSqLRWdUTeQYg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.34.31.png?type="><img src="https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMjk2/MDAxNTI5ODI1NzE0OTQw.n4jWjPYo4kE1H4tDIOo7yCQROJ5A_gmKpwabYpepVpgg.mLYXssVU-9w_PLaBGPtzhcBvMwq5IVTqSqLRWdUTeQYg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.34.31.png?type=w2" largesrc="javascript:location.href='https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMjk2/MDAxNTI5ODI1NzE0OTQw.n4jWjPYo4kE1H4tDIOo7yCQROJ5A_gmKpwabYpepVpgg.mLYXssVU-9w_PLaBGPtzhcBvMwq5IVTqSqLRWdUTeQYg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.34.31.png?type=w2'" id="img_4" data-top="1509.0833740234375"></span>&nbsp;</p>

<p style="" _foo="text-align: left;" align="left">1~3 까지의 과정을 거쳐 프로그램을 실행하게 된다. <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">Makefile이 전체적으로 컴파일 과정에 대해서는 관리를 해주고 있는데 만약 Makefile에 의해 관리가 되지 않는다면 개발자는 파일 내용이 수정되거나 컴파일을 해야 할 경우 1~3까지 하나씩 명령을 입력</span>해야 한다. 만약 프로젝트 <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">규모가 대규모라면 하나씩 처리하면서 하게 될 경우, 실수도 발생하게 되고 상당히 비효율적</span>이게 된다. 위와 같은 컴파일 구조를 Makefile로 관리하는 방법을 아래 단계별로 알아보겠다.</p>

<p style="" _foo="text-align: left;" align="left"><b>(1) Makefile 생성</b></p>

<p style="" _foo="text-align: left;" align="left"><span class="_img  fx" thumburl="https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMjM0/MDAxNTI5ODI1MjI0NDcy.Kut9t7vbnINM4i7nBvwFWp7WfYrL1cMFCMHr9bB1jPAg.pno0iaxSZGWBpKuPN6QjMEjAMCWv3T_8IvjOB6xRD8sg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.26.34.png?type="><img src="https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMjM0/MDAxNTI5ODI1MjI0NDcy.Kut9t7vbnINM4i7nBvwFWp7WfYrL1cMFCMHr9bB1jPAg.pno0iaxSZGWBpKuPN6QjMEjAMCWv3T_8IvjOB6xRD8sg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.26.34.png?type=w2" largesrc="javascript:location.href='https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMjM0/MDAxNTI5ODI1MjI0NDcy.Kut9t7vbnINM4i7nBvwFWp7WfYrL1cMFCMHr9bB1jPAg.pno0iaxSZGWBpKuPN6QjMEjAMCWv3T_8IvjOB6xRD8sg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.26.34.png?type=w2'" id="img_5" data-top="2159.70849609375"></span>&nbsp;</p>

<p style="" _foo="text-align: left;" align="left">Makefile은 <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">vim을 이용</span>해서 생성한다. Makefile로 파일 이름을 만들 경우 <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">리눅스에서 자동으로 관리</span>를 해주게 된다.</p>

<p style="" _foo="text-align: left;" align="left">Makefile은 <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">vim을 이용</span>해서 생성한다. Makefile로 파일 이름을 만들 경우 <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">리눅스에서 자동으로 관리</span>를 해주게 된다.</p>

<p style="" _foo="text-align: left;" align="left"><b>(2) Makefile 작성</b></p>

<p style="" _foo="text-align: left;" align="left"><span class="_img  fx" thumburl="https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMTk0/MDAxNTI5ODI2NTQ0NzU3.-kllZ_g0QlkkyjXmWqJiy64RXn95cgvPaoojCYeLKBUg.hhGX_BP6_1qTR3lj9VgPf_omXDHL9JGevXV5u-jQgiog.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.47.23.png?type="><img src="https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMTk0/MDAxNTI5ODI2NTQ0NzU3.-kllZ_g0QlkkyjXmWqJiy64RXn95cgvPaoojCYeLKBUg.hhGX_BP6_1qTR3lj9VgPf_omXDHL9JGevXV5u-jQgiog.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.47.23.png?type=w2" largesrc="javascript:location.href='https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMTk0/MDAxNTI5ODI2NTQ0NzU3.-kllZ_g0QlkkyjXmWqJiy64RXn95cgvPaoojCYeLKBUg.hhGX_BP6_1qTR3lj9VgPf_omXDHL9JGevXV5u-jQgiog.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.47.23.png?type=w2'" id="img_6" data-top="2329.70849609375"></span>&nbsp;</p>

<p style="" _foo="text-align: left;" align="left">위와 같이 Makefile을 작성한다. 각 번호는 규칙을 의미하므로 하나씩 알아보겠다.</p>

<p style="" _foo="text-align: left;" align="left"><b>1) Target :&nbsp;</b></p>

<p style="" _foo="text-align: left;" align="left"><span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">실행파일, Object 파일, 라이브러리 등 목적 규칙을 정의</span>한다. <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">3)의 실행결과로 만들어지는 파일을 의미</span>한다. 생성파일이나 install 같은 기능적 블록도 사용가능하다.</p>

<p style="" _foo="text-align: left;" align="left"><b>2) Dependency, Prerequisites :&nbsp;</b></p>

<p style="" _foo="text-align: left;" align="left"><span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">Target을 만들 때, 의존성(연관관계)를 규정</span>한다. 의존성을 규정한 파일들 중 수정된 파일이 있으면 Target을 다시 만든다.</p>

<p style="" _foo="text-align: left;" align="left"><b>3) Recipe :&nbsp;</b></p>

<p style="" _foo="text-align: left;" align="left"><span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">Target을 만들기 위한 실행 파일</span>이다. 해당 실행규칙에 따라 Target이 생성된다. 해당 부분에는 리눅스 명령어를 이용해서 작성한다. 명령구문은 여러개가 올 수 있다. <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">작성 시 주의사항은 구분하기 위해서 TAB키를 이용해서 들여쓰기를 해야한다는 점</span>이다. TAB키 말고 다른 키로 구분을 할 경우 make 시 정상적으로 수행되지 않는다.</p>

<p style="" _foo="text-align: left;" align="left"><b>4) Macro :&nbsp;</b></p>

<p style="" _foo="text-align: left;" align="left"><span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">반복적인 구문은 매크로를 이용해서 효율적으로 작성</span>할 수 있다. C언어에서 #define과 같은 경우이다. <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">매크로를 사용할 경우 $(MACRO_NAME)을 이용</span>하면 된다. 또한 <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">사용할려는 구문보다 앞서서 정의</span>가 되어야 한다.</p>

<p style="" _foo="text-align: left;" align="left"><b>5) Dummy Target :</b></p>

<p style="" _foo="text-align: left;" align="left">더미타켓은 의존성 파일들을 정의하지 않아서 파일을 생성하지 않는다. 대신, <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">make로 명령을 실행 시 생성되는 Target파일들을 제거해주는 용도</span>로 사용된다. <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">make를 수행 전 안전하게 파일들을 제거하고 다시 새롭게 하기 위한 용도</span>로 사용된다. 명령은 'make clean' 을 이용한다.</p>

<p style="" _foo="text-align: left;" align="left">이 밖에도 다양한 문법요소, 규칙들이 있지만 생략하겠다.&nbsp;</p>

<p style="" _foo="text-align: left;" align="left"><b>(3) Makefile 실행</b></p>

<p style="" _foo="text-align: left;" align="left">작성된 Makefile을 실행시키기 위해서는 <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">make 명령</span>이 필요하다.&nbsp;</p>

<p style="" _foo="text-align: left;" align="left"><span class="_img  fx" thumburl="https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMjg4/MDAxNTI5ODI3Njc4NjQ5.M6KSEDzi2oyS4JcAbwmW2uS9S4C0qp96JckvnrCQqKIg.ATNWC-zt2iwgc7TTSF0JxTa2Plsu42ifdXb9lpIcpqcg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.33.39.png?type="><img src="https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMjg4/MDAxNTI5ODI3Njc4NjQ5.M6KSEDzi2oyS4JcAbwmW2uS9S4C0qp96JckvnrCQqKIg.ATNWC-zt2iwgc7TTSF0JxTa2Plsu42ifdXb9lpIcpqcg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.33.39.png?type=w2" largesrc="javascript:location.href='https://mblogthumb-phinf.pstatic.net/MjAxODA2MjRfMjg4/MDAxNTI5ODI3Njc4NjQ5.M6KSEDzi2oyS4JcAbwmW2uS9S4C0qp96JckvnrCQqKIg.ATNWC-zt2iwgc7TTSF0JxTa2Plsu42ifdXb9lpIcpqcg.PNG.scw0531/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2018-06-24_%EC%98%A4%ED%9B%84_4.33.39.png?type=w2'" id="img_7" data-top="3480.229248046875"></span>&nbsp;</p>

<p style="" _foo="text-align: left;" align="left">처음 ls를 한 결과 vim 으로 생성한 Makefile을 볼 수 있다. make 명령을 이용해서 Makefile에 정의했던 순서대로 명령을 실행하여 파일을 만든다. 로그를 보면 g++을 이용해서 cal.cpp을 컴파일하고 해당 결과인 오브젝트 파일을 가지고 다시 main.cpp와 컴파일을 하여 main이라는 실행파일을 만든다. 다시 ls 한 결과 main 실행파일을 확인할 수 있다. <span style="color: rgb(255, 0, 0);" _foo="color: rgb(255, 0, 0);">만약 파일을 아무런 수정작업 없이 다시 make를 시도할 경우 바뀔 것이 없기에 아무런 작업을 수행하지 않는다. 만약 의존성에 정의된 파일 중 수정이 된 부분이 있다면 수정된 부분만 다시 컴파일을 수행</span>하게 된다. 최종적으로 실행파일을 실행시켜 결과를 얻는다. 효율적으로 작업이 가능하다.&nbsp;</p>






### References
<https://m.blog.naver.com/PostView.nhn?blogId=scw0531&logNo=221305718407&proxyReferer=https:%2F%2Fwww.google.com%2F>
<https://bowbowbow.tistory.com/12>