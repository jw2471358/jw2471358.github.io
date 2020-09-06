---
layout: post
title: Shell script
subtitle: 
description: Shell script
# image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/pixabay/me-nots-5302712_1920_ktf3cg.jpg
category: linux
tags:
  - Shell script
author: jw2471358
---

#### 인자 및 분기 처리

```
# 첫번째 인자 값을 변수명 carName에 저장합니다.
# 변수에 할당할 때 =기호 앞뒤로 공백이 없어야 합니다.
# $1 또는 ${1}는 Shell Script Name뒤 첫번째 인자를 의미합니다.
carName=${1}

# 입력된 자동차명을 출력합니다.
echo input car is ${carName}
# ${변수:위치:길이} 형태로 자동차명 앞 1자리를 benzClass변수에 저장합니다.
benzClass=${carName:0:1}
# 벤츠클래스를 출력합니다.
echo car class is ${benzClass}

# 조건문은 "if...elif...else...fi" 형태입니다.
# if, elif와 대괄호[ 사이 꼭 공백이 있어야 합니다.
# 대괄호[ 뒤에 공백, 대괄호] 앞에 공백이 있어야 합니다.
# == 앞뒤로 공백이 있어야 합니다.
# 문자열 비교 시 같음은 ==, 다름은 !=을 사용합니다. 참고로 숫자 같음은 -eq, 다름은 -ne입니다.
if [ "${benzClass}" == "C" ]; then # C클래스이면
    echo "Compact Class" 
elif [ "${benzClass}" == "E" ]; then # E클래스이면
    echo "Executive Class"
elif [ "${benzClass}" == "S" ]; then # S클래스이면
    echo "Special Class" 
else # 모두 아니면
    echo "No information" 
fi # if문 종료
```

출처 : https://m.blog.naver.com/wideeyed/221524148361


#### Shell Script 파일 존재 유무 문법

[~]# vi test.sh
```
#!/bin/sh
#
#
## 변수 선언
##
FILE1=/usr/local/file.tar

## 디렉토리명 파일 직적 선택
##
if [ -f /usr/loca/file.tar ]; then
    echo "file.tar exists!"
else 
    echo "file.tar not exists!"
fi

## 변수 이용
##
if [ -f $FILE1 ]; then
    echo "$FILE1 exists!"
else 
    echo "$FILE1 not exists!"
fi
```

출처: https://itposting.tistory.com/35 [IT 관련 포스팅]

