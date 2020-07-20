---
layout: post
title: Linux grep 명령어 옵션
subtitle: 
description: Linux grep 명령어 옵션
# image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/pixabay/moon-5224745_1920_ufjpll.jpg
category: linux
tags:
  - grep
author: jw2471358
---

### 1. grep 명령어.

grep은 입력으로 전달된 파일의 내용에서 특정 문자열을 찾고자할 때 사용하는 명령어입니다. 리눅스에서 가장 많이 사용되는 명령어 중 하나이죠.



하지만 grep 명령어가 문자열을 찾는 기능을 수행한다고 해서, 단순히 문자열이 일치하는지 여부만을 검사하는 것은 아닙니다. 문자열이 같은지(equal)만을 검사하는 수준을 넘어, 훨씬 복잡하고 다양한 방식으로, 그리고 매우 효율적으로 문자열을 찾는 기능을 제공하죠. 이는 grep이 파일의 문자열을 검색할 때, 단순 문자열 매칭이 아니라, 정규 표현식(Regular Expression)에 의한 패턴 매칭(Pattern Matching) 방식을 사용하기 때문입니다.

#### 1.1 정규 표현식(Regular Expression)
정규 표현식(Regular Expression)이란, 특정 규칙을 가진 문자열 집합을 표현하기 위한 형식 언어로써, 주로 문자열 패턴 매칭을 검사하거나 또는 문자열을 치환하기 위해 사용됩니다.



문자열 검색에 정규 표현식을 적용하게 되면, 지정된 문자열의 문자가 단순히 "같은지(equal)" 여부가 검사되는 것이 아니라, 정규 표현식의 규칙에 매칭(Matching)되는지 여부가 검사됩니다.



예를 들어, 단순 문자열 검색에서 '*'은 문자 그대로 '*'을 의미하기 때문에, ('*' == '*')은 성립하지만 ('A' == '*')는 성립하지 않습니다. 하지만 정규 표현식에서 '*'는 0개 이상의 모든 문자를 의미하므로, ('*' == '*') 뿐만 아니라 ('A' == '*')도 TRUE로 판단됩니다.



정규 표현식을 모두 설명하려면 지면이 한참 모자라니, 여기서는 정규 표현식을 작성할 때 사용되는 메타 문자(Meta Character)에 대해서만 간략히 정리하겠습니다.



메타 문자
(Meta Character)	설명
.	1개의 문자 매치 (정확히 1개의 문자와 매치)
*	앞 문자가 0회 이상 매치
{n}	앞 문자가 정확히 n회 매치
{n,m}	앞 문자가 n회 이상 m회 이하 매치
[ ]	대괄호에 포함된 문자 중 한개와 매치
[^ ]	대괄호 안에서 ^뒤에 있는 문자들을 제외
[ - ]	대괄호 안 문자 범위에 있는 문자들 매치
()	표현식을 그룹화
^	문자열 라인의 처음
$	문자열 라인의 마지막
?	앞 문자가 0 또는 1회 매치 (확장 정규 표현식)
+	앞 문자가 1회 이상 매치 (확장 정규 표현식)
|	표현식 논리 OR (확장 정규 표현식)

