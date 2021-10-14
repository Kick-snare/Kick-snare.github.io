---
layout: post
title: JAVA 자바 Reflection 리플렉션 활용 예제
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
- Reflection

## Reflection 리플렉션이란?
---
Reflection이란, JVM에서 실행되는 어플리케이션의 런타임 동작을 검사하거나 수정할 수 있는 기술이다.

byte code상의 클래스 정보를 분석하여 활용할 수 있다.

`import java.lang.reflect`로 임포트하여 사용한다.

주로 코드상의 **클래스**를 찾아 생성할 때 많이 사용한다.

이렇게 사용되는 reflection의 사용 예제를 살펴보자.  
Student가 Person을 상속받는 구조를 생각해보아라.
```java
Scanner scanner = new Scanner(System.in);
System.out.print("Enter class name (e.g. java.util.Date): ");
name = scanner.next();
scanner.close(); 
```
먼저 찾고 싶은 클래스의 이름은 표준입력으로 입력받아 `name`에 저장한다.  
**Student**을 입력했다고 치자.

```java
inal Class<?> cl = Class.forName(name); // java.lang.Class
final Class<?> supercl = cl.getSuperclass(); // cl의 부모클래스

System.out.print("class " + name); // class Student

if (supercl != null && supercl != Object.class)
    System.out.print(" extends " + supercl.getName()); // extends Person

printConstructors(cl); // 생성자 출력

printMethods(cl); // 메소드 출력
```

#### printConstructor()
```java
public static void printConstructors(final Class<?> cl) {
  // java.lang.reflect.Constructor
  final Constructor<?>[] constructors = cl.getDeclaredConstructors();
  for (final Constructor<?> constructor : constructors) {

    System.out.print("   " + Modifier.toString(constructor.getModifiers()));
    System.out.print(" " + constructor.getName() + "(");

    final Class<?>[] parameterTypes = constructor.getParameterTypes(); 

    for (int j = 0; j < parameterTypes.length; j++) {
      if ( j > 0) System.out.print(", ");
      System.out.print(parameterTypes[j].getName()); 
    } 
    System.out.println(") { }");
  } 
} // 생성자를 출력
```

#### printMethod()
```java
public static void printMethods(final Class<?> cl) {
  final Method[] methods = cl.getDeclaredMethods();

  for (final Method method : methods) {
    final Class<?> returnType = method.getReturnType();

    // print modifiers, return type and method name 
    System.out.print("   " + Modifier.toString(method.getModifiers())); 
    System.out.print(" " + returnType.getName() + " " + method.getName() + "(");

    // print parameter types 
    final Class<?>[] parameterTypes = method.getParameterTypes(); 
    for (int j = 0; j < parameterTypes.length; j++) {
      if ( j > 0) System.out.print(", ");
      System.out.print(parameterTypes[j].getName());
    } 
    System.out.println(") { }");
  } 
}
// 모든 메소드들을 출력
```

위 두 함수와 같이 객체를 통해 클래스의 정보를 분석해낼 수 있음을 확인할 수 있다.

또한 동적으로 인스턴스를 Reflection을 통해 생성할 수 있다.