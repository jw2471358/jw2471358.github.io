---
layout: post
title: Linux 프로세스 원리
subtitle: 
description: Linux 프로세스 원리
# image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/pixabay/moon-5224745_1920_ufjpll.jpg
category: linux
tags:
  - linux 프로세스 원리
  - 프로세스
  - process
author: jw2471358
---

프로세스의 내부구조, 프로세스를 생성하는 원리, 프로세스에 프로그램을 실행시키는 원리, 시스템 부팅 과정

### 프로세스 이미지
일반적으로 프로그램은 하드디스크에 저장되며 프로그램을 실행하여 프로세스가 되기 위해서는 먼저 하드디스크로부터 프로그램의 실행 화일(executable file)을 읽어서 주메모리인 RAM 공간에 적재시켜야 한다. 
먼저 프로세스를 관리하기 위해서 커널 내에 프로세스에 대한 정보가 필요한데 이러한 정보를 보통 PCB(Process Control Block)라고 한다. 
또한 프로그램을 실행하기 위해서는 텍스트(실행 코드), 데이터, 힙, 스택 등의 영역(segment)들을 위한 메모리를 할당해야 한다. 이러한 메모리 배치를 프로세스 이미지(proecess image)라고 한다.

 | ---------------- |
 | 텍스트(코드)     |
 | ---------------- |
 | 데이터           |
 | ---------------- |
 | 힙              |
 | ---------------- |
 |                  |
 |                  |
 |                  |
 | 스택             |
 | ---------------- |
 | U-영역           |
 | ---------------- |

- 텍스트(text)
프로세스가 실행하는 실행 코드를 저장하는 영역으로 텍스트 영역 혹은 코드 영역이라고 한다.

- 데이터(data)
프로그램 내에 선언된 전역 변수(global variable) 및 정적 변수(static variable) 등을 위한 메모리 영역이다. 프로그램에서 초기화된 데이터를 저장하는 영역(보통 bss 영역이라고 함)과 초기화되지 않는 데이터를 저장하는 영역으로 구분할 수 있다.

- 힙(heap)
동적 메모리 할당을 위한 영역이다. C 프로그램에서 malloc 함수를 호출하면 이 영역에서 동적으로 메모리를 할당해준다.

- 스택(stack area)
함수 호출을 구현하기 위한 실행시간 스택(runtime stack)을 위한 영역으로 함수가 호출될 때마다 해당 함수의 지역 변수, 매개변수, 반환주소, 반환값 등을 포함하는 활성 레코드(activation record)가 할당되고 함수가 반환될 때마다 할당된 활성 레코드를 회수한다.

- U-영역(user-area)
열린 파일의 파일 디스크립터, 현재 작업 디렉터리 등과 같은 프로세스의 내부 정보를 저장하는 영역이다.

$ size [실행파일]  
실행파일의 각 영역의 크기를 알려준다.

$ size /bin/ls  
   text     data  bss   dec     hex    filename  
  109479    5456   0   114935  1c0f7   /bin/ls

### 프로세스 ID

#### 쉘의 명령어 처리과정
쉘은 보통 사용자가 입력한 명령어를 실행하기 위해 새로운 자식 프로세스를 생성하여 이 프로세스로 하여금 입력된 명령어(프로그램)를 실행하게 한다. 따라서 쉘은 명령어를 실행하는 자식 프로세스의 부모 프로세스가 된다. 특히 후면 처리의 경우에는 다음과 같이 명령어 실행을 위해 생성된 자식 프로세스의 번호를 알려준다.

$ 명령어 &  
[1] 프로세스번호

전면처리는 부모 쉘 프로세스가 자식 프로세스가 끝나기를 기다리고 후면처리는 부모 쉘 프로세스가 자식 프로세스가 끝나기를 기다리지 않는다.

#### 프로세스 ID

hello.c
```c
 #include <stdio.h>
 #include <unistd.h>
  
 int main()
 { 
     printf("Hello !\n");
     printf("나의 프로세스 번호 : [%d] \n", getpid());
     printf("내 부모 프로세스 번호 : [%d] \n", getppid());
     system("ps");
 }
 ```

