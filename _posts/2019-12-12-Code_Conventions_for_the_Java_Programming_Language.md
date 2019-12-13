---
layout: post
title:  "Java 프로그래밍 언어의 코드 규칙"
date:   2019-12-12
categories: blog
tags: java
comments: true
---
Java 코딩 규칙을 확인 해야할 때 마다 검색하는 것이 귀찮아 웹에 있는 [Java&trade; 프로그래밍 언어의 코드 규칙](https://www.oracle.com/technetwork/java/javase/documentation/codeconvtoc-136057.html)을 구글 번역기로 번역한 후 어색한 내용은 약간 고쳐 보았다.

해당 문서는 다음과 같은 안내 문구와 함께 시작한다.

>#### <center>이 페이지의 정보는 보관 목적만을위한 것입니다.</center>
><center>이 페이지는 적극적으로 관리되지 않습니다. 문서 내의 링크가 작동하지 않을 수 있으며 정보 자체가 더 이상 유효하지 않을 수 있습니다. 이 문서의 마지막 개정은 1999 년 4 월 20 일에 작성되었습니다.</center>

## <center>Java&trade; 프로그래밍 언어의 코드 규칙</center>
<center>1999 년 4 월 20 일 개정</center>

<hr>

### 1 소개

#### 1.1 코드 규칙이있는 이유

코드 규칙은 여러 가지 이유로 프로그래머에게 중요합니다.

- 소프트웨어는 전체 비용의 80%가 유지 관리에 소요 됩니다.
- 원래의 저자가 평생 동안 유지하는 소프트웨어는 거의 없습니다.
- 코드 규칙은 소프트웨어의 가독성을 향상시켜 엔지니어가 새 코드를 보다 빠르고 완벽하게 이해할 수 있도록 합니다.
- 소스 코드를 제품으로 출시하는 경우 당신이 만드는 다른 제품과 마찬가지로 올바르게 포장되었고 깨끗한 지 확인해야 합니다.

#### 1.2 감사의 말

이 문서는 Sun Microsystems, Inc.의 [Java Language Specification](https://docs.oracle.com/javase/specs/)에 제시된 Java 언어 코딩 표준을 반영합니다. 주요 기여자는 Peter King, Patrick Naughton, Mike DeMoney, Jonni Kanerva, Kathy Walrath 및 Scott Hommel입니다.

이 문서의 번안, 수정 또는 재배포에 관한 질문은 저작권 침해 신고서를 읽으십시오.[^1]

이 문서에 대한 의견은 피드백 양식에 제출해야 합니다.[^2]

### 2 파일 이름

이 절에서는 일반적으로 사용되는 파일 확장자와 이름에 대한 규칙을 설명합니다.

#### 2.1 파일 확장자

Java 소프트웨어는 다음과 같은 파일 확장자를 사용합니다.

| 파일 형식 | 확장자 |
|---|---|
| Java 소스 | .java |
| Java 바이트 코드 | .class |

#### 2.2 공통 파일 이름

자주 사용되는 파일 이름은 다음과 같습니다.

| 파일 이름 | 용도 |
|---|---|
| GNUmakefile | make 파일의 이름으로 주로 사용합니다. `gnumake`를 사용하여 소프트웨어를 빌드 한다는 것을 나타냅니다. |
| README | 특정 디렉토리의 내용을 요약하는 파일의 이름으로 주로 사용합니다. |

### 3 파일 구성

파일은 공백 행으로 구분해야 하는 섹션과 각 섹션을 식별하기 위한 선택적 주석으로 구성됩니다.

2000 줄보다 긴 파일은 너무 커서 부담이 되며 피해야합니다.

올바른 형식의 Java 프로그램 예시는 [19 페이지의 "Java 소스 파일 예시"](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-137946.html#182)[^3]를 참조하십시오.

#### 3.1 Java 소스 파일

각 Java 소스 파일은 단일 public 클래스 또는 인터페이스를 포함합니다. private 클래스와 인터페이스가 public 클래스와 관련되어있을 때에는 public 클래스와 동일한 소스 파일에 넣을 수 있습니다. public 클래스는 파일에서 첫 번째 클래스 또는 인터페이스 여야합니다.

Java 소스 파일의 순서는 다음과 같습니다.

- 시작 주석 ([4 페이지의 "시작 주석"](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-141855.html#3441)[^4]참조)
- Package 및 Import 문
- Class 및 Interface 선언 ([4 페이지의 "Class 및 Interface 선언"](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-141855.html#1852)[^5]참조)

##### 3.1.1 시작 주석

모든 소스 파일은 클래스 이름, 버전 정보, 날짜 및 저작권 고지를 나열하는 c-style 주석으로 시작해야합니다.

```java
/*
 * Classname
 * 
 * Version information
 *
 * Date
 * 
 * Copyright notice
 */
```

##### 3.1.2 Package 및 Import 문

대부분의 Java 소스 파일의 첫 번째 행은 주석이 아니라면 `package `문입니다. 그 다음에는 `import` 문을 사용할 수 있습니다.

```java
package java.awt;

import java.awt.peer.CanvasPeer;
```

##### 3.1.3 Class 와 Interface 선언

다음 표에서는 Class 또는 Interface 선언의 일부분들을 나타나는 순서대로 설명합니다. 주석이 포함 된 예시는 [19 페이지의 "Java 소스 파일 예시"](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-137946.html#182)[^3]를 참조하십시오.

|  | Class/Interface 선언의 일부 | 내용 |
|---|---|---|
| 1 | Class/Interface 문서 주석 (`/**...*/`) | 이 주석에 포함되어야 할 내용에 대해서는 [9 페이지의 "문서 주석"](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-141999.html#16838)[^6]을 참조하십시오. |
| 2 | `class` 또는 `interface` 문 |  |
| 3 | 필요한 경우 Class/Interface 구현 주석 (`/*...*/`) | 이 주석은 Class/Interface 문서 주석에 적합하지 않은 클래스 전반 또는 인터페이스 전반의 정보를 포함해야합니다. |
| 4 | Class(`static`) 변수 | 먼저 `public` 클래스 변수, `protected` 클래스 변수, (접근 한정자가 없는) 패키지 수준 클래스 변수, 그리고 `private` 클래스 변수 순서로 선언한다. |
| 5 | Instance 변수 | 먼저 `public`, `protected`, (접근 한정자가 없는) 패키지 수준, `private` 순서로 선언한다. |
| 6 | 생성자 |  |
| 7 | 메소드 | method들은 범위 또는 접근 한정에 의한 것이 아닌 기능별로 그룹화해야합니다. 예를 들어, private 클래스 메소드는 두 개의 public 인스턴스 메소드 사이에있을 수 있습니다. method 그룹화의 목적은 코드를 읽고 이해하는 것이 더 쉽도록 만드는 것입니다. |

### 4 들여 쓰기

들여 쓰기의 단위는 4개의 공백을 사용하는 것이 좋습니다. 들여 쓰기를 어떤 방식(공백으로 할 지, 탭으로 할 지)으로 해야 한다는 규칙은 없습니다. 탭은 정확히 8개의 공백(4개가 아닌)으로 설정해야합니다.

#### 4.1 라인 길이

80자 이상의 행은 많은 터미널과 도구로 잘 처리되지 않으므로 사용하지 마십시오.

>참고 : 문서에 사용 되는 예시는 줄 길이가 더 짧아야 하므로 일반적으로 70자를 넘기지 않습니다.

#### 4.2 줄 바꿈

표현식이 한 줄에 들어 가지 않으면 다음 일반 원칙에 따라 표현식을 분리하십시오.

- 콤마 이후에 분리하십시오.
- 연산자를 포함하여 분리하십시오.
- 낮은 수준 보다 높은 수준에서 표현식 분리하는 것이 좋습니다.
- 새 줄의 시작 부분이 이전 줄과 같은 수준에 위치 하도록 맞춥니다.
- 위의 규칙들로 인해 코드가 혼란 스럽거나 오른쪽 여백 없이 80자를 넘어가는 코드가 생기면, 표현식을 다음 줄로 분리하고 8칸을 들여 씁니다.

다음은 메소드 호출 시 표현식을 분리하는 몇 가지 예시입니다.

```java
someMethod(longExpression1, longExpression2, longExpression3, 
        longExpression4, longExpression5);
 
var = someMethod1(longExpression1,
                someMethod2(longExpression2,
                        longExpression3)); 
```

다음은 산술 식을 분리하는 두 가지 예입니다. 첫 번째 방법은 괄호로 둘러싸인 식 외부(더 높은 수준)에서 산술식을 분리하기 때문에 더 좋습니다.

```java
longName1 = longName2 * (longName3 + longName4 - longName5)
           + 4 * longname6; // PREFER

longName1 = longName2 * (longName3 + longName4
                       - longName5) + 4 * longname6; // AVOID
```
다음은 메소드를 선언할 때 들여쓰기를 사용한 두 가지 예시입니다. 첫 번째는 일반적인 경우입니다. 두 번째는 기존의 들여 쓰기를 사용할 경우 두 번째 줄과 세 번째 줄이 점점 더 오른쪽으로 이동하므로, 8개의 공백 들여 쓰기만 사용하였습니다.

```java
//CONVENTIONAL INDENTATION
someMethod(int anArg, Object anotherArg, String yetAnotherArg,
           Object andStillAnother) {
    ...
}

//INDENT 8 SPACES TO AVOID VERY DEEP INDENTS
private static synchronized horkingLongMethodName(int anArg,
        Object anotherArg, String yetAnotherArg,
        Object andStillAnother) {
    ...
}
```

if 문에 대한 줄 바꿈은 일반적으로 8칸 공백 규칙을 사용해야합니다. 기존 들여쓰기 규칙(4칸 공백)을 사용하면 다음 예시의 첫 번째 처럼 가독성이 떨어집니다.

```java
//DON'T USE THIS INDENTATION
if ((condition1 && condition2)
    || (condition3 && condition4)
    ||!(condition5 && condition6)) { //BAD WRAPS
    doSomethingAboutIt();            //MAKE THIS LINE EASY TO MISS
} 

//USE THIS INDENTATION INSTEAD
if ((condition1 && condition2)
        || (condition3 && condition4)
        ||!(condition5 && condition6)) {
    doSomethingAboutIt();
} 

//OR USE THIS
if ((condition1 && condition2) || (condition3 && condition4)
        ||!(condition5 && condition6)) {
    doSomethingAboutIt();
} 
```

다음은 삼항 연산자를 사용할 때 허용되는 세가지 들여쓰기 방법입니다.

```java
alpha = (aLongBooleanExpression) ? beta : gamma;  

alpha = (aLongBooleanExpression) ? beta
                                 : gamma;  

alpha = (aLongBooleanExpression)
        ? beta 
        : gamma;  
```

### 5 주석

Java 프로그램은 구현 주석과 문서 주석의 두 가지 주석을 가질 수 있습니다. 구현 주석은 C++에서 사용되는 것으로, `/*...*/` 및 `//`로 구분됩니다. 문서 주석은 Java에서만 사용되며 `/**...*/`로 구분됩니다. 문서 주석은 javadoc 도구를 사용하여 HTML 파일로 추출 할 수 있습니다.

구현 주석은 코드를 주석으로 처리하거나 특정 구현에 대한 설명을 주석으로 처리하기위한 것입니다. 문서 주석은 구현의 관점이 아닌 코드의 스펙을 설명하기위한 것으로, 소스 코드를 반드시 가지고 있지 않은 개발자도 읽을 수 있어야 합니다.

주석은 코드에 대한 개요를 제공하고 코드 자체로는 쉽게 파악할 수 없는 추가 정보를 제공하기 위해 사용해야 합니다. 주석은 프로그램을 읽고 이해하는 데 관련된 정보만 포함해야 합니다. 예를 들어, 해당 패키지를 빌드하는 방법 또는 패키지가 포함하고있는 디렉토리에 대한 정보는 주석으로 포함하면 안됩니다.

중요한 내용 또는 명백하지 않은 설계에 대한 논의는 주석으로 적절하지만 코드에 명확하게 나타나 있어 중복이 된다면 주석으로 적절하지 않습니다. 주석의 내용이 코드에도 있는 경우 시간이 지나 코드가 변경된다면 주석의 내용은 구식이 되어 불필요 하므로, 일반적으로 코드가 발전함에 따라 구식이 될 수있는 주석은 피하십시오.

>참고 : 잦은 주석의 사용은 코드의 품질이 좋지 않다는 것을 의미할 수 있습니다. 주석을 달아야만 한다는 느낌이 들면 코드를 더 명확하게 재작성 해야 하는 것은 아닌지 고민해 봐야 합니다.

주석을 별표 또는 기타 문자를 사용한 큰 상자에 넣지 마십시오.
주석에는 폼 피드(form-feed) 및 백스페이스(backspace)와 같은 특수 문자가 포함되어서는 안됩니다.

#### 5.1 구현 주석 형식

프로그램에는 블록(block), 단일 행(single-line), 후행(trailing) 및 줄 끝(end-of-line)과 같은 네 가지 스타일의 구현 주석이 있습니다.

##### 5.1.1 블록(Block) 주석

블록 주석은 파일, 메소드, 자료 구조 및 알고리즘에 대한 설명을 제공하는 데 사용됩니다. 블록 주석은 각 파일의 시작 부분과 각 메소드 앞에 사용될 수 있습니다. 그들은 또한 메소드 내부와 같은 다른 장소에서도 사용될 수 있습니다. 함수 또는 메소드 내부의 블록 주석은 설명하려는 코드와 동일한 레벨로 들여 쓰기되어야 합니다.

블록 주석은 나머지 코드와 구별되도록 빈 줄이 앞에 와야합니다.

```java
/*
 * Here is a block comment.
 */
```         

블록 주석은 `/*-`로 시작할 수 있습니다. `/*-`으로 시작하는 주석은 `indent(1)`[^7]에 의해 변형이 발생하지 않습니다.

```java
/*-
 * Here is a block comment with some very special
 * formatting that I want indent(1) to ignore.
 *
 *    one
 *        two
 *            three
 */
```

>참고 : 여러분이 `indent(1)`을 사용하지 않거나, 다른 사람이 여러분의 코드에서 `indent(1)`을 실행할 가능성이 없다면, 코드에서 `/*-`를 사용할 필요가 없습니다.

[9 페이지의 "문서 주석"](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-141999.html#16838)[^6]도 참조하십시오.

##### 5.1.2 단일 행(Single-Line) 주석

짧은 주석은 뒤 따르는 코드의 들여쓰기 수준에 맞춰 한 줄에 나타낼 수 있습니다. 주석을 한 줄로 작성할 수 없으면 블록 주석 형식을 따라야합니다. ([5.1.1 절 참조](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-141999.html#680)) 단, 한 줄 주석은 앞에 공백 행이 있어야 합니다. 다음은 Java 코드의 단일 행 주석의 예시입니다 ([9 페이지의 "문서 주석"](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-141999.html#16838)[^6]참조).

```java
if (condition) {

    /* Handle the condition. */
    ...
}
```

##### 5.1.3 후행(Trailing) 주석

매우 짧은 주석은 설명하는 코드와 동일한 행에 나타날 수 있지만 구문과 분리되어야 하므로 가능한 많은 공백을 두어야 합니다. 하나 이상의 짧은 주석이 코드 조각에 여러번 나타나면 모두 동일한 탭 설정으로 들여쓰기를 해야 합니다.

다음은 Java 코드에서 후행 주석의 예입니다.

```java
if (a == 2) {
    return TRUE;            /* special case */
} else {
    return isPrime(a);      /* works only for odd a */
}
```

##### 5.1.4 줄 끝(End-Of-Line) 주석

`//` 주석은 완전한 하나의 행 또는 행에서 필요한 부분만을 주석 처리 할 수 있습니다. 텍스트의 주석처리를 위해 연속 된 여러 줄에 사용해서는 안됩니다. 그러나 코드 섹션을 주석 처리하기 위해 연속 된 여러 줄에서 사용하는 것은 가능합니다. 다음은 줄 끝 주석 사용과 관련된 세 가지 스타일의 예시 입니다.

```java
if (foo > 1) {

    // Do a double-flip.
    ...
}
else {
    return false;          // Explain why here.
}
//if (bar > 1) {
//
//    // Do a triple-flip.
//    ...
//}
//else {
//    return false;
//}
```

#### 5.2 문서 주석

>참고 : 여기에 설명 된 주석 형식의 예는 [19 페이지의 "Java 소스 파일 예시"](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-137946.html#182)[^3]를 참조하십시오.

더 상세한 내용은 문서 주석 태그(@return, @ param, @see 등)에 관한 정보를 포함한 ["Javadoc을 위한 문서 주석 작성법(How to Write Doc Comments for Javadoc)"](https://www.oracle.com/technetwork/java/javase/documentation/index-137868.html)을 참조 해주세요.

더 상세한 문서 주석 및 javadoc에 대한 것은 [javadoc 홈 페이지](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-141999.html#)[^8]를 참조 해주세요.

문서 주석은 Java 클래스, 인터페이스, 생성자, 메소드 및 필드를 설명합니다. 각 문서 주석은 `/**...*/` 내에 기술 하며 클래스, 인터페이스 또는 멤버별 주석이 있습니다. 문서 주석은 각 선언 바로 앞에 있어야 합니다.

```java
/**
 * The Example class provides ...
 */
public class Example { ...
```

최상위 클래스와 인터페이스는 들여 쓰여지지 않는 반면 해당 클래스와 인터페이스의 멤버들은 들여쓰기를 해야 합니다. 클래스 및 인터페이스에 대한 문서 주석(`/**`)의 첫 번째 줄은 들여 쓰기를 하지 않습니다. 이후의 문서 주석 줄에는 각각 별표를 세로로 맞추기 위해 공백 1칸 들여 쓰기를 합니다. 생성자를 포함한 멤버는 첫 번째 문서 주석 줄에 4칸, 그 이후에는 5칸 들여 쓰기를 합니다.

문서에 적합하지 않은 클래스, 인터페이스, 변수 또는 메소드에 대한 정보를 제공해야하는 경우 해당 선언 바로 뒤에 블록 주석([5.1.1절 참조](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-141999.html#680)) 또는 단일 행 주석([5.1.2 절 참조](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-141999.html#341))을 사용하십시오. 예를 들어, 클래스 구현에 대한 세부 사항은 클래스 문서 주석에 기술하면 안되며, 클래스 선언 구문 다음에 블록 주석으로 작성해야 합니다.

Java는 주석 뒤에 나타나는 첫 번째 선언을 해당 선언의 문서 주석으로 처리하므로, 메소드 또는 생성자 정의 블록 안에 문서 주석을 작성하면 안됩니다.

### 6 선언

#### 6.1 라인 당 개수

한 줄에 하나의 선언문을 쓰는 것이 좋습니다. 다음 첫 번째 예시가 두 번째 예시 보다 좋습니다.

```java
int level; // indentation level
int size;  // size of table
```

```java
int level, size;
```

다음 예시처럼 같은 줄에 다른 타입을 넣지 마십시오.

```java
int foo,  fooarray[]; //WRONG!
```

>참고 : 위의 예시는 유형과 ID 사이에 하나의 공백을 사용하며, 다음 예시와 같이 탭을 사용할 수 있습니다.

```java
int     level;          // indentation level
int     size;            // size of table
Object  currentEntry;    // currently selected table entry
```

#### 6.2 초기화

변수의 초기값이 어떤 계산에 의존하는 경우를 제외하고는, 로컬 변수는 변수가 선언 된 곳에서 초기화 하십시오.

#### 6.3 위치

선언문은 블록 시작 부분에만 넣으십시오. (블록은 중괄호 "`{`"와 "`}`"로 둘러싸인 코드입니다.) 변수가 당장 사용되지 않는다고 변수 선언을 미루지 마십시오. 변수 선언을 미루는 것은 부주의 한 프로그래머를 혼란스럽게하고 변수가 사용되는 범위 내에서 코드 이식성을 저해할 수 있습니다.

```java
void myMethod() {
    int int1 = 0;         // beginning of method block

    if (condition) {
        int int2 = 0;     // beginning of "if" block
        ...
    }
}
```

변수 선언 위치와 관련된 규칙의 한 가지 예외는 `for` 루프의 인덱스 변수를 선언할 경우 입니다. Java는 `for` 문 내부에 변수를 선언할 수 있습니다.

```java
for (int i = 0; i < maxLoops; i++) { ... }
```

상위 수준에서 선언한 변수를 숨길 수 있는 로컬 변수 선언은 피하십시오. 예를 들어, 다음 처럼 내부 블록에 동일한 변수 이름을 선언하지 마십시오.

```java
int count;
...
myMethod() {
    if (condition) {
        int count = 0;     // AVOID!
        ...
    }
    ...
}
```

#### 6.4 클래스 및 인터페이스 선언

Java 클래스 및 인터페이스를 코딩할 때는 다음 형식 규칙을 따라야 합니다.

- 메소드 이름과 매개 변수 목록이 시작하는 괄호 "`(`" 사이에는 공백을 두지 마십시오.
- 블록을 시작하는 중괄호 "`{`"는 선언문의 줄 끝에 있어야 합니다.
- 블록을 닫는 중괄호 "`}`"는 새로운 줄에, 해당 블럭을 시작하는 선언문과 대응 되도록 들여 쓰기를 해야 합니다. 단, 블록의 내용이 없는 경우 "`}`"는 "`{`"의 바로 뒤에 있어야 합니다.

```java
class Sample extends Object {
    int ivar1;
    int ivar2;

    Sample(int i, int j) {
        ivar1 = i;
        ivar2 = j;
    }

    int emptyMethod() {}

    ...
}
```

- 메소드들은 공백 행을 사용하여 구분합니다.

### 7 문장(Statement) 

#### 7.1 간단한 문장

각 행은 다음 예시와 같이 최대 하나의 문장만을 포함해야 합니다.

```java
argv++;         // Correct
argc--;         // Correct  
argv++; argc--; // AVOID!
```

#### 7.2 복합(Compound) 문장

복합 문장은 나열된 문장들을 중괄호로 묶은 문장 "`{ statements }`"을 포함하는 문장 입니다. 복합 문장의 규칙들을 살펴보겠습니다.

- 복합 문장으로 묶인 문장 들은 복합 문장보다 한 단계 더 들여 쓰기를 해야 합니다.
- 복합 문장을 시작하는 중괄호는 복합 문장이 시작되는 행의 끝에 있어야 합니다. 종료하는 중괄호는 새로운 줄에, 복합 문장의 시작 부분과 동일하게 들여 쓰기를 해야 합니다.
- `if-else` 또는 `for` 문과 같은 제어 구조의 일부인 문장도(심지어 내용이 단일 문장 일지라도) 모두 중괄호로 둘러싸야 합니다. 이렇게 하면 문장을 추가할때 중괄호를 추가하지 않아 발생하는 버그를 막을 수 있습니다.

#### 7.3 return 문

값이 있는 `return` 문은 반환 값을 더 명확하게 표시하기 위한 경우를 제외하고 괄호를 사용하지 않아야 합니다.

```java
return;

return myDisk.size();

return (size ? size : defaultSize);
```

#### 7.4 if, if-else, if else-if 문

`if-else` 문은 다음과 같은 형식이어야 합니다.

```java
if (condition) {
    statements;
}

if (condition) {
    statements;
} else {
    statements;
}

if (condition) {
    statements;
} else if (condition) {
    statements;
} else {
    statements;
}
```

>참고 : `if` 문은 항상 중괄호 `{}`를 사용합니다. 오류가 발생하기 쉬운 다음과 같은 형식은 피하십시오.

```java
if (condition) //AVOID! THIS OMITS THE BRACES {}!
    statement;
```

#### 7.5 for 문

`for` 문은 다음과 같은 형식이어야 합니다.

```java
for (initialization; condition; update) {
    statements;
}
```

빈 `for` 문(모든 작업이 초기화, 조건 및 업데이트 절에서 수행되는 문)은 다음 형식이어야 합니다.

```java
for (initialization; condition; update);
```

`for` 문의 초기화 또는 업데이트 절에서 쉼표 연산자를 사용할 때는 복잡성을 피하기 위해 세 개 이상의 변수를 사용하지 말아야 하며, 필요한 경우 `for` 루프 앞 부분(초기화 절에서 사용하는 경우) 또는 루프 끝 부분(업데이트 절에서 사용하는 경우)을 분리하여 사용하십시오.

#### 7.6 while 문

`while` 문은 다음과 같은 형식이어야 합니다.

```java
while (condition) {
    statements;
}
```

빈 `while` 문은 다음 형식이어야 합니다.

```java
while (condition);
```

#### 7.7 do-while 문

`do-while` 문은 다음과 같은 형식이어야 합니다.

```java
do {
    statements;
} while (condition);
```

#### 7.8 switch 문

`switch` 문은 다음과 같은 형식이어야 합니다.

```java
switch (condition) {
case ABC:
    statements;
    /* falls through */
case DEF:
    statements;
    break;
case XYZ:
    statements;
    break;
default:
    statements;
    break;
}
```

case를 그냥 통과시켜야 할 경우(`break` 문을 사용하지 않았을 경우), 일반적으로 `break` 문이 있어야할 곳에 항상 주석을 추가 하십시오. 위 코드 예시에서는 `/* falls through */` 주석을 통해 이것을 보여주고 있습니다.

모든 `switch` 문은 default case를 추가하는 것이 좋습니다. defualt case에서 `break`는 생략할 수 있지만, 생략하지 않는다면 나중에 다른 case가 추가되어 발생하는 통과 오류(fall-through error)를 방지할 수 있습니다. 

#### 7.9 try-catch 문

`try-catch` 문은 다음과 같은 형식이어야 합니다.

```java
try {
    statements;
} catch (ExceptionClass e) {
     statements;
}
```

`try-catch` 문은 `finally`가 마지막에 붙을 수 있으며, `try` 블럭의 성공적으로 완료되었는지 여부와 상관없이 내용을 실행합니다.

```java
try {
    statements;
} catch (ExceptionClass e) {
    statements;
} finally {
    statements;
}
```

### 8 여백(White Space)

#### 8.1 빈 줄(Blank Lines)

빈 줄은 논리적으로 관련이 있는 코드 섹션들을 구별하여 가독성을 향상 시킵니다.

다음과 같은 상황에서는 항상 두 개의 빈 줄을 사용해야 합니다.

- 소스 파일의 섹션 사이
- 클래스 정의 그리고 인터페이스 정의 사이

다음과 같은 상황에서는 항상 한 개의 빈 줄을 사용해야 합니다.

- 메소드 사이
- 메소드의 로컬 변수와 첫 번째 명령문 사이
- 블록 ([5.1.1절 참조](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-141999.html#680)) 또는 한 줄 ([5.1.2 절 참조](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-141999.html#341)) 주석 전에
- 가독성을 높이기 위해 메소드 내부의 논리적 섹션 간

#### 8.2 공백(Blank spaces)

다음과 같은 상황에서는 공백을 사용해야합니다.

- 키워드 뒤에 괄호가 있으면 공백으로 구분해야합니다. 예를 들면 다음과 같습니다.

```java
        while (true) {
            ...
        }
```

>메소드 이름과 여는 괄호 사이에 공백을 사용해서는 안됩니다. 이렇게 키워드와 메소드 뒤에 괄호를 공백의 여부로 구별하면 키워드를 메소드 호출과 구별하는 데 도움이 됩니다.

- 인수 목록에서는 쉼표 뒤에 공백을 사용합니다.
- `.`를 제외한 모든 이항 연산자는 피연산자와 공백으로 구분해야합니다. 공백은 음수를 나타내는 단항 빼기(unary minus), 증가(`++`) 및 감소 (`--`)와 같은 단항 연산자를 피연산자와 분리해서는 안됩니다. 예를 들면 다음과 같습니다.

```java
    a += c + d;
    a = (a + b) / (c * d);

    while (d++ = s++) {
        n++;
    }
    printSize("size is " + foo + "\n");
```

- `for`문의 표현식은 공백으로 분리해야합니다. 예를 들면 다음과 같습니다.

```java
    for (expr1; expr2; expr3)
```

- 형변환 뒤에 공백을 사용합니다. 예를 들면 다음과 같습니다.

```java
    myMethod((byte) aNum, (Object) x);
    myMethod((int) (cp + 5), ((int) (i + 3)) + 1);
```

### 9 명명 규칙

명명 규칙은 프로그램을 보다 쉽게 읽을 수 있도록 하여 프로그램을 보다 이해하기 쉽게 만듭니다. 또한 코드의 이해에 도움이 될 수 있는 상수, 패키지 또는 클래스 등 식별자의 기능에 대한 정보를 제공 할 수도 있습니다.

| 식별자 종류 | 명명 규칙 | 예시 |
|---|---|---|
|패키지|고유 한 패키지 이름의 접두사는 항상 소문자 ASCII 문자로 작성되며 최상위 도메인 이름으로 현재 사용중인 com, edu, gov, mil, net, org 이거나 ISO 표준 3166, 1981에 명시된 영어 2문자로 된 국가 식별 코드 중 하나 여야합니다.<br/>패키지 이름의 후속 구성 요소는 조직 자체의 내부 명명 규칙에 따라 다릅니다. 이러한 규칙은 특정 디렉토리 이름 구성 요소를 부문, 부서, 프로젝트, 장비 또는 로그인 이름으로 지정할 수 있습니다.|com.sun.eng<br/>com.apple.quicktime.v2<br/>edu.cmu.cs.bovik.cheese|
|클래스|클래스 이름은 명사이어야 하며 각 내부 단어의 첫 글자는 대문자를 사용하는 mixed case를 사용해야 합니다. 클래스 이름을 단순하고 설명하기 쉽게 만드십시오. 완전한 단어를 사용하고 두문자어 및 약어 사용은 지양 하십시오 (약어가 URL 또는 HTML과 같은 긴 형식보다 훨씬 널리 사용되는 경우는 예외로 함).|class Raster;<br/>class ImageSprite;|
|인터페이스|인터페이스 명명 규칙은 클래스 명명 규칙과 동일 합니다.|interface RasterDelegate;<br/>interface Storing;|
|메소드|메소드는 첫 글자가 소문자인 동사이어야 하며 각 내부 단어의 첫 글자는 대문자를 사용하는 mixed case를 사용해야 합니다.|run();<br/>runFast();<br/>getBackground();|
|변수|변수들 중에서 모든 인스턴스, 클래스 및 클래스 상수를 제외하고 나머지 변수들은 첫 글자는 소문자를 사용하는 mixed case를 사용합니다. 내부 단어는 대문자로 시작합니다. 변수 이름은 밑줄 `_` 또는 달러 기호 `$` 문자로 시작해서는 안됩니다.<br/>변수 이름은 짧지만 의미가 있어야 합니다. 변수 이름을 선택할 때는 인지하기 쉬운 이름을 선택해야 합니다. 즉, 다른 사람에게 변수의 사용 의도를 나타낼 수 있도록 지어야 합니다. 임시로 잠깐 사용되는 변수를 제외하고 한 문자로 된 변수 이름은 사용하지 않아야 합니다. 임시 변수의 일반적인 이름은 정수의 경우 `i`, `j`, `k`, `m` 및 `n`을 사용하고, 문자의 경우 `c`, `d` 및 `e`를 사용합니다.|int i;<br/>char c;<br/>float myWidth;|
|상수|클래스 상수로 선언된 변수 이름과 ANSI 상수의 이름은 모두 대문자이어야 하며 단어의 구분자로 밑줄(`_`)을 사용해야 합니다.(ANSI 상수는 디버깅하기 어려우므로 사용을 지양 해야 합니다.)|static final int MIN_WIDTH = 4;<br/>static final int MAX_WIDTH = 999;<br/>static final int GET_THE_CPU = 1;|

### 10 프로그래밍 습관

#### 10.1 인스턴스 변수 및 클래스 변수 접근

정당한 이유없이 인스턴스 변수나 클래스 변수를 공개하지 마십시오. 대부분의 경우 인스턴스 변수들은 명시적으로 설정하거나 가져올 필요가 없습니다.(인스턴스 변수들을 명시적으로 설정하거나 가져오는 행위는 메소드를 호출할 때 부작용을 유발하기도 합니다.)

적절한 공개 인스턴스 변수의 예는 클래스가 전적으로 데이터 구조이며 어떠한 행위도 하지 않는 경우입니다. 다시 말해, 클래스 대신 구조체를 사용했다면((Java가 구조체를 지원하는 경우), 클래스의 인스턴스 변수를 공개하는 것이 적절합니다.

#### 10.2 클래스 변수 및 메소드 참조

객체를 사용하여 클래스 (정적) 변수 또는 메서드에 접근하지 마십시오. 대신 클래스 이름을 사용하십시오. 예를 들면 다음과 같습니다.

```java
classMethod();             //OK
AClass.classMethod();      //OK
anObject.classMethod();    //AVOID!
```

#### 10.3 상수

`for` 루프에서 카운터 값으로 나타날 수 있는 -1, 0 및 1을 제외하고 숫자 상수(고정된 값)는 직접 사용해서는 안됩니다.

#### 10.4 변수 할당

단일 문에서 동일한 값을 여러 변수에 지정하지 마십시오. 이는 가독성을 떨어뜨립니다. 예를 들면 다음과 같습니다.

```java
fooBar.fChar = barFoo.lchar = 'c'; // AVOID!
```

등식 연산자가 사용되는 곳에 할당 연산자를 사용하면 쉽게 혼동될 수 있으니 사용하지 마십시오. 예를 들면 다음과 같습니다.

```java
if (c++ = d++) {        // AVOID! (Java disallows)
    ...
}
```

위의 경우 다음과 같이 작성해야 합니다.

```java
if ((c++ = d++) != 0) {
    ...
}
```

런타임 성능을 향상시키기 위해 내부 할당을 사용하지 마십시오. 이것은 컴파일러의 일입니다. 예를 들면 다음과 같습니다.

```java
d = (a = b + c) + r;        // AVOID!
```

위의 경우 다음과 같이 작성해야 합니다.

```java
a = b + c;
d = a + r;
```

#### 10.5 기타 습관

##### 10.5.1 괄호

여러 연산자가 포함 된 표현식에서 연산자 우선 순위 문제를 피하기 위해 괄호를 자유롭게 사용하는 것이 좋습니다. 연산자 우선 순위가 명확 해 보일지라도 다른 사람에게는 그렇지 않을 수 있습니다. 다른 프로그래머가 우선 순위를 알고 있다고 생각해서는 안됩니다.

```java
if (a == b && c == d)     // AVOID!
if ((a == b) && (c == d)) // RIGHT
```

##### 10.5.2 반환 값

프로그램 구조와 의도를 일치 시키십시오. 예를 들면 다음과 같습니다.

```java
if (booleanExpression) {
    return true;
} else {
    return false;
}
```

위의 경우 다음과 같이 작성해야 합니다.

```java
return booleanExpression;
```

위와 유사한 예는 다음과 같습니다.

```java
if (condition) {
    return x;
}
return y;
```

위의 경우 다음과 같이 작성해야 합니다.

```java
return (condition ? x : y);
```

위의 경우 다음과 같이 작성해야 합니다.

##### 10.5.3 조건부 연산기호에서 `?` 앞의 표현식

삼항 연산자 `?:`의 `?` 앞에 있는 이항 연산자를 포함하는 표현식은 괄호로 묶어야 합니다. 예를 들면 다음과 같습니다.

```java
(x >= 0) ? x : -x;
```
##### 10.5.4 특별한 주석

제대로 만들어 지지 않았지만 작동하는 코드의 경우 주석에 `XXX` 플래그를 사용하십시오. 제대로 만들어 지지 않았고 작동하지 않는 코드의 경우 주석에 `FIXME` 플래그를 사용하십시오.

### 11 코드 예시

#### 11.1 Java 소스 파일 예시

다음 예제는 단일 공개 클래스(public class)를 포함하는 Java 소스 파일 작성 방법을 보여줍니다. 인터페이스의 형식도 이와 비슷합니다. 자세한 내용은 [4 페이지의 "Class 및 Interface 선언"](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-141855.html#1852)[^5] 및 [9 페이지의 "문서 주석"](https://www.oracle.com/technetwork/java/javase/documentation/codeconventions-141999.html#16838)[^6]을 참조하십시오.

```java
/*
 * @(#)Blah.java        1.82 99/03/18
 *
 * Copyright (c) 1994-1999 Sun Microsystems, Inc.
 * 901 San Antonio Road, Palo Alto, California, 94303, U.S.A.
 * All rights reserved.
 *
 * This software is the confidential and proprietary information of Sun
 * Microsystems, Inc. ("Confidential Information").  You shall not
 * disclose such Confidential Information and shall use it only in
 * accordance with the terms of the license agreement you entered into
 * with Sun.
 */


package java.blah;

import java.blah.blahdy.BlahBlah;

/**
 * Class description goes here.
 *
 * @version        1.82 18 Mar 1999
 * @author         Firstname Lastname
 */
public class Blah extends SomeClass {
    /* A class implementation comment can go here. */

    /** classVar1 documentation comment */
    public static int classVar1;

    /** 
     * classVar2 documentation comment that happens to be
     * more than one line long      */
    private static Object classVar2;

    /** instanceVar1 documentation comment */
    public Object instanceVar1;

    /** instanceVar2 documentation comment */
    protected int instanceVar2;

    /** instanceVar3 documentation comment */
    private Object[] instanceVar3;

    /** 
     * ...constructor Blah documentation comment...    */
    public Blah() {
        // ...implementation goes here...
    }

    /**
     * ...method doSomething documentation comment...   */
    public void doSomething() {
        // ...implementation goes here...
    }

    /**
     * ...method doSomethingElse documentation comment...
     * @param someParam description
     */
    public void doSomethingElse(Object someParam) {
        // ...implementation goes here...
    }
}
```

Copyright &copy; 1995-1999, Sun Microsystems, Inc. All rights reserved.[^9]

[^1]: 원문의 링크가 더이상 유효하지 않아 제거 하였다.
[^2]: 원문의 링크가 더이상 유효하지 않아 제거 하였다.
[^3]: 페이지는 PDF 버전의 페이지를 나타태며, 목차로는 `11.1 Java 소스 파일 예시` 이다.
[^4]: 페이지는 PDF 버전의 페이지를 나타내며, 목차로는 `3.1.1 시작 주석` 이다.
[^5]: 페이지는 PDF 버전의 페이지를 나타내며, 목차로는 `3.1.3 Class 와 Interface 선언` 이다.
[^6]: 페이지는 PDF 버전의 페이지를 나타내며, 목차로는 `5.2 문서 주석` 이다.
[^7]: [indent(1)](http://man7.org/linux/man-pages/man1/indent.1.html)은 Linux 명령어 이다. 
[^8]: 원문 링크가 [Javadoc Tool](https://www.oracle.com/technetwork/java/javase/tech/index-jsp-135444.html)이 아닌 자기 자신을 가리키고 있다.
[^9]: 원문의 Copyright 링크가 더이상 유효하지 않아 제거 하였다.