### 2. grep 명령어 옵션.
grep 명령에서 사용할 수 있는 옵션은 아래와 같습니다. (grep 명령에 대한 더 자세한 옵션은 "grep --help" 명령을 통해 확인할 수 있습니다.)

    grep [OPTION...] PATTERN [FILE...]
        -E        : PATTERN을 확장 정규 표현식(Extended RegEx)으로 해석.
        -F        : PATTERN을 정규 표현식(RegEx)이 아닌 일반 문자열로 해석.
        -G        : PATTERN을 기본 정규 표현식(Basic RegEx)으로 해석.
        -P        : PATTERN을 Perl 정규 표현식(Perl RegEx)으로 해석.
        -e        : 매칭을 위한 PATTERN 전달.
        -f        : 파일에 기록된 내용을 PATTERN으로 사용.
        -i        : 대/소문자 무시.
        -v        : 매칭되는 PATTERN이 존재하지 않는 라인 선택.
        -w        : 단어(word) 단위로 매칭.
        -x        : 라인(line) 단위로 매칭.
        -z        : 라인을 newline(\n)이 아닌 NULL(\0)로 구분.
        -m        : 최대 검색 결과 갯수 제한.
        -b        : 패턴이 매치된 각 라인(-o 사용 시 문자열)의 바이트 옵셋 출력.
        -n        : 검색 결과 출력 라인 앞에 라인 번호 출력.
        -H        : 검색 결과 출력 라인 앞에 파일 이름 표시.
        -h        : 검색 결과 출력 시, 파일 이름 무시.
        -o        : 매치되는 문자열만 표시.
        -q        : 검색 결과 출력하지 않음.
        -a        : 바이너리 파일을 텍스트 파일처럼 처리.
        -I        : 바이너리 파일은 검사하지 않음.
        -d        : 디렉토리 처리 방식 지정. (read, recurse, skip)
        -D        : 장치 파일 처리 방식 지정. (read, skip)
        -r        : 하위 디렉토리 탐색.
        -R        : 심볼릭 링크를 따라가며 모든 하위 디렉토리 탐색.
        -L        : PATTERN이 존재하지 않는 파일 이름만 표시.
        -l        : 패턴이 존재하는 파일 이름만 표시.
        -c        : 파일 당 패턴이 일치하는 라인의 갯수 출력.

### 3. grep 명령 사용 예제.
grep을 사용하여 파일로부터 문자열을 검색하는 방법은 아래와 같습니다.


```
$ grep [OPTION] [PATTERN] [FILE]
```

아래는 "FILE.txt"의 내용에서 "PAT"라는 문자열을 검색하고, 문자열이 존재하는 라인을 출력하는 예제입니다. 기본적으로 대소문자를 구분한다는 점에 주의하세요.

```
$ cat FILE.txt
grep searches for PATTERNS in each FILE.
PATTERNS is one or patterns separated by newline characters.
And grep prints each line that matches a pattern.
$ grep "PAT" FILE.txt
grep searches for PATTERNS in each FILE.
PATTERNS is one or patterns separated by newline characters.
```

자주 사용하는 grep 명령어 사용 예제는 아래와 같습니다. 각 항목의 링크를 선택하면, 좀 더 자세한 설명과 사용 예제를 확인할 수 있습니다.



grep 사용 예	명령어 옵션
대상 파일에서 문자열 검색	grep "STR" [FILE]
현재 디렉토리 모든 파일에서 문자열 검색	grep "STR" *
특정 확장자를 가진 모든 파일에서 문자열 검색	grep "STR" *.ext
대소문자 구분하지 않고 문자열 검색	grep -i "STR" [FILE]
매칭되는 PATTERN이 존재하지 않는 라인 선택	grep -v "STR" [FILE]
단어(Word) 단위로 문자열 검색	grep -w "STR" [FILE]
검색된 문자열이 포함된 라인 번호 출력	grep -n "STR" [FILE]
하위 디렉토리를 포함한 모든 파일에서 문자열 검색	grep -r "STR" *
최대 검색 결과 갯수 제한	grep -m 100 "STR" FILE
검색 결과 앞에 파일 이름 표시	grep -H "STR" *
문자열 A로 시작하여 문자열 B로 끝나는 패턴 찾기	grep "A.*B" *
0-9 사이 숫자만 변경되는 패턴 찾기	grep "STR[0-9]" *
문자열 패턴 전체를 정규 표현식 메타 문자가 아닌
일반 문자로 검색하기	grep -F "*[]?..." [FILE]
정규 표현식 메타 문자를 일반 문자로 검색하기	grep "\*" [FILE]
문자열 라인 처음 시작 패턴 검색하기	grep "^STR" [FILE]
문자열 라인 마지막 종료 패턴 검색하기	grep "$STR" [FILE]