### 프로세스 생성

#### 프로세스 생성: fork()
리눅스 시스템에서는 fork() 시스템 호출이 새로운 프로세스를 생성하는 유일한 방법이다. 이렇게 생성한 새로운 프로세스를 자식 프로세스(child proces)라고 하고 자식 프로세스를 생성한 프로세스는 부모 프로세스(parent process)라고 한다.

자식 프로세스에게는 0을 반환하고 부모 프로세스에게는 자식 프로세스 ID를 반환한다.

fork() 시스템 호출은 부모 프로세스를 똑같이 복제하여 새로운 자식 프로세스를 생성한다.

fork1.c
```c
#include <stdio.h>
#include <unistd.h>

/* 자식 프로세스를 생성한다. */
int main()
{ 
    int pid;
    printf("[%d] 프로세스 시작 \n", getpid());
    pid = fork();  
    printf("[%d] 프로세스 : 리턴값  %d\n", getpid(), pid);
}
```

#### 부모-자식 프로세스

pid = fork();  
if( pid == 0 ){  
    //자식 프로세스의 실행 코드  
}else{  
    //부모 프로세스의 실행 코드  
}  

fork2.c
```c
#include <stdlib.h>
#include <stdio.h>

/* 부모 프로세스가 자식 프로세스를 생성하고 서로 다른 메시지를 프린트한다. */
int main() 
{
   int pid;

   pid = fork();
   if(pid ==0){  /* 자식 프로세스 */
      printf("[Child] : Hello, world pid=%d\n",getpid());
   }
   else {        /* 부모 프로세스 */
      printf("[Parent] : Hello, world pid=%d\n",getpid());
   }
}
```

실행결과  
$ fork2  
[Parent] : Hello, world ! pid=15065  
[Child] : Hello, world ! pid=15066  

#### 프로세스 기다리기
부모 프로세스는 wait() 시스템 호출을 이용하여 자식 프로세스 중의 하나가 종료할 때까지 기다릴 수 있다. 자식 프로세스가 종료하면 자식 프로세스의 종료코드가 *status에 저장되며 종료한 자식 프로세스의 ID를 반환한다.

exit() 시스템 호출은 프로세스를 종료시킨다. 프로세스의 종료 상태를 알리는 종료 상태 코드(exit status code)를 부모 프로세스에게 전달한다.


### 프로그램 실행

#### 프로그램 실행의 원리
리눅스 시스템에서는 exec() 시스템 호출을 이용하여 프로세스 내에서 새로운 프로그램을 실행시킬 수 있다. 이를 자기대치라고 할 수 있다. 

exec() 시스템 호출이 성공하면 그 프로세스 내에 기존의 프로그램은 없어지고 새로운 프로그램으로 대치되므로 실패할 경우에만 반환한다는 점을 유의하자. 

#### exec() 시스템 호출

```c
#include <unistd.h>
int execl(char* path, char* arg0, char* arg1, ... , char* argn, NULL)
int execp(char* file, char* arg0, char* arg1, ... , char* argn, NULL)
int execv(char* path, char* argv[])
int execvp(char* file, char* argv[])
//호출한 프로세스의 코드, 데이터, 힙, 스택 등을 path(혹은 file)가 나타내는 새로운 프로그램으로 대치한 후 새 프로그램을 실행한다. 성공한 exec() 호출은 반환하지 않으며 실패하면 -1을 반환한다.
```

exec1.c

```c
#include <stdio.h>
#include <unistd.h>

/* echo 명령어를 실행한다. */
int main( ) 
{    
	printf("시작\n");
    execl("/bin/echo", "echo", "hello", NULL);
	printf("exec 실패!\n"); 
}
```

$ exec 명령어 [인수]  

```
$ exec date  
2016. 13. 22. (화) 16:04:41 KST  
```

