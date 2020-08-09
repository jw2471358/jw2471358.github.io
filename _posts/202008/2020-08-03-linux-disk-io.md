---
layout: post
title: Linux에서 DISK I/O 사용량 확인
subtitle: 
description: Linux에서 DISK I/O 사용량 확인
# image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/pixabay/moon-5224745_1920_ufjpll.jpg
category: Linux
tags:
  - Linux DISK I/O
author: jw2471358
---

Linux에서 DISK I/O 사용량을 확인하기 위한 가장 기본 적인 방법은 iostat 명령이며 기본적으로 설치되는 도구이다.

만약 이 도구가 설치되어 있지 않다면 sysstat 패키지를 설치하여 사용할 수 있다.

sudo apt-get install sysstat 

기본적으로 이 명령은 장치와 파티션에 대한 CPU 및 I/O 통계에 대한 두 개의 정보를 표시하지만 -c 및 –d 옵션을 사용하면 CPU 또는 Disk 정보만 표시하도록 할 수 있다. 위의 그림에서 보면 설치된 장치에 대해 초당 전송(tps), 초당 읽기 및 쓰기(KB), 읽기 및 쓰기의 (KB) 정보가 나타난다.

iostat 명령을 실행하면 명령이 실행된 순간의 데이터만 나타나지만 반복 시간을 설정하면 지정된 간격(초단위)로 계속 정보를 표시할 수 있다. 아래 명령은 4초 간격으로 Disk의 I/O 정보만 표시되록 한다.

iostat –d 4

![placeholder](https://mblogthumb-phinf.pstatic.net/MjAxNzA2MDlfMTYx/MDAxNDk2OTQ1NDc3MDk5.El8j--EYagq-aFc5YsVUF-u04cGoGeM2CbUYauvDNwYg.OQybnEivheGaZd1am8mZZ3OfBijoD97nDDcs8INrnOgg.PNG.jevida/060817_1811_LinuxDISKI2.png?type=w2)

그림을 보면 4초 간격으로 Disk I/O 데이터를 나타내며 읽기/쓰기에 대한 정보는 이전 실행값과 비교한 델타 값이 표시된다. [Ctrl + C]를 누를때 까지 지정된 간격으로 데이터를 표시 한다.

 

iostat과 함께 –x 옵션을 사용하면 더 많은 정보를 보여준다. 가장 유용한 정보는 평균 대기열 길이 인 avgqu-sz 정보를 보여준다.

iostat –xd

![placeholder](https://mblogthumb-phinf.pstatic.net/MjAxNzA2MDlfNTQg/MDAxNDk2OTQ1NDc4MjU3.xB6edJgrWNsscH2zhC57ImjBKP97XBUotfXmncn0yQMg.zdO9C7mV4AZ9h8nsdGYi0MdRoqvSRfV9a4mtMM9nJDMg.PNG.jevida/060817_1811_LinuxDISKI3.png?type=w2) 

- rrqm/s : 장치에 대기중인 초당 읽기 요청 수
- wrqm/s : 장치에 대기중인 초당 쓰기 요청 수
- r/s : 초당 읽기 요청 수
- w/s : 초당 쓰기 요청 수
- rkB/s : 초당 읽기 KB
- wkB/s : 초당 쓰기 KB
- avgrq-sz : 요청의 평균 크기(섹터 단위)
- avgqu-sz : 요청의 평균 대기열 길이
- await : I/O 요청의 평균 시간(ms). 이 정보는 대기열 요청 시간과 대기열에 대기하는 시간이 포함
- r_await : 서비스 요청을 받은 장치에 대한 읽기 요청의 평균 시간(ms). 대기열 요청 시간과 대기열에 대기하는 시간이 포함
- w_await : 장치에 제공되는 쓰기 요청의 평균 시간(ms). 이 정보는 대기열 요청 시간과 대기열에 대기하는 시간이 포함
- svctm : 장치에 발급 된 I/O 요청의 평균 시간(ms) (향후 제거되므로 사용하지 말것)
- %util : I/O 요청이 장치에 발급된 동안의 CPU %. 이 수치가 100%에 가까울 수록 오버헤드 발생
 

iotop 명령은 프로세스 또는 스레드당 I/O 사용량을 나타내며 htop 유틸리티와 비슷한 형식으로 표시 한다.

iotop 

만약 해당 명령문이 실행되지 않으면 package 를 설치 한다.

sudo apt-get install iotop

![placeholder](https://mblogthumb-phinf.pstatic.net/MjAxNzA2MDlfMTQx/MDAxNDk2OTQ1NDc5OTA0.k_4eimqfyV10JpXsPycZErobx_COfQP599MQwzfSKc4g.MC87Fk4LMhdlyr_l-53o6bsn1NEWPjFogL8AkPZS5hsg.PNG.jevida/060817_1811_LinuxDISKI4.png?type=w2) 

위 그림을 보면 DISK에 대한 스왑 및 프로세스의 총 I/O 정보를 표시한다. Iotop에 다양한 매개 변수를 사용하여 더 많은 정보를 볼 수 있다.

- -o : 모든 프로세스 또는 스레드를 표시하는 대신 실제로 I/O를 수행하는 프로세스 또는 스레드만 표시
- -b : 배치 모드로 작동. 시간 경과에 따른 I/O 사용량 로깅에 유용
- -P : 프로세스만 표시 (일반적으로 iotop은 모든 스레드를 표시)
- -a : 누적된 I/O 대역폭 표시. 이 모드는 iotop이 시작된 이후에 수생한 I/O 프로세스의 양을 보여준다
 

iotop 실행 상태에서 키보드 단축키를 사용하여 표시 방법를 변경할 수도 있다.

- Left and right arrow(방향키) : 정렬 열을 변경
- r : 정렬 순서를 반대로 표시
- : 실제로 I/O를 수행하는 프로세스 또는 스레드만 표시
- p : 스레드 대신 프로세스 표시
- a : 누적 된 I/O 대역푝 표시
- I : 스레드 또는 프로세스의 우선순위 변경
 
### References

https://m.blog.naver.com/PostView.nhn?blogId=jevida&logNo=221024972067&proxyReferer=http:%2F%2Fwww.google.com%2F