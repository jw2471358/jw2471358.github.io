---
layout: post
title: TypeScript 란?
subtitle: 
description: TypeScript 란?
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_760/v1591001871/dev/ts_overview_ibhqxe.jpg
category: TypeScript
tags:
  - developer
author: jw2471358
---

### TypeScript
TypeScript 는 Microsoft에서 개발하고 유지 관리 하는 오픈 소스 프로그래밍 언어 입니다. JavaScript 의 strict syntactical superset 이며 언어에 선택적 static typing 을 추가합니다. TypeScript는 대규모 응용 프로그램 개발을 위해 설계되었으며 JavaScript로 transcompiles 됩니다. TypeScript는 JavaScript의 상위 집합이므로 기존 JavaScript 프로그램도 유효한 TypeScript 프로그램입니다.

TypeScript는 Node.js 또는 Deno 와 같이 클라이언트 측 및 서버 측 실행 을위한 JavaScript 응용 프로그램을 개발하는 데 사용될 수 있습니다. 트랜스 컴파일에 사용할 수있는 여러 옵션이 있습니다. 기본 TypeScript Checker를 사용 하거나 또는 Babel 컴파일러를 호출하여 TypeScript를 JavaScript로 변환 할 수 있습니다.

TypeScript는 C++ 헤더 파일 이 기존 객체 파일의 구조를 설명할 수 있는 것처럼 기존 JavaScript 라이브러리의 유형 정보를 포함 할 수 있는 definition files 을 지원 합니다. 이렇게하면 다른 프로그램이 파일에 정의된 값을 마치 정적으로 유형이 지정된 TypeScript 엔터티 인 것처럼 사용할 수 있습니다. jQuery, MongoDB 및 D3.js 와 같이 널리 사용되는 라이브러리에 대한 타사 헤더 파일이 있습니다. Node.js 기본 모듈 용 TypeScript 헤더도 제공되므로 TypeScript 내에서 Node.js 프로그램을 개발할 수 있습니다.

TypeScript 컴파일러 자체는 TypeScript로 작성되어 JavaScript로 컴파일 됩니다. Apache License 2.0에 따라 라이센스가 부여됩니다. TypeScript는 C # 및 기타 Microsoft 언어 외에 Microsoft Visual Studio 2013 업데이트 2 이상 에서 일류 프로그래밍 언어로 포함되어 있습니다. 공식 확장을 통해 Visual Studio 2012는 TypeScript도 지원할 수 있습니다. Anders Hejlsberg, 리드의 건축가 C# 과의 창조자 델파이 와 터보 파스칼, 타이프의 개발에 근무하고있다.

### History
TypeScript는 Microsoft에서 2 년간 내부 개발 한 후 2012 년 10 월 (버전 0.8)에 처음 공개되었습니다. 발표 후 곧 Miguel de Icaza 는 언어 자체를 칭찬했지만 당시에는 Linux 및 OS X에서 사용할 수 없었던 Microsoft Visual Studio를 제외하고는 성숙한 IDE 지원이 부족하다는 비판을 받았다. 오늘날 Palantir Technologies 에서 제공하는 플러그인을 통해 다른 IDE, 특히 Eclipse 에서 지원됩니다. Emacs, Vim, Webstorm, Atom을 포함한 다양한 텍스트 편집기와 Microsoft 자체의 Visual Studio Code 도 TypeScript를 지원합니다.

2013 년에 출시 된 TypeScript 0.9는 제네릭에 대한 지원을 추가했습니다. TypeScript 1.0은 2014 년 Microsoft의 Build 개발자 회의에서 발표되었습니다. Visual Studio 2013 업데이트 2는 TypeScript를 기본적으로 지원합니다.

2014 년 7 월에 개발 팀은 5 배의 성능 향상을 주장하는 새로운 TypeScript 컴파일러를 발표했습니다. 동시에 CodePlex 에서 처음 호스팅되었던 소스 코드 는 GitHub 로 옮겨졌습니다.

