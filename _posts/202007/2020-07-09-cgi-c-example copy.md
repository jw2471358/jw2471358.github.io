---
layout: post
title: CGI C Programming
subtitle: 
description: CGI C Programming
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/pixabay/dog-4390885_1920_f82yat.jpg
category: CGI
tags:
  - CGI
  - C
author: jw2471358
---

### CGI란 무엇인가?

CGI는 Common Gateway Interface의 약자다. 웹브라우저에서 HTML로 여러가지 정보를 처리하는데, 그 기능만으로 모든 정보처리를 다 할 수 없다. 이것을 보충하기 위한 외부 프로그램과 웹서버(HTTP Server) 간의 연결 역할을 하기 위한 규약이 CGI이다.

 ![placeholder](http://dpnm.postech.ac.kr/cs103/lab-material/11/cse103-1120-CGI.files/image001.jpg)

또는 넓은 의미로 CGI를 수행하는 외부 프로그램을 포함하여 말하기도 한다. 예를 들어, 홈페이지에 방문객들의 comment를 받을 수 있는 방명록을 만들려고 할 때, 웹에서 구현하는 HTML만으로는 해결할 수 없다. 그래서 외부 프로그램이 필요한데, 이 때 외부 프로그램과 웹 간에 서로 주고 받을 수 있는 규약을 CGI라고 하고, 그 때 사용하는 프로그램을 gateway프로그램이라고 하는데 이것을 흔히 CGI 프로그램(혹은 스크립트)이라고 한다. 이 CGI프로그램은 통상적으로 C/C++ 나 PERL혹은 UNIX Shell, Tcl/Tk 등을 사용하여 구현한다.

 

이 CGI를 구현하기 위해서는 보통 웹 쪽에서는 FORM 택을 통해서 사용자의 입력값들을 웹서버(httpd)로 보내고, 서버에서는 그 값을 CGI프로그램에게 입력값들을 넘겨준다.



 

 

위의 그림을 보고 데이타의 흐름을 알아 보면,

 

1) 클라이언트(웹브라우저)에서 서버로 TCP/IP 연결을 통해 데이타 요청

2) 서버가 CGI프로그램에게 실행을 하도록 요청을 건네주기

3) CGI프로그램에서 서버로 출력이 전달

4) 적절한 MIME헤더를 갖고 서버가 클라이언트로 응답한 후, 연결이 해제
 ![placeholder](http://dpnm.postech.ac.kr/cs103/lab-material/11/cse103-1120-CGI.files/image001.jpg)
 

### C-CGI로 Hello CGI World를 웹 브라우저에 print하기

(주의 [ID]는 자신의 계정을 말한다.)

1) pshell에 로긴한다.

2) /usr/local/apache/cgi-bin/[ID]에 Hello.c 파일을 만든다.
```c
#include<stdio.h>

int main()

{

   printf("Content-type: text/html\n\n");   //CGI문서라는 것을 알려주는 것으로

                                   // 반드시 있어야 한다.

   printf("<H1>Hello CGI World!!! </H1><P>\n");

}
```

3) cc –o Hello.cgi Hello.c

4) http://pshell.postech.ac.kr/cgi-bin/[ID]/Hello.cgi

![placeholder](http://dpnm.postech.ac.kr/cs103/lab-material/11/cse103-1120-CGI.files/image003.jpg)

 

### CGI Library

웹브라우저는 공백은 +로 인식하며 %로 시작하는 2바이트 16진수값(%XX)을 사용한다.  이것은 다음과 같은 예에서 나타난다.  이 예는 검색엔진에서 검색결과를 보여줄 때 나타나는 문자이다.

http://www.lycos.co.kr/srch/?lpv=1&loc=searchhp&query=%B3%EB%B6%F3

또한 예에서 보면 ?와 =이 사용된 것을 알 수 있다.  이 말은 다시 말해서 C로 CGI프로그래밍을 하려면 공백(+), %XX, ?, =등을 처리를 해가면서 프로그래밍을 해야 한다는 이야기 이다.  이런 것을 본인지 직접 만들어 처리하려면 쉽지 않지만 다음과 같은 라이브러리를 통해 쉽게 처리할 수 있으며 이 라이브러리는 위의 글자를 처리해 주는 것 외에도 유용한 함수를 포함하고 있다.  참고로 여기서 소개하는 라이브러리는 가장 공통으로 많이 사용하는 C-CGI라이브러리이며 인터넷을 찾아보면 고급 프로그래밍을 위한 라이브러리도 찾아볼 수 있다. 

1) cgiutil.h

