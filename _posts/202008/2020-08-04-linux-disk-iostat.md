---
layout: post
title: 리눅스 디스크 모니터링 - iostat i/o 모니터링
subtitle: 
description: 리눅스 디스크 모니터링 - iostat i/o 모니터링
# image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/pixabay/moon-5224745_1920_ufjpll.jpg
category: Linux
tags:
  - Linux iostat i/o 모니터링
author: jw2471358
---

![placeholder](https://t1.daumcdn.net/cfile/tistory/2542DF3D58CA443A1B)

### iostat 모니터링

iostat는 디스크 입출력 대한 통계를 보고하고 처리량, 사용률, 대기열 길이, 드랜잭션 비율 및 서비스 시간에 대한 측정 결과를 알수 있는 프로그램이입니다.

평소 디스크에 베드 섹터라든지 이상이 없는데, 서버의 부하가 평소보다 높을 경우에 디스크 사용량을 알수 있습니다.

또한 간단한 명령어 한줄로 디스크 처리의 입출력 통계 및 처리량, 대기열 길이등을 실시간으로 모니터링 할수 있습니다.

### iostat 설치

```
1 [root@web /]# yum -y install sysstat
```

### iostat 출력 정보

#### CPU의 사용자원 출력 정보

- %user - CPU가 사용자 모드에서 사용된 시간의 비율의 출력값 입니다.
- %nice - 작업 우선순위 정책에 의하여 우선순위가 바뀐 프로세서가 사용한 시간의 비율을 출력하값 입니다.
- %system - CPU가 시스템 모드에서 사용된 시간의 비율을 출력한 값 입니다.
- %iowait - 디스크의 입출력을 대기하는데 사용된 시간의 비율을 출력한 값 입니다.
- %steal - Steal CPU의 사용시간을 비율로 출력한 값 입니다.
- %idle - 디스크의 입출력을 대기하지 않은 유휴상태의 시간을 출력한 값 입니다.

#### 디스크 장치의 활용량 출력 정보
- tps - 디스크 장치에서 초단 처리한 입출력의 잡업 개수 입니다.
- kB-read/s - 디스크 장치에서 초당 읽어들인 데이터 블록 단위 입니다.
- kB_wrtn/s - 디스크 장치에서 초당 쓴 데이터 블록 단위 입니다.
- kB_wrtn - 디스크 장치에서 쓴 데이터 블록 단위

### IOSTAT 사용법

#### iostat 명령어 : istat [옵션] [출력시간] [횟수]

iostat는 출력될 결과는 대부분 시간(출력될 시간)가 횟수(총 출력된 시간)를 숫자로 지정하여 사용합니다.

#### CPU 정보를 출력

명령어 : iostat -c [출력시간] [횟수]

```
 1 [root@web /]# iostat -c 1 3
 2 Linux 2.6.32-642.13.1.el6.x86_64 (web.server)   2017년 03월 16일   _x86_64_  (1 CPU)
 3 
 4 avg-cpu:  %user   %nice %system %iowait  %steal   %idle
 5            0.04    0.00    0.14    0.10    0.00   99.72
 6 
 7 avg-cpu:  %user   %nice %system %iowait  %steal   %idle
 8            0.00    0.00    0.00    0.00    0.00  100.00
 9  
10 avg-cpu:  %user   %nice %system %iowait  %steal   %idle
11            0.00    0.00    0.98    0.00    0.00   99.02
```

- %user - 유저가 사용한 프로세스가 사용된시간(백분율)
- %nice - 자업 우선순위가 바뀐 프로세스가 사용된 시간 입니다.
- %system - 시스템이 작동한 시간입니다.
- %iowait - 입출력(I/O) 대기시간(%idle과 다르며 iowait가 높은경우 메모리 부족이나 비효율적인 I/O부시스템이 구성되어 있음을 의미합니다.)
- %steal - Steal CPU의 작동 시간
- %idle - 입출력(I/O) 대기시간(%idle과는 다르며 ioswait가 높은경우 메모리 부족이나 비효율적인 I/O부 시스템이 구성되어 있음을 의미합니다.)

#### 디스크 장치의 입출력 정보 출력

명령어 : iostat -d [출력시간] [횟수]

```
 1 [root@web /]# iostat -d 1 3
 2 Linux 2.6.32-642.13.1.el6.x86_64 (web.server)   2017년 03월 17일   _x86_64_  (1 CPU)
 3 
 4 Device:            tps   Blk_read/s   Blk_wrtn/s   Blk_read   Blk_wrtn
 5 scd0              0.00         0.02         0.00        264          0
 6 sda               0.75        21.61         7.80     303458     109580
 7 
 8 Device:            tps   Blk_read/s   Blk_wrtn/s   Blk_read   Blk_wrtn
 9 scd0              0.00         0.00         0.00          0          0
10 sda               0.00         0.00         0.00          0          0
11  
12 Device:            tps   Blk_read/s   Blk_wrtn/s   Blk_read   Blk_wrtn
13 scd0              0.00         0.00         0.00          0          0
14 sda               0.00         0.00         0.00          0          0
```

- tps - 디스크 장치에서 초당 처리한 입출력의 잡업 개수 입니다.
- kB-read/s - 디스크 장치에서 초당 읽어들인 데이터 블록 단위 입니다.
- kB_wrtn/s - 디스크 장치에서 초당 쓴 데이터 블록 단위 입니다.
- kB_wrtn - 디스크 장치에서 쓴 데이터 블록 단위 입니다.

#### 지정된 디스크 장치의 정보 출력

명령어 : iostat -p  /dev/장치명

```
 1 [root@web /]# iostat -p /dev/sda
 2 Linux 2.6.32-642.13.1.el6.x86_64 (web.server)   2017년 03월 17일   _x86_64_  (1 CPU)
 3  
 4 avg-cpu:  %user   %nice %system %iowait  %steal   %idle
 5            0.02    0.00    0.11    0.06    0.00   99.80
 6 
 7 Device:            tps   Blk_read/s   Blk_wrtn/s   Blk_read   Blk_wrtn
 8 sda               0.61        16.97         6.34     303458     113428
 9 sda1              0.03         0.26         0.00       4636         28
10 sda2              0.03         0.26         0.00       4698         24
11 sda3              0.03         0.28         0.01       5066         96
12 sda4              0.00         0.00         0.00          4          0
13 sda5              0.03         0.26         0.00       4698         24
14 sda6              0.32         9.60         5.59     171570     100024
15 sda7              0.02         0.16         0.00       2904          0
16 sda8              0.13         6.08         0.74     108642      13232
```

- %user - 유저가 사용한 프로세스가 사용된시간(백분율)
- %nice - 자업 우선순위가 바뀐 프로세스가 사용된 시간 입니다.
- %system - 시스템이 작동한 시간입니다.
- %iowait - 입출력(I/O) 대기시간(%idle과 다르며 iowait가 높은경우 메모리 부족이나 비효율적인 I/O부시스템이 구성되어 있음을 의미합니다.)
- %steal - Steal CPU의 작동 시간
- %idle - 입출력(I/O) 대기시간(%idle과는 다르며 ioswait가 높은경우 메모리 부족이나 비효율적인 I/O부 시스템이 구성되어 있음을 의미합니다.)

#### 디스크 장치의 활용량 출력 정보
- tps - 디스크 장치에서 초당 처리한 입출력의 잡업 개수 입니다.
- kB-read/s - 디스크 장치에서 초당 읽어들인 데이터 블록 단위 입니다.
- kB_wrtn/s - 디스크 장치에서 초당 쓴 데이터 블록 단위 입니다.
- kB_wrtn - 디스크 장치에서 쓴 데이터 블록 단위 입니다.

#### 확장된 통계 정보를 출력

명령어 : iostat -x

```
1 [root@web /]# iostat -x
2 Linux 2.6.32-642.13.1.el6.x86_64 (web.server)   2017년 03월 17일   _x86_64_  (1 CPU)
3 
4 avg-cpu:  %user   %nice %system %iowait  %steal   %idle
5            0.02    0.00    0.11    0.06    0.00   99.80
6  
7 Device:         rrqm/s   wrqm/s     r/s     w/s   rsec/s   wsec/s avgrq-sz avgqu-sz   await r_await w_await  svctm  %util
8 scd0              0.00     0.00    0.00    0.00     0.01     0.00     8.00     0.00    1.36    1.36    0.00   1.36   0.00
9 sda               0.12     0.62    0.44    0.16    16.72     6.27    38.02     0.00    4.79    2.62   10.74   2.02   0.12
```

### References
https://itstudyblog.tistory.com/393