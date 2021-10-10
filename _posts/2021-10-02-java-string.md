---
layout: post
title: 자바 String 문자열 클래스 정리
comments: true
categories: [Java]

# Insight
# Project
# Retrospect
# PS
# LogicDesign
# Contest
# DataStructure
# Java

---


>목차
- Spring
  - Methods
  - Conversion
  - Formatting


## String 문자열 정리
---
**String** 클래스는 자바에서 **문자열**을 다루기 위한 자료형이다.

```java
String greeting = "Hello" ;
```

### Methods

- **length()** : 문자열의 길이 반환
```java
String greeting = "Hello" ;
int strLength = greeting.length();  // 5
```
- **charAt(idx)** : idx번째 인덱스의 문자 리턴
```java
String greeting = "Hello" ;
char strChar = greeting.charAt(1) // e
```
- **substring(begin, end)** : begin 부터 end-1 까지의 문자열 리턴
```java
String greeting = "Hello" ;
String hel = greeting.substring(1, 4) ; // "ell"
```
- **+** : Concatentation 문자열 연결
```java
String greeting = "Hello", language = "Java !" ;
String msg = greeting + " " + language ; // "Hello Java !"
```
- **equals(str)** : str 문자열과 비교 / ***비교연산자 ==을 사용할 수 없다!!**
```java
String greeting = "Hello"
greeting.equals("Hello") // true;
```
- **equalsIgnoreCase(str)** : str 문자열과 대소문자 구분없이 비교 
```java
String greeting = "Hello"
greeting.equals("hello") // true;
```
- **compareTo(str)** : str 문자열과 우선 순위 비교
```java
String greeting = "Hello"
if ( greeting.compareTo(str) < 0 ) // greeting comes before str
else if ( greeting.compareTo(str) > 0 ) // greeting comes after str
else // equal
```
- **replace(str1 , str2)** : 문자열에서 str1을 str2로 모두 바꾼다.
```java
String greeting = "Hello"
String greeting2 = greeting.replace('l', 'L') ; // HeLLo;
```
- **indexOf(str or char)** : 인자 str 또는 char가 문자열 내에서 처음 시작되는 인덱스를 리턴
```java
String greeting = "Hello"
greeting.indexOf('l') ; // 2
greeting.indexOf("lo") ; // 3
greeting.indexOf("L") ; // -1
```
- **lastIndexOf(str or char)** : 인자 str 또는 char가 문자열 내에서 마지막 시작되는 인덱스를 리턴
```java
String greeting = "Hello"
greeting.indexOf('l') ; // 2
greeting.lastIndexOf('l') ; // 3
```
- **startWith(str)**, **endWith(str)** : 문자열이 str로 시작하는지, 끝나는지 참거짓 리턴
```java
String greeting = "Hello"
greeting.startsWith("He"); // true
greeting.startsWith("he"); // false
greeting.endsWith("lo")  ; // true
greeting.startsWith("LO"); // false
```
- **split(regex)** : 문자열을 regex 기준으로 쪼개서 배열로 리턴
```java
String line = "first : second : third"; 
String[] items1 = line.split(":");  //["first ", " second ", " third"]
String[] items2 = line.split("\\s*:\\s*"); //["first", "second", "third"]
```
- **join(str1, str2...)** : str1기준으로 뒤에 모든 문자열 인자들을 연결하여 리턴
```java
String.join("-", "I", "Love", "Java") // I-Love-Java
```

### Conversion between Number 숫자와 형변환
- **String to Number**

`Number.valueOf(str)`을 사용한다.  `valueOf()` 메소드는 Wrapper object 를 반환해준다. 또는 `Number.parseNum(str)` 사용.

```java
int a = Integer.parseInt(intString) ;
float b = Float.parseFloat(floatString) ;

a = Integer.valueOf(intString); // auto unboxing
b = Float.valueOf(floatString); // auto unboxing
```
*참고로 valueOf()가 메모리 공간과 수행 시간 모두 더 나은 퍼포먼스를 보인다고 한다.*

- **Number to String**

`Number.toString()` 함수 사용. primitive type일 경우 Wrapper 클래스로 바꿔준다.

```java
Integer intValue = 100 ;
float f = 1.234F ;
String strI = intValue.toString() ; // "100"
String strF = Float.valueOf(f).toString() ; // "1.234"
```

### Formattind String
`String.format(format, string)`를 사용하여 문자열을 원하는대로 format할 수 있다.
```java
String.format("%d", 101);         // 101
String.format("|%8d|", 101);      // |     101|
String.format("|%-8s|", "Hello"); // |Hello   |
String.format("|%08f|", 101.00);  // |00101.000|
String.format("|%8.2f|", 101.00); // |   101.00|
String.format("%x", 101);         // 65 (hex)
```