2016 년 9 월 22 일에 TypeScript 2.0이 릴리스되었습니다. 또한 프로그래머가 변수에 null값 이 할당되는 것을 선택적으로 방지할 수있는 기능을 포함하여 몇 가지 기능을 도입했습니다. 때로는 수십억 달러의 실수라고도 합니다.

TypeScript 3.0은 2018 년 7 월 30 일에 릴리스되었으며 나머지 매개 변수 및 스프레드 표현식의 tuples, tuples 유형의 나머지 매개 변수, 일반 나머지 매개 변수 등과 같은 많은 언어 추가 기능을 제공합니다.

### Design
TypeScript는 Microsoft와 외부 고객 모두에서 대규모 응용 프로그램을 개발하기 위한 JavaScript의 단점에서 비롯되었습니다. 복잡한 자바 스크립트 코드 처리와 도전은 언어의 구성 요소의 개발을 쉽게하기 위해 사용자 정의 도구에 대한 수요가 되었다.

TypeScript 개발자는 표준 및 플랫폼 간 지원과 호환되지 않는 솔루션을 찾고있었습니다. 현재 ECMAScript 표준 제안이 클래스 기반 프로그래밍에 대한 향후 지원을 약속한다는 것을 알고 TypeScript는 해당 제안을 기반으로했습니다. 이로 인해 제안에 기반한 superset 구문 언어 확장 세트가 포함 된 JavaScript 컴파일러가 확장을 일반 JavaScript로 변환합니다. 이러한 의미에서 TypeScript는 ECMAScript 2015에 대한 미리보기입니다. 제안서에는 없지만 TypeScript에 추가 된 고유한 측면은 정적 언어 분석을 가능하게 하는 선택적인 정적 타이핑 으로 툴링 및 IDE 지원을 용이하게 합니다.

ECMAScript 2015 지원 
주요 기사 : ECMAScript § 6th Edition-ECMAScript 2015
TypeScript는 ECMAScript 2015 표준에 정의 된 클래스, 모듈 및 화살표 함수 구문과 같은 기능에 대한 지원을 추가합니다.

### Features 
TypeScript는 ECMAScript 6에 기능을 추가하는 언어 확장입니다 . 추가 기능은 다음과 같습니다.
- Type annotations and compile-time type checking (타입 주석과 컴파일 타임 타입 검사)
- Type inference (타입 추론)
- Type erasure (유형 삭제)
- Interfaces (인터페이스)
- Enumerated types (열거 형)
- Generics (제네릭)
- Namespaces (네임 스페이스)
- Tuples (튜플)
- Async/await (비동기 / 대기)
다음 기능은 ECMAScript 2015에서 백 포트되었습니다.
- Classes (클래스)
- Modules (모듈)
- Abbreviated "arrow" syntax for anonymous functions (익명 함수의 약자 "화살표" 구문)
- Optional parameters and default parameters (선택적 매개 변수 및 기본 매개 변수)
문법적으로 TypeScript는 정적 입력 및 클래스, 상속, 인터페이스 및 네임 스페이스와 같은 고전적인 객체 지향 언어 기능에 대한 지원을 추가 한 ECMA-262 언어 표준의 또 다른 Microsoft 구현 인 JScript .NET 과 매우 유사 합니다.

#### Type annotations (타입 주석)
타이프 라이터가 제공하는 정적 타이핑을 가능하게 하는 유형 약어를 통해 유형 검사에서 컴파일 시간을 . 이것은 선택 사항이며 JavaScript 의 일반적인 동적 입력을 사용하기 위해 무시할 수 있습니다 .
```typescript
function add(left: number, right: number): number {
	return left + right;
}
```
원시 유형에 대한 주석이다 number, boolean하고 string. 약하거나 동적으로 유형이 지정된 구조는 유형 any입니다.

JavaScript로 이미 컴파일 된 형식을 사용하여 TypeScript 스크립트에서 형식 정보를 사용할 수 있도록 형식 주석을 별도의 선언 파일 로 내보낼 수 있습니다 . Node.js 및 jQuery에서 와 같이 기존 JavaScript 라이브러리에 주석을 선언 할 수 있습니다 .