#### 3.1 대상 파일에서 문자열 검색.
grep 명령에 문자열과 파일 이름을 지정하여, 파일에서 문자열을 검색할 수 있습니다. 이 때 문자열 검색 결과는 문자열이 포함된 라인 단위로 출력됩니다.

$ grep "STR" FILE1.txt         > FILE.txt에서 "STR" 문자열 검색.
```
$ cat FILE1.txt
grep searches for PATTERNS in each FILE.
PATTERNS is one or patterns separated by newline characters.
And grep prints each line that matches a pattern.
$ grep "PAT" FILE.txt
grep searches for PATTERNS in each FILE.
PATTERNS is one or patterns separated by newline characters.
```

#### 3.2 현재 디렉토리 모든 파일에서 문자열 검색
파일 이름에 "*" 문자를 사용하여, 현재 디렉토리에 있는 모든 파일에서 문자열을 검색할 수 있습니다. 단, 현재 디렉토리에 포함된 하위 디렉토리에 있는 파일은 탐색하지 않습니다. (하위 디렉토리를 탐색하려면 -r 옵션 사용.)

$ grep "STR" *                > 현재 디렉토리 모든 파일에서 "STR" 문자열 검색.
```
$ ls
FILE1.txt  FILE2.txt
$ grep "PAT" *
FILE1.txt:grep searches for PATTERNS in each FILE.
FILE1.txt:PATTERNS is one or patterns separated by newline characters.
FILE2.txt:grep searches for PATTERNS in each FILE.
FILE2.txt:PATTERNS is one or patterns separated by newline characters.
```

#### 3.3 특정 확장자를 가진 모든 파일에서 문자열 검색
파일 이름 확장자 앞에 "*" 문자를 사용하여, 특정 확장자를 가진 모든 파일에서 문자열을 검색할 수 있습니다.

$ grep "STR" *.ext            > ext 확장자를 가진 파일에서 "STR" 문자열 검색.
```
$ ls
A.c  A.h  B.c  B.h 
$ grep "include" *.h
A.h:#include <stdio.h>
B.h:#include <string.h"
```

#### 3.4 대소문자 구분하지 않고 문자열 검색
grep 명령에 "-i" 옵션을 사용하여, 대소문자 구분없이 문자열을 검색할 수 있습니다.

grep -i "STR" FILE.txt        > FILE.txt 파일에서 대소문자 구분없이(STR, str) 문자열 검색.
```
$ cat FILE1.txt
grep searches for PATTERNS in each FILE.
PATTERNS is one or patterns separated by newline characters.
And grep prints each line that matches a pattern.
$ grep -i "Pat" FILE1.txt
grep searches for PATTERNS in each FILE.
PATTERNS is one or patterns separated by newline characters.
And grep prints each line that matches a pattern.
```

#### 3.5 매칭되는 PATTERN이 존재하지 않는 라인 선택
어떤 경우에는, 문자열이 매칭되는 라인이 아닌, 매칭되는 패턴이 존재하지 않는 라인을 선택해야 하는 경우가 있습니다. 이 때, "-v" 옵션을 사용합니다.

grep -v "STR" FILE.txt        > FILE.txt 파일에서 "STR"이 포함되지 않은 라인 표시.
```
$ cat FILE1.txt
grep searches for PATTERNS in each FILE.
PATTERNS is one or patterns separated by newline characters.
And grep prints each line that matches a pattern.
$ grep -v "PAT" FILE1.txt
And grep prints each line that matches a pattern.
```

#### 3.6 단어(Word) 단위로 문자열 검색
"-w" 옵션을 사용하면, 단어(Word) 단위로 문자열을 검색할 수 있습니다.

