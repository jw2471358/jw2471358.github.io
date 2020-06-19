---
layout: post
title: 전자정부프레임워크
subtitle: 
description: 전자정부프레임워크
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_599,q_auto,w_700/v1592202880/me/%EC%A0%84%EC%9E%90%EC%A0%95%EB%B6%80%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC_%EA%B5%AC%EC%84%B1_gkyjbp.jpg
category: 전자정부프레임워크
tags:
  - 전자정부프레임워크
author: jw2471358
---


[표준프레임워크 공통컴포넌트 v3.8 가이드](https://www.egovframe.go.kr/wiki/doku.php?id=egovframework:com:v3.8:init)


### 하이브리드 앱
폰갭은 구축하신 모바일 웹페이지를 네이티브앱 형태로 감싸주는 역할을 합니다.
네이티브앱에 구축하신 모바일 웹페이지를 웹뷰로 보여주는 형태지요.
웹뷰에 메인화면 띄워주면 그 뒤에 로직은 그냥 모바일웹에서 구현하신 방법으로 실행되는거..

폰갭은 웹뷰안에서 디바이스 내의 고유 기능(카메라, 마이크 제어 등)을 쓸 수 있게 만들어주는 솔루션

### 모바일 디바이스 API 실행환경
#### 구성
모바일 디바이스 API는 각 플랫폼(Android, iOS) 별 구현환경 위에서 HTML, CSS, JavaScript 로 구성된웹 리소스를 통한 디바이스 하이브리드 어플리케이션 구현을 지원하며 플랫폼 별 SDK를 활용하여 구현된 웹 리소스 내의 JavaScript 형태의 Device API와 각 플랫폼 별 `Native Code` 가 `하이브리드 프레임워크` 및 `웹뷰 인터페이스`를 통해 연동되어 실제 디바이스의 고유 기능을 호출할 수 있도록 지원한다.

![placeholder](https://www.egovframe.go.kr/images/egovframework/adt_new/img_sub03_06_01.jpg)


#### 전자정부프레임워크에서 하이브리드 앱 개발을 위한 폰갭 정의
<https://www.egovframe.go.kr/wiki/doku.php?id=egovframework:hyb3.5:hrte:phonegap>

#### 모바일공통 컴포넌트
<https://www.egovframe.go.kr/wiki/doku.php?id=egovframework:mcom>

