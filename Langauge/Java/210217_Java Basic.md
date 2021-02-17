- [1. JAVA 기본 개념](#1-java-기본-개념)
- [2. 문법 - Syntax](#2-문법---syntax)
  - [2.1. Number](#21-number)
  - [2.2. String](#22-string)
  - [2.3. 변수](#23-변수)
    - [2.3.1. Number](#231-number)
    - [2.3.2. String](#232-string)
  - [2.4. Comment](#24-comment)
  - [2.5. Data Type](#25-data-type)

-------------

<br>

# 1. JAVA 기본 개념

Java는 원래 가전제품을 제어하기 위한 언어로 고안되었지만 웹의 등장으로 엄청난 성공을 거두면서 주류 언어가 되었습니다.
한국에서는 정부/기업의 시스템 통합 프로젝트가 대부분 자바로 구현되기 때문에 자바는 기업용 시장에서 두각을 나타내고있습니다.

# 2. 문법 - Syntax

## 2.1. `Number`

``` java
  System.out.printIn(1 + 2)
  // result: 3
  
  System.out.printIn(1.2 + 1.3)
  // result: 2.5
```

## 2.2. `String`

JAVA는 문자(`Character`)와 문자열(`String`)을 구분한다. <br>
문자는 한 글자를 의#미하고, 문자열은 여러 개의 문자가 결합한 것을 의미한다.<br>
자바에서 문자는 ''(작은 따옴표)로 감싸고, 문자 열은 ""(큰 따옴표) 로 감싸야 한다. 문자 열을 '' 로 감싸면 에러 발생

``` java
  System.out.printIn('생')
  
  System.out.printIn("생활코딩")
  
  // 여러 줄의 표시
  System.out.printIn("HTML \n CSS \n JS \n")
  
  System.out.printIn("생활" + "코딩")
```

## 2.3. Variable 변수

`데이터 형식` 과 `변수의 이름` 으로 구성됩니다.

### 2.3.1. Number
``` java
  int a;
  a = 1; // 정수
  System.out.printIn(a + 1); // 2 
  
  a = 2;
  System.out.printIn(a + 1); // 3
```
``` java
  double a = 1.1; // 실수
  System.out.printIn(a + 1.1) // 2.2
  
  a = 2.1;
  System.out.printIn(a + 1.1) // 3.2
```

### 2.3.2. String
``` java
  String a, b;
  a = "coding";
  b = " everybody";
  
  System.out.printIn(a + b)
```

## 2.4. Comment
``` java
  // 한줄 주석
  /*
    여러줄 주석
  */
  /**
  * JavaDoc 주석: 자바의 문서를 만들 때 사용합니다.
  */
```

## 2.5. Data Type

Java의 데이터 타입은 JS와 다르게 정말로 데이터 타입(`byte`, `short`, `int`, `long`)를 의미한다.