#### 쉘의 명령어 처리 원리
부모 프로세스는 wait() 시스템 호출을 이용하여 자식 프로세스가 종료할 때까지 기다릴 수 있다. 자식 프로세스가 종료하면 자식 프로세스의 종료코드가 *status에 저장되며 종료한 자식 프로세스의 ID를 반환한다. 

exec2.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

/* 자식 프로세스를 생성하여 echo 명령어를 실행한다. */
int main( ) 
{    
	int pid, child, status;	

    printf("부모 프로세스 시작\n");
    pid = fork();
	if (pid == 0) {
        execl("/bin/echo", "echo", "hello", NULL);
		fprintf(stderr,"첫 번째 실패");    
        exit(1);
    }
    else {
		child = wait(&status);
        printf("자식 프로세스 %d 끝\n", child);
		printf("부모 프로세스 끝\n");
	}
}
```

실행결과  
$ exec2  
부모 프로세스 시작  
hello  
자식 프로세스 15066 끝  
부모 프로세스 끝  

이 프로그램은 echo 명령어만 실행시키고 있는데 쉘은 사용자가 입력한 명령어를 이와 같은 방식으로 실행시킨다. 


### 프로그램 실행 과정


```c
#include <stdio.h>

/* 모든 명령줄 인수를 프린트한다. */
int main(int argc, char *argv[])
{
    int      i;

    for (i = 0; i < argc; i++)            /* 모든 명령줄 인수 프린트  */
        printf("argv[%d]: %s \n", i, argv[i]);

    return 0;
}
```

실행결과  
$ printargv hello world  
argv[0]: printargv    
argv[1]: hello  
argv[1]: world  

exit( main( argc, argv ) ); 

exit() 시스템 호출은 프로세스를 정상적으로 종료시키는데 종료 전에 모든 열려진 스트림을 닫고(fclose), 출력 버퍼의 내용을 디스크에 쓰는(fflush) 등의 뒷정리를 한다. 그리고 프로세스의 종료 상태를 알리는 종료 코드(exit code)를 부모 프로세스에게 전달한다.


### 시스템 부팅과 프로세스

#### 시스템 부팅 과정

시스템 부팅은 fork/exec 시스템 호출을 통해 이루어진다.

리눅스 시스템 부팅은 부트로더에 의해서 시작된다. 리눅스 운영체제의 경우에는 GNU GRUB(GRand Unified Bootloader)에 의해 부팅이 시작된다. GRUB 부트로더는 실행과 함께 /boot/grub/grub.conf(혹은 /boot/grub2/grub.cfg) 파일을 읽어서 어떤 부팅메뉴(커널)로 부팅을 할 것인가를 결정하고 부팅이 시작되면 커널(kernel) 이미지를 로딩하고 시스템 제어권을 커널에게 넘겨준다.

커널은 커널 내부에서 프로세스 ID가 0인 첫 번째 프로세스 swapper를 만든다. swapper는 커널이 사용할 각 장치 드라이브들을 초기화하고 fork/exec를 수행하여 1번 프로세스인 init 프로세스를 생성한다.

init 프로세스는 /etc/inittab 파일을 읽어 들여서 그 내용들을 차례대로 실행하는데 보통 fork/exec를 반복적으로 수행하여 시스템 운영에 필요한 다양한 프로스세들(주로 서버 데몬 프로세스)을 새로 생성한다. 따라서 init 프로세스는 많은 프로세스의 조상이 된다. 최근 리눅스 배포판인 RHEL 7, CentOS 7 등에서는 systemd 프로세스가 init 시스템을 대치하여 시스템 부팅을 담당하고 있다. 


-> fork/exec  
--> exec : 로그인 과정  

swapper(0) -> init(1) -> sshd(120)  
swapper(0) -> init(1) -> getty(350) --> login(350) --> shell(350)  

#### 부팅 관련 프로세스

- swapper(스케줄러 프로세스)
0번 프로세스인 swapper는 커널 내부에서 최초로 만들어진 프로세스로 프로세스 스케줄링을 담당한다. 이 프로세스는 커널 내의 코드를 실행하기 때문에 별도의 실행 파일이 존재하지 않는다.

- init(초기화 프로세스)
init 프로세스(/etc/init 혹은 /sbin/init)는 /etc/inittab 파일에 기술된 대로 시스템을 시작하고 초기화한다. 시스템 초기화시 어떤 레벨로 초기화할지 /etc/inittab 파일에 0~6의 레벨 중 하나로 명시할 수 있다. 이 레벨을 런레벨(runlevle)이라고 하고 이 런레벨에 따라 다른 부팅 과정을 거친다.  
init 프로세스에 의한 실제 시스템 초기화는 시스템 초기화를 처리해주는 명령들을 포함하고 있는 쉘 스크립트들을 수행하여 이루어진다. 이러한 쉘 스크립트를 rc(run command) 스크립트라고 하며 이 스크립트들은 /etc/rc.d 디렉터리 내에 각 런레벨별로 서브디렉터리에 나누어 저장되어 있다. 예를 들어, 부팅 레벨이 5이면 해당 디렉터리는 /etc/rc.d/rc5.d 이며 부팅 레벨에 따라 해당 디렉터리 내에 있는 쉘 스크립트들을 실행하게 된다. 이러한 쉘 스크립트 실행 과정을 통해서 파일 시스템 마운트, 서버 데몬 프로세스 생성, getty 프로세스 생성 등의 작업을 수행하여 시스템을 초기화한다. 
init 프로세스는 /etc/inittab 파일에 기술된 대로 시스템을 시작하고 초기화한다.

- 서비스 데몬 프로세스
부팅되는 컴퓨터에서 제공하는 서비스들을 위한 다양한 데몬 프로세스들이 생성된다. 예를들어, ftpd(file transfer protocol daemon) 프로세스는 파일 전송 서비스를 위한 데몬 프로세스이며, sshd 프로세스는 시큐어 쉘(Secure Shell, SSH)을 서비스하기 위한 데몬 프로세스이다. 시큐어 쉘은 네트워크 상의 원격 컴퓨터에 로그인하거나 원격으로 명령을 실행할 수 있도록 해주는 프로토콜이다.

- getty 프로세스
getty 프로세스(/etc/getty 혹은 /etc/mingetty)는 가상 콘솔을 가능하게 해주는 프로세스이다. 이 프로세스는 로그인 프롬프트를 내고 키보드 입력을 감지한다. 아이디, 패스워드를 입력하면 로그인 절차를 진행하기 위해 로그인 프로그램(/bin/login)을 실행(exec) 한다.

- login 프로세스
login 프로세스는 /etc/passwd 파일을 참조하여 사용자의 로그인 아이디 및 패스워드를 검사한다. 로그인 절차가 성공하면 쉘 프로그램(/bin/sh, /bin/csh 등)을 실행(exec)한다.

- shell 프로세스
shell 프로세스는 시작 파일을 실행한 후에 쉘 프롬프트를 내고 사용자로부터 명령어를 기다린다. 명령어가 입력되면 자식 프로세스를 생성하여 입력된 명령어를 실행(exec)시킨다. 명령어 실행 후에 다시 쉘 프롬프트를 내고 이 과정을 반복한다.

#### 프로세스 트리 출력
/proc 디렉터리에는 현재 메모리에 존재하는 모든 프로세스들이 파일형태로 존재한다. 활성 프로세스의 이미지는 여기에 해당 프로세스 ID 번호로 저장된다. 프로세스 관련 명령어를 사용하여 /proc 디렉털에 나열된 프로세스에 대한 자세한 정보를 표시할 수 있다. 

pstree 명령어는 부팅과정에서 생성되어 실행 중인 프로세스들의 부모, 자식 관계를 트리 형태로 출력한다.

$ pstree  
실행중인 프로세스들의 부모, 자식 관계를 트리 형태로 출력한다.

#### 로그인한 사용자 정보 출력

$ w  
로그인한 사용자의 자세한 작업 정보를 출력한다.  

```
$ w | grep bash  
```