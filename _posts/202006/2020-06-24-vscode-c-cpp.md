---
layout: post
title: VS Code에 C/C++ 확장하기
subtitle: 
description: VS Code에 C/C++ 확장하기
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/me/vs_code_extentions_c_cplusplus_k2czjh.jpg
category: VS Code C/C++
tags:
  - VS Code
  - C/C++
author: jw2471358
---

VS Code > Extentions

1) C/C++ for Visual Studio Code 설치한다.

2) 윈도우에서 gcc, g++ 컴파일하기 위해서 MinGW 라는 프로그램을 설치한다.
<https://sourceforge.net/projects/mingw/files/>

![placeholder](https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1592579222/me/mingw_install_h51res.jpg)

체크박스 클릭(Mark for installation)
mingw-developer-toolkit, mingw32-base, mingw32-gcc-g++, msys-base

메뉴 Installation > Apply Changes : Apply 버튼 클릭

3) 시스템 환경 변수 > 환경변수 > 시스템 변수 설정
Path : C:\MinGW\bin

명령 프롬프트에서 확인  
gcc -v  
g++ -v  

```cmd
C:\Users\user>gcc -v
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=c:/mingw/bin/../libexec/gcc/mingw32/6.3.0/lto-wrapper.exe
Target: mingw32
Configured with: ../src/gcc-6.3.0/configure --build=x86_64-pc-linux-gnu --host=mingw32 --target=mingw32 --with-gmp=/mingw --with-mpfr --with-mpc=/mingw --with-isl=/mingw --prefix=/mingw --disable-win32-registry --with-arch=i586 --with-tune=generic --enable-languages=c,c++,objc,obj-c++,fortran,ada --with-pkgversion='MinGW.org GCC-6.3.0-1' --enable-static --enable-shared --enable-threads --with-dwarf2 --disable-sjlj-exceptions --enable-version-specific-runtime-libs --with-libiconv-prefix=/mingw --with-libintl-prefix=/mingw --enable-libstdcxx-debug --enable-libgomp --disable-libvtv --enable-nls
Thread model: win32
gcc version 6.3.0 (MinGW.org GCC-6.3.0-1)

C:\Users\user>g++ -v
Using built-in specs.
COLLECT_GCC=g++
COLLECT_LTO_WRAPPER=c:/mingw/bin/../libexec/gcc/mingw32/6.3.0/lto-wrapper.exe
Target: mingw32
Configured with: ../src/gcc-6.3.0/configure --build=x86_64-pc-linux-gnu --host=mingw32 --with-gmp=/mingw --with-mpfr=/mingw --with-mpc=/mingw --with-isl=/mingw --prefix=/mingw --disable-win32-registry --target=mingw32 --with-arch=i586 --enable-languages=c,c++,objc,obj-c++,fortran,ada --with-pkgversion='MinGW.org GCC-6.3.0-1' --enable-static --enable-shared --enable-threads --with-dwarf2 --disable-sjlj-exceptions --enable-version-specific-runtime-libs --with-libiconv-prefix=/mingw --with-libintl-prefix=/mingw --enable-libstdcxx-debug --with-tune=generic --enable-libgomp --disable-libvtv --enable-nls
Thread model: win32
gcc version 6.3.0 (MinGW.org GCC-6.3.0-1)
```

4) VS Code 에서 New File > helloworld.c 을 만든다.

```c
#include <stdio.h>

int main()
{
  printf("Hello, world!\n");

  return 0;
}
```

5) VS Code Terminal > Run Build Task (Ctrl+Shift+B)  
C/C++: gcc.exe build active file

TERMINAL
```
The terminal process terminated with exit code: 1

Terminal will be reused by tasks, press any key to close it.

> Executing task: C:\MinGW\bin\gcc.exe -g c:\blog\jekflix-template\_posts\202006\helloworld.c -o c:\blog\jekflix-template\_posts\202006\helloworld.exe <

The terminal process terminated with exit code: 1

Terminal will be reused by tasks, press any key to close it.
```

tasks.json 설정
```json
{
	"version": "2.0.0",
	"tasks": [
		{
			"type": "shell",
			"label": "C/C++: gcc.exe build active file",
			"command": "C:\\MinGW\\bin\\gcc.exe",
			"args": [
				"-g",
				"${file}",
				"-o",
				"${fileDirname}\\${fileBasenameNoExtension}.exe"
			],
			"options": {
				"cwd": "${workspaceFolder}"
			},
			"problemMatcher": [
				"$gcc"
			],
			"group": "build"
		}
	]
}
```

6) Run > Start Debugging (F5)

launch.json 설정
```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [          
        {
            "name": "C++ Launch (Windows) 시작",
            "type": "cppvsdbg",
            "request": "launch",
            "program": "${fileDirname}\\helloworld.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false
        },
```

DEBUG CONSOLE
-------------------------------------------------------------------
You may only use the C/C++ Extension for Visual Studio Code
with Visual Studio Code, Visual Studio or Visual Studio for Mac
software to help you develop and test your applications.
-------------------------------------------------------------------
Loaded 'C:\blog\jekflix-template\_posts\202006\helloworld.exe'. Module was built without symbols.
Loaded 'C:\Windows\SysWOW64\ntdll.dll'. 
Loaded 'C:\Windows\SysWOW64\kernel32.dll'. 
Loaded 'C:\Windows\SysWOW64\KernelBase.dll'. 
Loaded 'C:\Windows\SysWOW64\msvcrt.dll'. 
Hello, world!
The program '[26700] helloworld.exe' has exited with code 0 (0x0).

### References
<https://m.blog.naver.com/PostView.nhn?blogId=suwon_man91&logNo=221382448285&categoryNo=11&proxyReferer=http:%2F%2Fwww.google.com%2F>
