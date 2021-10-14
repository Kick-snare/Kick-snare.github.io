---
layout: post
title: JAVA 자바 Date & Time 날짜,시간 정리
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
- Date & Time
  - Simple date format
  - Sleep
  - Measing Elapsed Time

## Date & Time
---
### 날짜와 시간 받기

자바에서 날짜와 시간을 불러오기 위해서는 Date 객체를 사용한다.

Date 클래스는 `import java.util.Date`로 불러올 수 있다.

```java
final Date date = new Date();
System.out.println(date.toString()); 
```
```
> Tue Oct 10 05:06:38 KST 2021
```

### SimpleDateFormat

`java.text.SimpleDateFormat` 클래스로 Date 클래스를 format 할 수 있다.

```java
final Date now = new Date( );
final SimpleDateFormat format =
  new SimpleDateFormat ("E yyyy.MM.dd 'at' hh:mm:ss a zzz");

System.out.println("Current Date: " + format.format(now));
```
```
> Current Date: 화 2021.10.05 at 05:06:38 오후 KST
```

### Sleep

`Threas.sleep()` 메소드로 Exception을 발생시켜 프로그램을 일정 시간동안 멈출 수 있다.
```java
try {
    System.out.println(new Date( ));
    Thread.sleep(3 * 1000); // throws InterruptedException 
    System.out.println(new Date( ));
    
} catch (Exception e) {
    System.out.println("Got an exception!"); 
}
System.out.println("end");
```
```
> Tue Oct 10 08:00:00 KST 2021
> Tue Oct 10 08:00:03 KST 2021
> end
```

### Measuring Elapsed Time 수행시간 확인

`System.currentTimeMills()` 함수로 밀리초 단위로 수행 당시 시간을 저장한 뒤 차이를 비교하여 프로그램의 수행 속도를 측정할 수 있다.

```java
try {
    final long start = System.currentTimeMillis(); // 1970. 1. 1. 과 현재와의 차이 
    System.out.println(new Date( ));

    Thread.sleep(3 * 1000); 
    System.out.println(new Date( ));

    final long end = System.currentTimeMillis();
    System.out.println("Difference is : " + (end - start)); 

} catch (Exception e) {
    System.out.println("Got an exception!"); 
}
```
```
> Tue Oct 10 08:00:00 KST 2021
> Tue Oct 10 08:00:03 KST 2021
> Difference is : 3025
```