grep -w "STRING" FILE.txt     > FILE.txt 파일에서 "STRING"이라는 문자열(단어 단위) 검색.
```
$ cat FILE1.txt
grep searches for PATTERNS in each FILE.
PATTERNS is one or patterns separated by newline characters.
And grep prints each line that matches a pattern.
$ grep -w "PAT" FILE1.txt
$ grep -w "PATTERNS" FILE1.txt
grep searches for PATTERNS in each FILE.
PATTERNS is one or patterns separated by newline characters.
```

#### 3.7 검색된 문자열이 포함된 라인 번호 출력
"-n" 옵션을 사용하여, 검색 결과가 포함된 라인 번호를 출력할 수 있습니다.

grep -n "STR" FILE.txt        > "STR"이 포함된 라인 번호 출력.
```
$ cat FILE1.txt
grep searches for PATTERNS in each FILE.
PATTERNS is one or patterns separated by newline characters.
And grep prints each line that matches a pattern.
$ grep -n "PAT" FILE1.txt
1:grep searches for PATTERNS in each FILE.
2:PATTERNS is one or patterns separated by newline characters.
```

#### 3.8 하위 디렉토리를 포함한 모든 파일에서 문자열 검색
"-r" 옵션을 사용하면, 하위 디렉토리를 포함한 모든 파일에서 문자열을 검색할 수 있습니다.

grep -r "STR" *               > "STR"이 포함된 라인 번호 출력.
```
$ grep -r "PAT" *
DIR_1/FILE1.txt:grep searches for PATTERNS in each FILE.
DIR_1/FILE1.txt:PATTERNS is one or patterns separated by newline characters.
FILE1.txt:grep searches for PATTERNS in each FILE.
FILE1.txt:PATTERNS is one or patterns separated by newline characters.
FILE2.txt:grep searches for PATTERNS in each FILE.
FILE2.txt:PATTERNS is one or patterns separated by newline characters.
```

#### 3.9 최대 검색 결과 갯수 제한
grep 명령의 결과가 너무 많이 표시될 때, "-m" 옵션을 사용하여 최대 표시 결과를 제한할 수 있습니다.

grep -m 100 "STR" FILE.txt    > FILE.txt 파일에서 문자열 "STR"이 포함된 결과를 100개까지만 표시.
```
$ cat FILE1.txt
grep searches for PATTERNS in each FILE.
PATTERNS is one or patterns separated by newline characters.
And grep prints each line that matches a pattern.
$ grep -n "PAT" FILE1.txt
1:grep searches for PATTERNS in each FILE.
2:PATTERNS is one or patterns separated by newline characters.
$ grep -m 1 "PAT" FILE1.txt
grep searches for PATTERNS in each FILE.
```

#### 3.10 검색 결과 앞에 파일 이름 표시
"-H" 옵션을 사용하여 검색 결과 앞에 파일 이름을 표시할 수 있습니다.

grep -H "STR" *               > "STR"이 포함된 파일 이름 표시.
grep -Hn "STR" *              > "STR"이 포함된 파일 이름과 라인 번호 표시.
```
$ grep -H "PAT" *
FILE1.txt:grep searches for PATTERNS in each FILE.
FILE1.txt:PATTERNS is one or patterns separated by newline characters.
$ grep -Hn "PAT" *
FILE1.txt:1:grep searches for PATTERNS in each FILE.
FILE1.txt:2:PATTERNS is one or patterns separated by newline characters.
```

#### 3.11 문자열 A로 시작하여 문자열 B로 끝나는 패턴 찾기
정규 표현식에서 "."와 "*"를 조합하여 문자열 A로 시작하여 문자열 B로 끝나는 패턴을 찾을 수 있습니다.