//각 함수에 대한 설명은 cgiutil.c에 주석 처리 해 놓았으니 지금 읽어보자.
```c
void getword(char *word, char *line, char stop);
char *makeword(char *line, char stop);
char *fmakeword(FILE *f, char stop, int *cl);
char *smakeword(char *str, char stop, int *cl);
char x2c(char *what);
void unescape_url(char *url);
void plustospace(char *str);
int  ind(char *s, char c);
int  rind(char *s, char c);
int  getline(char *s, int n, FILE *f);
void send_fd(FILE *f, FILE *fd);
void escape_shell_cmd(char *cmd);
char *rmCtrlChar(char *str);
char *rmCrLf(char *str);
void prtErrMsg(char *str);
void back(void);
```

2) cgiutil.h, cgiutil.c를 AFS의 cs103b/asn5에 넣어놓겠다.

 

### CGI 환경변수

CGI프로그래밍을 하기 위해서는 이 환경변수를 잘 이해해야 한다. 클라이언트가 요청하여 gateway프로그램이 수행되면 일련의 환경변수가 넘어온다. 이 환경변수는 크게 두 종류로 나눌 수 있다. 즉, 한 종류는 클라이언트의 요청과 무관한 것으로, 서버 metainformation 이라고 일컫는 서버의 정보에 관한 값들이다. 또 한 종류로는 클라이언트의 요청에 따라 값이 달라지는 것들이다.

이 환경변수들을 볼 수 있는 한 방법으로는 자신의 웹브라우저에서http://pshell.postech.ac.kr /cgi-bin/test-cgi 의 URL로 test-cgi를 불러내면 해당 시스템의 환경변수를 볼 수 있다.

 ![placeholder](http://dpnm.postech.ac.kr/cs103/lab-material/11/cse103-1120-CGI.files/image005.jpg)

 
1) 서버에 대한 HTTP 정보를 나타내는 환경변수들

| 환경변수 이름 | 설명     | 
| SERVER_SOFTWARE | 웹서버의 이름과 버전을 나타냅니다. 형식: 이름/버전 | 
| SERVER_NAME | 서버의 호스트 이름과 DNS alias 혹은 IP address | 
| GATEWAY_INTERFACE | 서버의 CGI 타입과 개정레벨을 나타냅니다. 형식: CGI/revision | 

2) 클라이언트의 요청에 따른 환경변수들

| 환경변수 이름 | 설명 | 
| SERVER_PROTOCOL | 클라이언트 요청이 사용하는 프로토콜. 보통 HTTP 1.0 혹은 HTTP 1.1 | 
| SERVER_PORT | 클라이언트 요청을 보내는 포트 번호. | 
| REQUEST_METHOD | HTML 폼이 사용하는 METHOD 보통 GET이나 POST | 
| PATH_INFO | 클라이언트에 의해 전달되는 추가 PATH 정보. 이 환경변수를 이용하여 스크립트를 부를 수 있습니다. | 
| PATH_TRANSLATED | PATH_INFO에 나타난 가상 경로(path)를 실제의 물리적인 경로로 바뀐 값. | 
| SCRIPT_NAME | 현재 실행이 요청된 스크립트 명 | 
| QUERY_STRING | GET 방식에서 URL의 뒤에 나오는 정보를 저장하거나 폼입력 정보를 저장합니다.(POST방식은 제외) | 
| REMOTE_ADDR | 클라이언트의 IP주소 | 
| REMOTE_HOST | 클라이언트의 호스트 이름 | 
| REMOTE_USER | 서버가 사용자 인증을 지원하고, 스크립트가 그 확인을 요청한다면, 이것이 확인된 사용자이름이 됩니다. | 
| REMOTE_IDENT | 서버가 RFC931 사용자 확인을 지원한다면 서버로부터 발췌된 사용자 이름이 이 환경변수에 저장된다. 이 변수 의 용도는 로그인에만 한정됩니다. | 
| CONTENT_LENGTH | POST방식일 경우 클라이언트에서 넘겨 지는 사용자 입력의 길이를 표시합니다. | 
| CONTENT_TYPE | POST방식을 이용하여 검색문에 정보가 들어있는 경우에 그 정보의 타입을 나타냅니다. | 
| HTTP_USER_AGENT | 클라이언트의 사용 프로그램(웹브라우저)을 표시합니다. | 

