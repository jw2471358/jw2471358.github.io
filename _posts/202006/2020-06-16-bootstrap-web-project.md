---
layout: post
title: bootstrap 프레임워크로 웹 프로젝트 만들기
subtitle: 
description: bootstrap 프레임워크로 웹 프로젝트 만들기
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_599,q_auto,w_700/v1592202880/pixabay/skateboard-5221914_1920_gmxuzw.jpg
category: bootstrap
tags:
  - bootstrap
author: jw2471358
---

### bootstrap
부트스트랩은 웹사이트를 쉽게 만들 수 있게 도와주는 HTML, CSS, JS 프레임워크이다. 하나의 CSS 로 휴대폰, 태블릿, 데스크탑까지 다양한 기기에서 작동한다. 다양한 기능을 제공하여 사용자가 쉽게 웹사이트를 제작, 유지, 보수할 수 있도록 도와준다.

### bootstrap 을 이용한 간단 웹 프로젝트 만들기 (4강)

1. eclipse-mars > New > Dynamic Web Project : bs_simple

2. WebContent 폴더 하위에 css, js 폴더를 만든다.

3. bootstrap download 하여 css 폴더에 넣는다. (bootstrap.min.css)
	<https://getbootstrap.com/docs/4.5/getting-started/download/>  
	Compiled CSS and JS  
	Download (bootstrap-4.5.0-dist.zip)

4. jquery download 또는 script를 복사하여 js 폴더에 넣는다. (jquery.min.js)
	<https://jquery.com/download/>  
	Download the compressed, production jQuery 3.5.1

5. popper.js download 하여 js 폴더에 넣는다. (popper.min.js)
	<https://unpkg.com/@popperjs/core@2>  
	navigation bar의 색상을 바꾼다.  
	custom.css를 사용하여 bootstrap.min.css를 overriding 하여 만든다.

6. 웹폰트 설정하기
	<https://fonts.google.com/earlyaccess>  
	Jeju Gothic 와 Nanum Gothic (Korean)  
	아래 Link를 복사하여 custom.css 에 넣는다.  
	Link  
	@import url(//fonts.googleapis.com/earlyaccess/jejugothic.css);  
	@import url(//fonts.googleapis.com/earlyaccess/nanumgothic.css);  
	custom.css
	```css
	@import url(https://fonts.googleapis.com/earlyaccess/jejugothic.css);
	@import url(https://fonts.googleapis.com/earlyaccess/nanumgothic.css);
	.navbar-brand, h1, h2, h3, h4 {
	    font-family: 'Jeju Gothic';
	}
	h5 {
	    font-family: 'Jeju Gothic';
	    font-size: 18px;
	}
	body {
	    font-family: 'Nanum Gothic';
	}
	```

7. WebContent 에 index.jsp 파일을 만든다.
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
<title>강의평가 웹 사이트</title>
<!-- 부트스트랩 css 추가하기 -->
<link rel="stylesheet" href="./css/bootstrap.min.css">
<!-- 부트스트랩 css 추가하기 -->
<link rel="stylesheet" href="./css/custom.css">
</head>
<body>
	<nav class="navbar navbar-expand-lg navbar-light bg-light">
		<a class="navbar-brand" href="index.jsp">강의평가 웹 사이트</a>
		<button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbar">
			<span class="navbar-toggle-icon"></span>
		</button>
		<div id="navbar" class="collapse navbar-collapse">
		    <ul class="navbar-nav mr-auto">
		        <li class="nav-item active">
		            <a class="nav-link" href="index.jsp">메인</a>
		        </li>
		        <li class="nav-item dropdown">
		            <a class="nav-link dropdown-toggle" id="dropdown" data-toggle="dropdown">
		                회원관리
		            </a>
		            <div class="dropdown-menu" aria-labelledby="dropdown">
		                <a class="dropdown-item" href="#">로그인</a>
		                <a class="dropdown-item" href="#">회원가입</a>
		                <a class="dropdown-item" href="#">로그아웃</a>
		            </div>
		        </li>
		    </ul>
		    <form class="form-control mr-sm-2" type="search" placeholder="내용을 입력하세요." aria-label="Search">
		        <button class="btn btn-outline-succes my-2 my-sm-0" type="submit">검색</button>
		    </form>
		</div>
	</nav>
	<script src="./js/jquery.min.js"></script>
	<script src="./js/popper.min.js"></script>
	<script src="./js/bootstrap.min.js"></script>
</body>
</html>
```

### References
<https://www.youtube.com/watch?v=lN1HCaPJ-jE>