TypeScript 컴파일러는 형식이 제공되지 않은 경우 형식을 유추 하기 위해 형식 유추 를 사용 합니다. 예를 들어, add위의 코드 에서 메소드는 number리턴 유형 어노테이션이 제공되지 않은 경우에도 리턴하는 것으로 추론 됩니다. 이것은 정적 유형 left과 right존재를 기반으로하며 numbers, 2를 더한 결과 numbers는 항상이라는 컴파일러의 지식입니다 number. 그러나 반환 유형을 명시 적으로 선언하면 컴파일러가 정확성을 확인할 수 있습니다.

선언 부족으로 인해 유형을 유추 할 수없는 경우 기본값은 동적 any유형입니다. 의 값 any타입은 자바 스크립트의 값과 최소 정적 타입 검사가 연산에 대해 수행되는 동일한 동작을 지원 any값.

#### Declaration files (선언 파일)
TypeScript 스크립트가 컴파일되면 컴파일 된 JavaScript 의 구성 요소 에 대한 인터페이스 역할을하는 선언 파일 (확장명 .d.ts) 을 생성하는 옵션이 있습니다. 프로세스에서 컴파일러는 모든 함수 및 메소드 본문을 제거하고 내 보낸 유형의 서명 만 보존합니다. 그런 다음 결과 선언 파일을 사용하여 타사 개발자가 TypeScript에서이를 사용하는 경우 JavaScript 라이브러리 또는 모듈의 내 보낸 가상 TypeScript 유형을 설명 할 수 있습니다.

선언 파일의 개념은 C / C ++에 있는 헤더 파일 의 개념과 유사합니다 .
```c++
declare ​namespace arithmetics {
   ​add(left: number, right: number): number;
   ​subtract(left: number, right: number): number;
   ​multiply(left: number, right: number): number;
   ​divide(left: number, right: number): number;
}
```
jQuery 및 Node.js와 마찬가지로 기존 JavaScript 라이브러리에 대해 유형 선언 파일을 직접 작성할 수 있습니다.

많이 사용되는 JavaScript 라이브러리를위한 대규모 선언 파일 모음은 GitHub의 DefinitelyTyped 에서 호스팅됩니다 .

#### Class 
TypeScript는 선택적 형식 주석 지원을 통합하는 ECMAScript 2015 클래스를 지원합니다.
```typescript
class ​Person {
   ​private name: string;
   ​private age: number;
   ​private salary: number;

   ​constructor(name: string, age: number, salary: number) {
       ​this.name = name;
       ​this.age = age;
       ​this.salary = salary;
   ​}

   ​toString(): string {
       ​return `${this.name} (${this.age}) (${this.salary})`; // As of version 1.4
   ​}
}
```

#### Generic 
TypeScript는 일반 프로그래밍을 지원합니다. 다음은 예이다 항등 함수.

```typescript
function doSomething<T>(arg: T): T {
    return arg;
}
```

#### Modules and namespaces (모듈과 네임 스페이스)
TypeScript는 모듈과 네임 스페이스를 구분합니다. TypeScript의 두 기능은 클래스, 인터페이스, 함수 및 변수를 컨테이너에 캡슐화하는 것을 지원합니다. 네임 스페이스 (이전의 내부 모듈)는 즉시 호출 된 JavaScript의 함수 표현식 을 사용하여 코드를 캡슐화하는 반면 모듈 (이전의 외부 모듈)은 JavaScript 라이브러리 패턴을 사용하여이를 수행합니다 ( AMD 또는 CommonJS ).



### 개발 도구 
#### 컴파일러 
라는 TypeScript 컴파일러 는 TypeScripttsc 로 작성됩니다 . 결과적으로 일반 JavaScript로 컴파일 된 다음 모든 JavaScript 엔진 (예 : 브라우저)에서 실행할 수 있습니다. 컴파일러 패키지에는 컴파일러를 실행할 수있는 스크립트 호스트가 번들로 제공됩니다. Node.js를 호스트로 사용 하는 Node.js 패키지 로도 제공됩니다 .