3) 환경변수를 CGI 프로그램에서 사용하기

환경변수를 CGI프로그램에서 사용하는 형식은 간단하다. PERL에서는 $ENV{'환경변수이름'} 의 형식으로 환경변수들을 참조할 수 있다. C에서는 getenv("환경변수이름") 의 형식으로 참조한다.

 

ex) Hello CGI World에 다음을 입력해 보자.

printf("<B>%s</B>\n", getenv("SERVER_SOFTWARE"));

 

 

### 입력값 전달 방식 get/post

// get방식은 URL에서 입력인자를 직접주는 것이고 post방식은 html form을 사용한다고 쉽게 생각하자.

// 지금 실습할 *.c파일을 cs103b/asn5에 넣어놓겠다.  여러분들이 asn5를 할 때 유용하게 사용할 수 있는 예제들이다.

 

웹 쪽에서 입력값들을 넘겨주는 FORM택의 구성은 보통 다음과 같다.
```html
<FORM METHOD=get/post ACTION="http://www.abc.com/cgi-bin/abc.cgi">
```
 

물론 이것은 보편적으로 사용하는 경우의 예이고, 이 FORM택에는 다른 많은 속성들이 있다..  여기서 METHOD는 post와 get 두 개의 방식이 있는데, 이 방식에 대해서 알아 보자.

 

1) get method

FORM택에 METHOD=get으로 하거나 생략하면 사용자의 입력값들이 환경변수(Environment Variable)에 저장되어 넘겨진다. 즉 각 입력값들이 기본URL에 붙는 인수(PARAMETER)로서 첨가되어 CGI프로그램으로 값을 넘겨 주게 된다.

물론 이 get METHOD는 FORM택을 사용하지 않고 바로 URL에 인수를 첨가하여 사용할 수도 있다.

 

예를 들어, http://www.abc.com/cgi-bin/abc.cgi?First+Name=foo&Last+Name=bar 와 같은 형식으로 사용된다.

 

이 GET METHOD를 이용하면 그 입력값들이 환경변수의 하나인 QUERY_STRING 에 들어가서 전달되는데, CGI스크립트는 그 QUERY_STRING에 들어 있는 값을 읽습니다. 이 때 그 값들은 입력된 그대로 넘어가는 것이 아니라 서버에 의해 여러가지로 변환(인코딩)되어 넘어가는데 CGI스크립트에서는 그 값들을 해독(decoding)해야 한다.

 

이 GET METHOD는 보통 입력값들이 많지 않는 경우 혹은 그냥 URL에 붙는 파라미터로 넘겨서 CGI스크립트로 전달할 때에 사용한다.

 

ex) 다음 URL을 눈여겨 보자. 

