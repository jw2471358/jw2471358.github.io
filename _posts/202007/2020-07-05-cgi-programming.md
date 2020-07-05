---
layout: post
title: Getting Started with CGI Programming in C
subtitle: 
description: Getting Started with CGI Programming in C
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/pixabay/budapest-4011923_1920_kaujsl.jpg
category: CGI
tags:
  - CGI
  - C
author: jw2471358
---

#### CGI 프로그램에서 POST방식의 요청을 처리하는 예

웹브라우저에서 서버측의 CGI프로그램에 요청할 때는 GET, POST방식에 따라서 서버측에서 요청 문자열을 접수하는 방법이 다르다.

GET방식일 경우에는 웹브라우저의 요청 문자열을 서버측 환경변수인 QUERY_STRING에 저장되므로 CGI 프로그램에서는 getenv("QUERY_STRING) 과 같은 방법으로 읽을 수가 있다.

POST방식으로 요청한 경우에는 서버측 환경변수 CONTENT_LENGTH에 요청 문자열의 길이가 저장되고, 실제 요청문자열은 서버측에서 표준 입력스트림으로 읽어야 한다.

아래에 제시된 form.html은 Apache 2.2/htdocs/ 안에 복사하고, posttest.exe는 cgi-bin/안에 복사한 후에 웹브라우저에서 form.html을 요청하고 숫자를 입력한 후에 전송버튼을 누르면 CGI 프로그램이 실행된 결과를 볼 수 있다.

#### form.html
```html
<html>
 <head>  <title> POST example</title> </head>
 <body>
  <center>
 <form action="http://localhost/cgi-bin/posttest.exe" method="POST">
  <input type="text" name="m"/> x
  <input type="text" name="n"/> =
  <input type="text" value=""/><br>
  <input type="submit" value="보여주세요"/>
 </form>
  </center>
 </body>
</html>
```

#### posttest.exe

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(void) {
 char content[32];
 long m,n;
 long length;

 /* POST방식으로 요청한 문자열의 크기를 구한다 */
 char *content_len = getenv("CONTENT_LENGTH");

 /* 문자열의 크기는 문자열 형식이므로 정수로 변환한다 */
 sscanf(content_len, "%ld", &length);

 /* 표준입력스트림(stdin)으로부터 요청 문자열을 읽어온다 */
 fgets(content, length+2, stdin);

 printf("Content-Type:text/html;charset=euc-kr\n\n");

 printf("<html><head><title> POST요청, 곱셈결과 </title></head>\n");
 printf("<body><center>\n");
 printf("<h3>POST요청, 곱셈결과</h3>\n");

 printf("전달된 파라미터 : %s <br>\n 문자수 : %d \n", content, strlen(content));

 if(content==NULL) {
  printf("<p>웹브라우저에서 전달된 파라미터 문자열이 없습니다.<br>\n");
  printf("<p>요청폼에 2개의 수를 입력하고 다시 해보세요.<br>\n");
 }
 else if(sscanf(content, "m=%ld&n=%ld", &m, &n)!=2)
  printf("<p>파라미터의 값은 정수이어야 합니다<br>.\n");
 else
  printf("<p>계산 결과: %ld * %ld = %ld.\n", m,n,m*n);

 printf("</center></body>\n");

 return 0;

}
```

출처: <https://micropilot.tistory.com/1630>

-----------------------------------------------------------------

#### CGI 메커니즘

대부분의 웹 서버에서 CGI 메커니즘은 다음과 같은 방식으로 표준화되었습니다. 서버가 루트로 간주하는 일반 디렉토리 트리에서 cgi-bin 이라는 서브 디렉토리를 작성하십시오 . (이전 디렉토리의 그림에서이 디렉토리를 볼 수 있습니다.) 그러면 서버는 특수 cgi-bin 디렉토리에서 요청 된 모든 파일을 읽고 전송하는 것이 아니라 실행 해야한다는 것을 이해 합니다. 실행 된 프로그램의 출력은 실제로 페이지를 요청한 브라우저로 전송 된 것입니다. 실행 파일은 일반적으로 C 컴파일러 출력과 같은 순수한 실행 파일 이거나 PERL 스크립트입니다. PERL은 CGI 스크립팅에 널리 사용되는 언어입니다.

```c
#include <stdio.h>

int main()
{
  printf("Content-type: text/html\n\n");
  printf("<html>\n");
  printf("<body>\n");
  printf("<h1>Hello there!</h1>\n");
  printf("</body>\n");
  printf("</html>\n");
  return 0;
}
```
On my Web server, I entered this program into the file simplest.c and then compiled it by saying:

```
gcc simplest.c -o simplest.cgi
```

simplest.pl:
```perl
#! /usr/bin/perl
print "Content-type: text/html\n\n";
print "<html><body><h1>Hello World!";
print "</h1></body></html>\n";
Place the file into your cgi-bin directory. On a UNIX machine, it may help to also type:
```

```
chmod 755 simplest.pl
```

The whole point of CGI scripting, however, is to create dynamic content -- each time the script executes, the output should be different. After all, if the output is the same every time you run the script, then you might as well use a static page. The following C program demonstrates very simple dynamic content:

```c
#include <stdio.h>

int incrementcount()
{
  FILE *f;
  int i;

  f=fopen("count.txt", "r+");
  if (!f)
  {
     sleep(1);
     f=fopen("count.txt", "r+");
     if (!f)
       return -1;
  }

  fscanf(f, "%d", &i);
  i++;
  fseek(f,0,SEEK_SET);
  fprintf(f, "%d", i);
  fclose(f);
  return i;
}

int main()
{
  printf("Content-type: text/html\n\n");
  printf("<html>\n");
  printf("<body>\n");
  printf("<h1>The current count is: ")
  printf("%d</h1>\n", incrementcount());
  printf("</body>\n");
  printf("</html>\n");
  return 0;
}
```
With a text editor, type this program into a file named count.c. Compile it by typing:

```
gcc count.c -o count.cgi
```

--------------------------------------------------------------------

다음과 같은 간단한 HTML 형식을 살펴 보겠습니다.

```html
<form action="http://www.example/cgi-bin/mult.cgi">
<div><label>Multiplicand 1: <input name="m" size="5"></label></div>
<div><label>Multiplicand 2: <input name="n" size="5"></label></div>
<div><input type="submit" value="Multiply!"></div>
</form>
```

요청을 보낼 때 브라우저는 상대 URL을 지정하여 추가 정보를 제공합니다.이 경우에는 물음표 " "와 양식 데이터를 구체적으로 인코딩 된 형식 으로 추가하여 호스트 이름 뒤에 오는 값
/cgi-bin/mult.cgi?m=4&n=9


서버 에서 C 프로그램 을 컴파일하고로드 해야 합니다 (또는 원칙적으로 동일한 아키텍처를 가진 시스템에서 생성 된 바이너리도 서버에서 실행 가능하도록).


- CGI 스크립트로 사용하기 위해 필요할 수있는 사항을 변경하십시오. 프로그램은 의도 된 양식 제출 방법에 따라 입력 내용을 읽어야합니다. 기본 GET방법을 사용하면 환경 변수에서 입력을 읽습니다. QUERY_STRING. 프로그램은 파일에서 데이터를 읽을 수도 있지만 서버에 상주해야합니다. stdout적절한 HTTP 헤더로 시작하도록 표준 출력 스트림 ( ) 에서 출력을 생성해야합니다 . 종종 출력은 HTML 형식입니다.

- 컴파일하고 다시 테스트하십시오. 이 테스트 단계에서는 QUERY_STRING 양식 데이터로 전송 될 테스트 데이터가 포함되도록 환경 변수를 설정할 수 있습니다 . 예를 들어, 명명 된 필드 foo 에 입력 데이터가 포함 된 양식을 사용하려는 경우
setenv QUERY_STRING "foo=42"(tcsh 쉘 사용시)
또는
QUERY_STRING="foo=42"(bash 쉘 사용시 ) 명령을 제공 할 수 있습니다 .


```
 gcc -o mult.cgi mult.c 
```
mv mult.cgi ./cgi-bin


실행 파일의 일반적인 확장명은 .cgi 및 .exe입니다.

```c
#include <stdio.h>
int main(void) {
  printf("Content-Type: text/plain;charset=us-ascii\n\n");
  printf("Hello world\n\n");
  return 0;
}
```

### References
<https://computer.howstuffworks.com/cgi3.htm>
<http://jkorpela.fi/forms/cgic.html>