JavaScript에는 클라이언트 버전 컴파일러 의 알파 버전이 있으며 페이지로드시 즉시 TypeScript 코드를 실행합니다.

컴파일러의 현재 버전은 기본적으로 ECMAScript 5를 지원합니다. ECMAScript 2015를 대상으로하여 해당 버전 전용 언어 기능 (예 : 생성기)을 사용할 수있는 옵션이 있습니다. ECMAScript 2015 표준의 일부 임에도 불구하고 클래스는 두 모드에서 모두 사용할 수 있습니다.

#### IDE 및 편집기 지원 
Microsoft 는 Visual Studio 2012 및 WebMatrix 용 플러그인 , Visual Studio 2013 , Visual Studio 2015의 완벽한 통합 지원 및 Emacs 및 Vim에 대한 기본 텍스트 편집기 지원을 제공합니다 .
Visual Studio Code 는 Microsoft가 Electron을 기반으로 개발 한 (주로) 오픈 소스 크로스 플랫폼 소스 코드 편집기입니다 . 다른 언어 외에도 TypeScript를 지원하며 디버깅 및 지능형 코드 완성 과 같은 기능을 제공합니다 .
alm.tools는 TypeScript, ReactJS 및 TypeStyle을 사용하여 빌드 한 TypeScript 용 오픈 소스 클라우드 IDE입니다.
JetBrains의이 리팩토링과 같은 인 IntelliJ 플랫폼을 기반으로 자사의 IDE에서 디버깅, 코드 완성과 타이프 라이터를 지원 PhpStorm 6, WebStorm 6, 인 IntelliJ의 IDEA, 뿐만 아니라 자신의 비주얼 스튜디오 추가 기능으로 및 확장, ReSharper에서 8.1.
아톰 에 의해 타이프 플러그인이 Basarat을 코드 완성, 탐색, 서식, 빠른 편집을 지원.
온라인 Cloud9 IDE 및 Codenvy는 TypeScript를 지원합니다.
NetBeans IDE 용 플러그인을 사용할 수 있습니다 .
Eclipse IDE (버전 Kepler) 용 플러그인 사용 가능
TypEcs는 Eclipse IDE에서 사용할 수 있습니다 .
Cross Platform Cloud IDE Codeanywhere 는 TypeScript를 지원합니다.
Webclipse TypeScript 및 Angular 2 를 개발하도록 설계된 Eclipse 플러그인입니다 .
Angular IDE 통합 터미널 지원 기능이있는 TypeScript 및 Angular 2 응용 프로그램을 개발하기 위해 npm을 통해 사용할 수있는 독립 실행 형 IDE입니다.
조수 – Emacs를 위한 TypeScript 대화식 개발 환경 .

#### 빌드 자동화 도구와 통합 
플러그인을 사용하여 TypeScript 를 Grunt (grunt-ts), Apache Maven (TypeScript Maven Plugin), Gulp (gulp -typescript) 및 Gradle (TypeScript Gradle )을 포함한 빌드 자동화 도구 와 통합 할 수 있습니다 . 플러그인).

#### Linting tools
TSLint 은 일련의 표준 및 지침을 준수하는지 TypeScript 코드를 스캔합니다. ESLint , 표준 자바 스크립트 린터은 또한 지역 사회의 플러그인을 통해 타이프 라이터에 대한 몇 가지 지원을 제공했다. 그러나 ESLint가 TypeScript의 언어 서비스를 활용할 수 없었기 때문에 특정 형태의 의미 론적 보푸라기와 프로그램 전체 분석이 불가능했습니다.  2019 년 초 TSLint 팀은 typescript-eslint성능, 커뮤니티 통합 및 개발자 접근성 향상을 위해 ESLint 우산 아래 린트를 통합하기 위해 TSLint, ESLint 및 TypeScript 팀의 공동 노력을 위해 린터의 지원 중단을 발표했습니다 . ESLint와 함께 TypeScript를 사용하려면 @typescript-eslint/eslint-plugin및 을 추가해야합니다 @typescript-eslint/parser.

### References
<https://en.wikipedia.org/wiki/TypeScript>
