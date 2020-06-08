---
layout: post
title: github pages 에 google analytics 추가하기
subtitle: 
description: github pages 에 google analytics 추가하기
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_760/v1591001871/dev/google_analytics_u6y98p.jpg
category: google analytics
tags:
  - github pages
  - google analytics
author: jw2471358
---

GitHub 페이지 사이트에 Google 웹 로그 분석 추적을 추가하는 방법.

먼저 Google 웹 로그 분석으로 이동하여 가입하십시오.  
관리자 페이지로 연결됩니다.  
그러면 사이트의 각 페이지에 추가해야하는 추적 코드가 제공됩니다.  
```javascript
<script>
    (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
    (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
    m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','//www.google-analytics.com/analytics.js','ga');
    ga('create', 'UA-########-#', 'auto');
    ga('send', 'pageview');
</script>
```

Jekyll은 이것을 쉽게 추가 할 수 있습니다. 이 코드가 포함 된 _includes 폴더 에 HTML 파일을 만듭니다 . 내 이름을 google_analytics.html로 지정했습니다. 그런 다음 기본 레이아웃에 다음을 추가하십시오 _layouts/default.html.  

{% include google_analytics.html %}  
\{\% include google_analytics.html %\}  

몇 시간 내에 Google 애널리틱스에서 변경 사항을 확인하면 세션 시간, 인구 통계 및 기타 사이트 방문자에 대한 유용한 정보를 캡처하게 됩니다.

### References
https://www.christopherlovell.co.uk/blog/2015/04/13/google-analytics-ghpages.html