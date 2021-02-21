---
layout: post
title: 예제로 풀어보는 구글딥러닝 프레임워크 텐서플로우 실전
subtitle: 
description: 예제로 풀어보는 구글딥러닝 프레임워크 텐서플로우 실전
# image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_700/v1593004373/pixabay/landscape-5313115_1920_bse9w2.jpg
category: 
tags:
  - 구글딥러닝
  - 텐서플로우
author: jw24713 블로거
---

Machine Learning

Deep Learning

장저위,구쓰위 지음 | 장우진 옮김


#### 2.2 TensorFlow 설치

#### 2.2.1 Docker 를 이용한 설치

Docker Desktop 3.1.0 를 설치하면 wsl2도 함께 설치한다.

내 pc : Windows10 home wsl2

윈도우 재시작


```
$ docker run -it -p 8888:8888 -p 6006:6006 cargo.caicloud.io/tensorflow/tensorflow:1.0.0
```

위 명령에서 -p 8888:8888은 컨테이너 실행 중인 Jupyter 서비스를 로컬 시스템에 맵핑하므로 브라우저에서 localhost:8888을 열면 Jupyter 인터페이스를 볼 수 있다.

```
$ nvidia-docker run -it -p 8888:8888 -p 6006:6006 cargo.caicloud.io/tensorflow/tensorflow:1.0.0-gpu
```

>https://docs.docker.com/engine/reference/commandline/cli  
http://jupyter.org

#### 2.2.2 pip를 이용한 설치

pip는 Python 소프트웨어 패키지를 설치 및 관리하는 도구로 TensorFlow 패키지 및 TensorFlow에 필요한 의존 패키지를 설치할 수 있다.
현재 일부 운영체제에서만 TensorFlow를 설치할 수 있다.

1) pip 설치

```
# Ubuntu/Linux 64-bit 환경.
$ sudo apt-get install python-pip python-dev

# Mac OS X환경
$ sudo easy_install pip
$ sudo easy_install --upgrade six
```

2) 알맞은 바이너리 URL 선택
- CPU버전의 TensorFlow:

```
# Unbuntu/Linux 64-bit, Python 2.7 환경.
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0-cp27-none-linux_x86_84.whl

# Unbuntu/Linux 64-bit, Python 3.4 환경.
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0-cp34-cp34m-linux_x86_84.whl

# Unbuntu/Linux 64-bit, Python 3.5 환경.
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0-cp35-cp35m-linux_x86_84.whl
```

- GPU 버전의 TensorFlow:

```
# Python 2.7 환경.
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow-1.0.0-cp27-none-linux_x86_84.whl

# Python 3.4 환경.
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow-1.0.0-cp34-cp34m-linux_x86_84.whl

# Python 3.5 환경.
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow-1.0.0-cp35-cp35m-linux_x86_84.whl
```

3) pip를 이용한 TensorFlow 설치

```
# Python 2 환경
$ sudo pip install --upgrade $TF_BINARY_URL

# Python 3 환경
$ sudo pip3 install --upgrade $TF_BINARY_URL
```

#### 2.2.3 소스 코드를 이용한 설치

TensorFlow 소스 코드를 pip 설치 패키지로 컴파일하는 것이다. TensorFlow의 소스 코드를 pip에서 사용되는 wheel 파일로 컴파일한 후, 2.2.2절에 설명된 pip로 설치할 수 있다. TensorFlow 소스 코드를 컴파일하기 전에 먼저 TensorFlow의 의존 패키지 설치 방법을 설명한다.

1) Ubuntu 14.04에서 의존 패키지 설치하기

컴파일 툴인 Bazel을 설치해야 한다. Bazel을 설치하기 위해선 우선 JDK8을 설치해야 한다. JDK8을 설치하는 방법은 아래와 같다.

```
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt-get update
$ sudo apt-get install oracle-java8-installer
```

Bazel에 필요한 소프트웨어를 설치한다.

```
$ sudo apt-get install pkg-config zip g++ zlib1g-dev unzip
```

