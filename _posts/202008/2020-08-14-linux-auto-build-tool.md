---
layout: post
title: Linux 자동 빌드 도구
subtitle: 
description: Linux 자동 빌드 도구
# image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/pixabay/moon-5224745_1920_ufjpll.jpg
category: linux
tags:
  - linux 자동 빌드 도구
  - Makefile
author: jw2471358
---

### 자동 빌드 도구

#### make 시스템
make 시스템을 사용하여 실행 파일을 관리하기 위해서는 먼저 메이크파일을 만들어야 하는데, 
이 파일에 실행 파일을 만들기 위해 필요한 파일들과 그들 사이의 의존 관계, 만드는 방법 등을 기술한다. 

>$ make [-f 메이크파일]  
make 시스템은 메이크파일(makefile 혹은 Makefile)을 이용하여 보통 실행 파일을 빌드한다. 
옵션을 사용하여 별도의 메이크파일을 지정할 수 있다.

#### 메이크파일
makefile, Makefile, .make, .mk 

메이크 파일의 일반적인 구성 형식

```
목적(target): 의존리스트(dependencies)  
    명령리스트(commands)
```

목표는 생성하고자 하는 목표 파일(일반적으로 목적 파일 혹은 실행 파일)이고, 
의존리스트는 목표 파일을 생성하기 위해 필요한 파일들이며, 
명령리스트는 목표 파일을 생성하기 위한 일련의 명령들이다.
명령리스트 줄은 탭(tab) 문자로 들여쓰기 해야 한다.

예를 들어, 다음 Makefile은 실행파일 main을 만들기 위해서는 main.o와 copy.o가 필요하며, 
만드는 방법은 gcc -o main main.o copy.o 명령이라는 점을 나타내고 있다. 
또한 main.o을 만들기 위해서는 main.c와 copy.h가 필요하며 만드는 방법은 
gcc -c main.c 명령이며 copy.o을 만들기 위해서는 copy.c가 필요하며 
만드는 방법은 gcc -c copy.c 명령이라는 점을 나타내고 있다.

Makefile
```
main: main.o copy.o 
    gcc -o main main.o copy.o 
main.o: main.c copy.h 
    gcc -c main.c 
copy.o:copy.c 
    gcc -c copy.c 
```

```
            main 
     main.o        copy.o  
main.c   copy.h    copy.c  
```
파일 의존 그래프

#### make 시스템 실행

make 시스템을 실행시키면 Makefile을 이용하여 실행파일 main을 생성하게 되는데 
Makefile에 기술된 의존 관계에 따라 먼저 main.o와 copy.o를 생성한 후에 실행파일 main를 최종적으로 생성한다.

```
$ make 혹은 $ make main 
gcc -c main.c 
gcc -c copy.c 
gcc -o main main.o copy.o 
```

만일 copy.c 파일이 변경된 후에 다시 make 시스템을 실행시키면 make 시스템은 파일 사이의 
의존 관계를 파악하여 이번에는 copy.o만을 새로 생성하고 이를 이용하여 실행 파일 main 을 다시 생성한다. 

```
$ make 
gcc -c copy.c 
gcc -o main main.o copy.o 
```