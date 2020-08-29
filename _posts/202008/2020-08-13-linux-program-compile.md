---
layout: post
title: Linux 프로그램과 컴파일
subtitle: 
description: Linux 프로그램과 컴파일
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/pixabay/four-spotted-dragonfly-1811835_1920_mlxgz4.jpg
category: linux
tags:
  - linux 프로그램
  - 컴파일
author: jw2471358
---

### 프로그램 작성과 컴파일

#### 단일 모듈 프로그램 컴파일

$ gcc [-옵션] 파일
C 프로그램을 컴파일한다. 옵션을 사용하지 않으면 실행파일 a.out 를 생성한다.

```
$ gcc long.c
```

컴파일하여 목적 파일을 생성한다.
```
$ gcc -c long.c 
```

목적 파일로부터 실행파일을 만들기 위해서는 -o 옵션을 사용한다.
```
$ gcc -o long long.o
$ long
```

혹은 목적 파일을 만들고 실행 파일을 만드는 이 두 과정을 단번에 할 수 있다.
```
$ gcc -o long long.c 
```

또한 -S 옵션을 사용하여 어셈블리 프로그램 long.s 파일을 생성한다.
```
$ gcc -S long.c 
```

-l 옵션을 이용하여 특정 라이브러리를 링크할 수 있다.
-lxxx 는 (보통 /usr/lib 디렉토리에 있는) 라이브러리 libxxx.a를 링크하라는 의미이다.
예를 들어, test.c 프로그램이 수학 라이브러리(libm.a)를 사용한다면 
다음과 같이 -lm 옵션을 이용하여 -libm.a을 링크할 수 있다.
```
$ gcc -o test -lm test.c 
```

#### 다중 모듈 프로그램

main.c
```c
#include <stdio.h>
#include "copy.h"

char line[MAXLINE];  	// 입력 줄
char longest[MAXLINE]; 	// 가장 긴 줄

/* 입력 줄 가운데 가장 긴 줄을 프린트한다. */
main()
{
    int len;
    int max;

    max = 0;

    while (gets(line) != NULL) {
        len = strlen(line);
        if (len > max) {
            max = len;
            copy(line, longest);
        }
    }

    if (max > 0)   // 입력 줄이 있었다면
       printf("%s", longest);

   return 0;
}
```

copy.h 
```c
#define MAXLINE 1000 /* maximum input line length */
void copy(char from[], char to[]);
```

copy.c 
```c
#include <stdio.h>
#include "copy.h"

/* copy: copy 'from' into 'to'; assume to is big enough */
void copy(char from[], char to[])
{
   int i;

   i = 0;
   while ((to[i] = from[i]) != '\0')
       ++i;
} 
```

```
$ gcc -o main main.c copy.c 
$ main 
```