grep "the.*step" *            > "the"로 시작하여 "step"으로 끝나는 패턴 검색.
grep "A.*Z" *                 > "A"로 시작하여 "Z"로 끝나는 패턴 검색.
```
$ cat FILE1.txt
the first step  : edit text file.
the second step : save the file.
the third step  : copy to usb.
$ grep -n "the.*step" FILE1.txt
1:the first step  : edit text file.
2:the second step : save the file.
3:the third step  : copy to usb.
$ cat FILE2.txt
ABCDEFGHIJKLMNOPQRSTUVWXYZ
BCD
XYZ
ABZ
$ grep -n "A.*Z" FILE2.txt
1:ABCDEFGHIJKLMNOPQRSTUVWXYZ
4:ABZ
```

#### 3.12 [0-9] 사이 숫자만 변경되는 패턴 찾기
정규 표현식 "[]"를 사용하여 0-9 사이 숫자만 변경되는 문자열 패턴을 검색할 수 있습니다.

grep step[0-9] *              > "step0", "step1", ..., "step9" 패턴을 검색.
```
$ cat FILE3.txt
step0  : edit text file.
step1  : save the file.
step2  : copy to usb.
$ grep -n step[0-9] FILE3.txt
1:step0  : edit text file.
2:step1  : save the file.
3:step2  : copy to usb.
```

#### 3.13 문자열 패턴 전체를 정규 표현식 메타 문자가 아닌 일반 문자로 검색하기
"-F" 옵션을 사용하면, 패턴에 지정된 문자열을 메타 문자로 인식하지 않고 일반 문자로 인식하여 패턴을 검색합니다.

grep -f "[0-9]" *             > "[0-9]" 문자열 검색.
```
$ cat FILE4.txt
01234567890
[0-9]
12345
$ grep -n "[0-9]" FILE4.txt
1:01234567890
2:[0-9]
3:12345
$ grep -Fn "[0-9]" FILE4.txt
2:[0-9]
```

#### 3.14 정규 표현식 메타 문자를 일반 문자로 검색하기
문자열 패턴에서 정규 표현식 메타 문자 앞에 "\"(백슬래시)를 사용하면, 해당 문자를 일반 문자로 인식하게 만들 수 있습니다.

grep "\*" FILE.txt            > FILE.txt 파일에서 * 문자 검색.
grep "\." FILE.txt            > FILE.txt 파일에서 . 문자 검색.
```
$ cat FILE5.txt
* step 1
1. sample text 1
2. sample text 2
$ grep "\*" FILE5.txt
* step 1
$ grep "." FILE5.txt
* step 1
1. sample text 1
2. sample text 2
$ grep "\." FILE5.txt
1. sample text 1
2. sample text 2
```

#### 3.15 문자열 라인의 처음 시작 패턴 검색하기.
정규 표현식 "^"를 사용하여 문자열 라인의 중간이 아닌 시작 패턴만 검색할 수 있습니다.

grep "^C" FILE.txt            > FILE.txt 에서 C로 시작하는 라인 검색.
grep "^1" FILE.txt            > FILE.txt 에서 "1"으로 시작하는 라인 검색.
```
$ cat FILE5.txt
* step 1
1. sample text 1
2. sample text 2
$ grep "^1" FILE5.txt
1. sample text 1
```

#### 3.16 문자열 라인 마지막 종료 패턴 검색하기.
정규 표현식 "$"를 사용하여 문자열 라인의 처음 또는 중간이 아닌 종료 패턴을 검색할 수 있습니다.

grep "\.$" FILE.txt           > FILE.txt "." 으로 끝나는 라인 검색.
grep -v "\.$" FILE.txt        > FILE.txt "." 으로 끝나지 않는 라인 검색.
```
$ cat FILE6.txt
..............
.............?
ABCDEFGHIJKLM.
$ grep "\.$" FILE6.txt
..............
ABCDEFGHIJKLM.
$ grep -v "\.$" FILE6.txt
.............?
```

### 4. 참고.
Man7 Linux Manual Page - grep
[Man7. man. grep] 내용을 참고하세요.
Wiki - 정규 표현식 (Regular Expression)
[Wiki - 정규 표현식] 내용을 참고하세요.

### References
https://recipes4dev.tistory.com/157