그런 다음 Bazel의 GitHub 배포 페이지(https://github.com/bazelbuild/bazel/release/tag/0.3.1)에서 설치 패키지를 다운로드한다.
Bazel 설치 과정은 아래 코드와 같다.

```
$chmod +x bazel-0.3.1-jdk7-installer-linux-x86_64.sh
$ ./bazel-0.3.1-jdk7-installer-linux-x86_64.sh -user
$ export PATH="$PATH:$HOME/bin"
```

Bazel의 설치가 완료되면 아래 코드로 TensorFlow의 의존 패키지를 설치해야 한다.

```
# Python 2.7 환경
$ sudo apt-get install python-numpy swig python-dev python-wheel

# Python 3.x 환경
$ sudo apt-get install python3-numpy swig python3-dev python-wheel
```

GPU 지원을 원하면 Nvidia의 Cuda Tookit(7.0 이상)과 cuDNN(v2 이상)을 설치해야 한다. 또한 TensorFlow는 계산 능력이 3.0이 넘는 Nvidia Titan, Nvidia Titan X, Nvidia K20, Nvidia K40 등과 같은 GPU만을 지원한다.

2) Max OS X에서 의존 패키지 설치하기
생략...

Bazel, SWIG, Homebrew

3) TensorFlow 컴파일 환경 구성

모든 의존성 패키지가 설치됐으면 이제 소스 코드를 통해 TensorFlow를 설치할 수 있다.

TensorFlow 소스코드를 받는다.

```
$ git clone https://github.com/tensorflow/tensorflow
```

만일 이전 버전의 TensorFlow를 받고 싶다면, 위의 명령에 -b <branchename> 변수를 추가하면 된다. r0.7, r0.8, r0.9 등이 있다. r0.8 이하 버전을 설치하고 싶다면 --recurse-submodules 변수를 더 추가해 TensorFlow 의존 패키지를 가져와야 한다. 소스 코드의 설치가 완료되면 configure 스크립트를 실행해 환경변수를 설정해야 한다.

```
$ cd tensorflow
$ ./configure
# Python 경로
Please specify the location of python. [Default is /usr/bin/python]:
# 구글 클라우드 플랫폼 지원 여부
Do you wish to build TensorFlow with Google Cloud Platform support? [y/N]N
No Google Cloud Platform support will be enabled for TensorFlow
# GPU 지원 여부 
Do you wish to build TensorFlow with GPU support? [y/N]y
GPU support will be enabled for TensorFlow
# GPU 설정
Please specify whitch gcc nvcc should use as the host compiler. [Default is /usr/bin/gcc]:
# Cuda SDK 버전 설정
...
# Cuda tollkit 디렉토리 설정
...
# Cudnn 버전 설정

# CuDNN 디렉토리 설정

# GPU 계산 능력 설정
```

환경 설정이 끝나면 Bazel을 통해 pip의 설치 패키지를 컴파일하고 pip를 통해 설치한다.

```
$ bazel build -c opt --config=cuda //tensorflow/tools/pip_package/:build_ pip_package
$ bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_ pkg
$ sudo pip install /tmp/tensorflow_pkg/tensorflow-1.0.0-py2-none-any.whl
```

첫 번째 명령에서 --config-cuda 변수는 GPU에 대한 것이다. GPU를 쓰지 않는다면 이 변수는 필요 없다. 마지막 행의 wheel 설치 패키지명(tensorflow-1.0.0-py2-none-any.whl)은 시스템 환경과 관련 있다. pip 설치 전에 ls 명령을 통해 설치 패키지명을 확인할 수 있다.


#### 2.3 TensorFlow 테스트 예제

이 절에서 파이썬의 자체 대화형 인터프리터를 사용하여 다음과 같은 예제를 시연한다.

```
# python
Python 2.7.6 (default, Jun 22 2015, 17:58:13)
[GCC 4.8.2] on linux 2
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

파이썬 인터프리터를 실행해 먼저 import를 통해 TensorFlow를 로드한다.
```
>>> import tensorflow as tf
>>>
```

두 벡터 a와 b를 정의한다.
```
>>> a= tf.constant([1.0,2.0], name="a")
>>> b= tf.constant([2.0,3.0], name="b")
>>> result = a + b
```

더한 결과를 출력하려면 단순히 result를 출력하면 안 되고, 우선 session을 생성하고 이를 통해 계산 결과를 출력할 수 있다. 
```
>>> sess = tf.Session()
>>> sess.run(result)
array(3., 5.], dtype=float32)
```

>http://www.numpy.org


#### References
https://github.com/caicloud/tensorflow-tutorial