?na=1&na=2의 의미를 정확하게 알자.

 ![placeholder](http://dpnm.postech.ac.kr/cs103/lab-material/11/cse103-1120-CGI.files/image007.jpg)

 

// 소스에서 위의 결과가 어떻게 나오는 것인지 분석해 보자.

#### form-get.c의 소스
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#include "cgiutil.h"

typedef struct {
    char name[128];
    char value[128];
} ENTRY;


void main(void)
{
    ENTRY entVal[10000];
    int i, m = 0;
    char *qs;

    /* MIME 헤더 전달 */
    printf("Content-type: text/html\n\n");

    /* 폼 전달 방법(Method)이 GET이 아니면 종료 */
    if(strcmp(getenv("REQUEST_METHOD"), "GET"))
        exit(1);

    /* 질의문자열을 qs가 가리키도록 함 */
    qs = getenv("QUERY_STRING");

    /* 질의문자열이 없으면 종료 */
    if(qs == NULL)
        exit(1);

    /* 질의문자열이 '\0'일 때까지 name/value쌍을 읽어 entVal에 저장 */
    for(i = 0; qs[0] != '\0'; i++) {
        m = i;  /* name/value쌍의 총 개수 */

        /* name/value쌍은 '&' 문자로 구분하므로 그 값을
           entVal[i].value에 넣고 */
        getword(entVal[i].value, qs, '&');

        /* entVal[i].value의 모든 '+' 문자를 공백으로 바꾼 다음 */
        plustospace(entVal[i].value);

        /* %로 시작하는 2바이트 16진수값은 '%xx' 해당 문자로 바꾸고 */
        unescape_url(entVal[i].value);

        /* 마지막으로 name과 value를 '=' 문자로 구분 지어 각각
           entVal[i].name과 entVal[i].value에 저장 */
        getword(entVal[i].name, entVal[i].value, '=');
    }

    /* 질의 결과 출력 */
    printf("<H1>질의 결과</H1><P>");
    for(i = 0; i <= m; i++)
        printf("<FONT     SIZE=+2>%s      =     %s</FONT><BR>\n",     entVal[i].name,
entVal[i].value);
}
```
 

2) post method

FORM택에서 METHOD=post로 하면, get METHOD가 환경변수중의 하나인 QUERY_STRING을 통해 전달되는 것과 달리 stdin(standard input:표준입력) 을 통해서 전달된다.  get METHOD가 인수를 통해서 전달되므로 커맨드라인 의 길이에 의한 제한을 받는 반면에, post METHOD는 stdin을 이용하므로 데이타양의 제한이 없다. 또한 post METHOD에서도 환경변수들은 stdin과 함께 전달된다. 그리고 post방식도 마찬가지로 입력값들이 encoding되어 넘어옴으로 CGI에서 그 값들을 decoding해야 한다.

ex) 다음과 같은 폼에서 다음 글자를 입력하면

 ![placeholder](http://dpnm.postech.ac.kr/cs103/lab-material/11/cse103-1120-CGI.files/image009.jpg)

 

다음과 같은 결과를 보여주는 cgi프로그램이다.

 ![placeholder](http://dpnm.postech.ac.kr/cs103/lab-material/11/cse103-1120-CGI.files/image011.jpg)

 

#### form-post.c의 소스

// 소스를 보면서 위의 결과가 어떻게 출력되었는지 정확하게 알자.
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#include "cgiutil.h"

typedef struct {
    char *name;
    char *value;
} ENTRY;

void main(void)
{
    ENTRY entVal[10000];
    int i, m = 0;
    int cl;

    /* MIME 헤더 전달 */
    printf("Content-type: text/html\n\n");

    /* 폼 전달 방법(Method)이 POST가 아니면 종료 */
    if(strcmp(getenv("REQUEST_METHOD"), "POST"))
        exit(1);

    /* FORM 인코딩 타입이 POST의 디폴트 인코딩 방식인
       'application/x-www-form-urlencoded'가 아니면 종료 */
    if(strcmp(getenv("CONTENT_TYPE"), "application/x-www-form-urlencoded"))
        exit(1);

    /* 폼데이터의 총 길이 */
    cl = atoi(getenv("CONTENT_LENGTH"));

    /* 표준입력에서 cl만큼 name/value쌍을 읽어 entVal에 저장 */
    for(i = 0; cl && (!feof(stdin)); i++) {
        m = i;
        entVal[i].value = fmakeword(stdin, '&', &cl);   /* name/value를 &로 구분 */

        /* CGI 디코딩 */
        plustospace(entVal[i].value);   /* '+'는 ' '으로 */
        unescape_url(entVal[i].value);  /* %xx는 ascii로 */
        entVal[i].name = makeword(entVal[i].value, '='); /* VALUE와 NAME값을 '=' 문자로 구분 */
    }

    /* 질의 결과 화면 출력 */
    printf("<H1>질의 결과</H1><P>");
    for(i = 0; i <= m; i++)
        printf("<FONT     SIZE=+2>%s      =     %s</FONT><BR>\n",     entVal[i].name,
entVal[i].value);
}
```
 

### 제출물

// 이번 제출물은 쉽지 않으므로 조교가 적당한 시간을 준다.(4일정도)

1) form-get.c와 form-post.c에서 사용된 library함수의 설명과 사용법을 메일로 제출한다.

2) 자신의 게시판에 쓰여질 자료를 입력받는 form을 설계하고 이것을 post방식으로 입력받아 웹에 보여주는 .c파일을 만들어 .cgi로 컴파일하고 이것을 자신의 홈페이지 제일 처음에 링크시켜 놓고 조교에게 링크주소와 소스를 메일로 보낸다.

### References
<http://dpnm.postech.ac.kr/cs103/lab-material/11/cse103-1120-CGI.html>