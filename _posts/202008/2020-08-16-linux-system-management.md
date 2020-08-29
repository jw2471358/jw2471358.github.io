---
layout: post
title: Linux 시스템 관리
subtitle: 
description: Linux 시스템 관리
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/pixabay/me-nots-5302712_1920_ktf3cg.jpg
category: linux
tags:
  - linux 시스템 관리
author: jw2471358
---

#### 시스템 관리자

슈퍼 유저는 root 계정으로 로그인하여 시스템 관리의 모든 측면을 수행할 수 있다.

#### 사용자 변경

$ su [사용자명]  

#### 사용자 계정 추가

$ useradd [옵션] 사용자명  

-c 코멘트  
-d 디렉터리  
-e 날짜  
-s 쉘  
-u uid  
-g 그룹  

$ passwd gildong

패스워드는 /etc/shadow 파일에 암호화되어 저장된다.

$ userdel [-r] 사용자명  
-r 옵션은 사용자 홈 디렉터리도 삭제한다.

$ groupadd [-g gid] 그룹명  
-g 옵션으로 추가할 그룹 ID를 지정할 수 있다.

$ groupdel 그룹명  


#### 런레벨

 | --- | --------------- |
 | 런레벨    |  부팅 환경     |
 | --- | --------------- |
 | 0 | 시스템을 정지한다.      |
 | 1 | 단일 사용자 모드로 부팅하며 네트워크 기능을 사용 안 한다. root로만 로그인 가능하다. |
 | 2 | 다중 사용자 모드로 부팅하며 네트워크 기능을 사용 안 한다. |
 | 3 | 정상 작동 모드로 다중 사용자 모드, 텍스트 인터페이스로 부팅한다. |
 | 4 | 사용되지 않으며 특별한 시스템을 구현하기 위한 예약된 레벨이다. |
 | 5 | 정상 작동 모드로 부팅하며 X-윈도우 인터페이스로 부팅한다. |
 | 6 | 시스템을 재부팅 한다. |

$ runlevel  
N 5  

$ init 6  


#### 프로세스 관리 도구 top

$ top [-d 숫자]  
프로세스별 CPU와 메모리 점유율 등을 출력한다.  
-d 옵션 숫자만큼의 시간마다 다시 출력한다.  

$ shutdown 시간 [경고메시지]  
지정된 시간에 시스템을 종료한다. 모든 사용자에게 보낼 경고 메시지를 명시할 수 있다.  

$ ntsysv [옵션]  
부팅시에 런레벨 별로 init 시스템이 실행하거나 실행하지 않을 서비스들을 설정한다.  

$ chkconfig [옵션] 서비슷명 [상태]  
부팅 시에 init 시스템에 의해 자동 실행할 각종 서비스들을 설정한다.  

$ service 서비스 명령어  
시스템 서비스를 조작하기 위해 서비스 데몬을 명령어에 따라 제어한다.  

$ rpm -ivh 패키지파일  
RPM 패키지 파일로부터 패키지를 새로 설치한다.  

$ rpm -Uvh 패키지파일  
이미 설치되어 있는 패키지를 업그레이드한다. 설치되어 있지 않으면 새로 설치한다.  

#### systemd 관련 명령어

$ systemd-analyze  
부팅에 걸린시간 표시  

$ systemd-analyze blame  
부팅시 서비스별 걸린 시간표시  

$ systemd-analyze plot  
부팅시 서비스별 걸린 시간을 정령해서 표시  

$ systemd-analyze critical-chain  
부팅시 시간이 많이 걸리는 서비스들을 트리 형태로 엮어서(chain) 표시

$ journalctl  
부팅을 포함한 전체적인 시스템 로그

$ journalctl -b  
마지막 부팅 이후 시스템 로그  

$ hostnamectl  
호스트 이름 표시  

$ hostnamectl  set-hostname 이름  
호스트 이름 변경  

#### systemctl 명령어

$ systemctl enable 서비스명  
$ systemctl disable 서비스명  
$ systemctl start 서비스명  
$ systemctl stop 서비스명  
$ systemctl restart 서비스명  
$ systemctl reload 서비스명  
$ systemctl kill 서비스명  
$ systemctl daemon-reload  
서비스 설정 정보를 데몬에 반영  

#### rpm 명령어 모드

설치모드 : # rpm -i [설치옵션] 패키지파일+  
검색모드 : # rpm -q [질문옵션] [패키지파일]  
검증모드 : # rpm -V |-y|--verify [검증옵션]  
서명확인모드 : # rpm --checksig 패키지파일+  
삭제모드 : # rpm -e 패키지명+  
제작모드 : # rpm -b0 [제작옵션] 패키지스펙+  

#### yum 명령어

업데이트 목록 확인 : # yum check-update  
패키지 리스트 : # yum list  
패키지 업데이트 : # yum update 패키지*  
패키지 설치 : # yum install 패키지+  
패키지 삭제 : # yum remove 패키지+  
패키지 정보 확인 : # yum info 패키지  
패키지 검색 : # yum search 패키지  
