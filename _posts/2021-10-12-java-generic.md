---
layout: post
title: JAVA 자바 Generic & WildCard 제네릭 프로그래밍, 와일드카드 정리
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
- Generic Programming
  - Old Style
  - New Style (Generic)
  - Bounded Type Parameters
  - Restrictions for generic
  - Generic Method
  - Bounded Type Parameters 2
- Wild Card
  - UnBouned
  - Upper Bounded
  - Lower Bounded
- Generic vs Wild Card


## Generic Programing
---

Generic 제네릭 프로그래밍이랑?  
여러 타입들이 들어오는 것을 허용함으로써 개발자여로 하여금 코드를 재사용 가능하게 하는 것.

### Old Style
자바에서 generic이 생기기 전에는 *polymorphism*을 사용하였다.

Object 객체는 모든 클래스의 상위 클래스이므로 Object 레퍼런스가 다른 타입들을 참조하고 있는 식으로 generic programming을 구현하였다고 한다.

예를 들면 ArrayList<>가 있다.

`ArrayList.add(Object o)`는 Object를 매개변수로 받기 때문에 어떠한 타입이라도 받아드릴 수 있는 것이다.
```java
ArrayList fileList = new ArrayList();
fileList.add(new File("...")); // File도 객체이므로 Object를 상속할 것이다.
```
 
그렇다면 이러한 Object의 polymorphism을 활용한 `ArrayList`안에는 어떻게 구현되어 있을까?

```java
public class ArrayList {
  public Object get(int i) {…}
  public void add(Object o) {…}
  …
  private Object[] elementData ; 
}

ArrayList filenames = new ArrayList() ; 
filenames.add(new String(“a.txt”)) ; 

String filename = (String) filenames.get(0) ;
filenames.add(new File(“…”)) ;
```
와 같이 내부 맴버 변수와 메소드의 반환형을 Object로 셋팅해주었다.

그렇다면 이러한 방식의 문제점은?
1. 위 코드와 같이 Object 타임으로 반환되기에 항상 casting이 필요하다
2. 다형성으로 구현되었기에 다른 타입이 들어가도 컴파일러단에서 잡아내지 못한다.
   - ex) 위 filenames에 String 객체가 들어간다면? -> 에러로 잡아내지 못함

이러한 문제들 때문에 자바 5(2004년)부터 Generic Class가 나오게 되었다.

### Generic 제네릭 클래스를 이용한 제네릭 프로그래밍

제네릭 클래스는 C++의 template의 개념과 상당히 유사하다.

프로그램의 가독성을 더 좋게 해주고 안전하게 만들어 준다.

다시 ArrayList를 살펴보자
```java
public class ArrayList <T> {
   public T get(int i) {…}
   public void add(T o) {…}
   private T[] elementData; 
   // Object 대신 제네릭 클래스 T로 받는다
}

ArrayList<String> filenames = new ArrayList<>();

filenames.add(new String(“a.txt”)) ; 

String filename = filenames.get(0) ; // 캐스팅이 필요없다! Object가 아니기 때문

filenames.add(new File(“…”)) ; // ERROR!! filenames는 String타입의 리스트
```

Generic 클래스를 이용한 또 다른 예제를 살펴보자

```java
class Pair<T> {
   private T first, second; 

   public Pair(T first, T second) { 
     this.first = first;  
     this.second = second; 
   }
   public T getFirst() { return first; }
   public T getSecond() { return second; }
   public void setFirst(T newValue) { first = newValue; }
   public void setSecond(T newValue) { second = newValue; }
} 
```

여러가지 타입을 받을 수 있는, (제네릭한)  
같은 타입 2개를 받아 여러가지 메소드를 제공하는 클래스 Pair<T>를 생각해보자.

```java
Pair<String> strPair = new Pair<String>() ; 

strPair.setFirst("Name") ; 
strPair.setSecond("Value"); 

System.out.println( strPair.getFirst() + " " + strPair.getSecond()) ; 

Pair<Rectangle> recPair = new Pair<Rectangle>() ; 

recPair.setFirst(new Rectangle(0, 0, 10, 10)) ; 
recPair.setSecond(new Rectangle(0, 0, 100, 100)); 

System.out.println( recPair.getFirst() + " " + recPair.getSecond()) ;
```

위 코드와 같이 `String`이던 `Rectangle`이던 어떠한 타입이 와도 처리가 가능한 Generic한 프로그래밍을 구현가능하다.

### Bounded Type Parameters 제한된 타입 매개변수 받기

자바의 제네릭 클래스에서 임의의 인자 <T>를 받아올 때에 제한을 둘 수 있다.

예를 들면 모든 클래스가 아닌 `Number`와 `Serializable`를 상속 받는 <T>클래스로만 제한하여 받아드릴 수 있다는 것이다.

```java
class Pair<T extends Number & Serializable> {
   private T first, second; 

   public Pair(T first, T second) { 
     this.first = first;  
     this.second = second; 
   }
   public T getFirst() { return first; }
   public T getSecond() { return second; }
   public void setFirst(T newValue) { first = newValue; }
   public void setSecond(T newValue) { second = newValue; }
}
```
좀 전에 예시로 든 `Pair<T>`클래스를 위와 같이 제한시켜보자.

```java
Pair<Integer> intPair = new Pair<Integer>() ;
intPair.setFirst(1) ; 
intPair.setSecond(100); 
System.out.println( intPair.getFirst() + " " + intPair.getSecond()) ;

Pair<Float> floatPair = new Pair<Float>() ; 
floatPair.setFirst(1.1F) ; 
floatPair.setSecond(100.1F); 
System.out.println( floatPair.getFirst() + " " + floatPair.getSecond()) ;

Pair<String> strPair = newPair<String> ; 
// ERROR!! String 클래스는 Number을 상속받지 않음
```

위와 같이 Number을 상속 받지 않는 String 클래스를 집어 넣을 경우 컴파일 단에서 에러를 발생시킴을 알 수 있다.

### Restrictions 제네릭 사용 시 제약사항

- 제네릭 타입으로 Primitive type은 받을 수 없다!
```java
Pair<int, char> p = new Pair<>(8, 'a');  // ERROR!!
Pair<Integer, Character> p = new Pair<>(8,'a); // OK
```
  
- 제네릭 타입으로 객체를 생성할 수 없다!
```java
public static <E> void append(List<E> list) {
  E elem = new E();  // ERROR!!
}
```

- 제네릭 타입에 형변환 Cast나 instanceof 연산자를 사용할 수 없다!
```java
public static <E> void rtti(List<E> list) {
  if (list instanceof ArrayList<Integer>)  // ERROR!!

  List<Integer> li = new ArrayList<>(); 
  List<Number>  ln = (List<Number>) li;  // ERROR!!
}
```

- 제네릭 타입을 static 필드로 선언할 수 없다!
```java
class Pair<T> {
  static T first; //ERROR!!
  static Pair<T> minmax (T[] a) { }  //ERROR!!
}
```

- 제네릭 타입을 배열로 선언할 수 없다!
```java
class Pair<T> {
  T[] toArray() {
    T[] tmpArr = new T[items.length];  //ERROR
    return tmpArr;
  } 
}
```

### Generic Method 제네릭 메소드

제네릭 타입은 클래스를 정의할 때 뿐만 아니라 기존 클래스의 메소드에도 사용이 가능하다.

변수명 앞에 <T>와 같이 제네릭임을 명시해주고 제네릭 타입을 메소드에서 사용가능하다.

```java
class ArrayAlg {
  public static <T> T getMiddle(T[] a) {
    return a[a.length/2] ; 
  }
}
```

타입 매개변수 <T>는 반드시 수식자(public, static 등)과 반환형 사이에 위치해야한다.

```java
String [] names = {“John”, “Q”, “Public”} ;

String middle1 = ArrayAlg.<String>getMiddle(names) ; //OK!
String middle2 = ArrayAlg.getMiddle(names) ; //OK!
```

제네릭 메소드를 호출할 때에는 실제 타입을 꺾쇠 안에 넣어준다.

꺾쇠는 컴파일러가 추측해줄꺼라 믿고 생략도 가능하다.

### Bounded Type Parameters 제한된 타입 매개변수 받기 2

제네릭 메소드에서도 물론 당연히 타입 매개변수를 제한할 수 있다.

`Pair` 에서 minmax를 알기 위해 오직 String만으로 제한해보자.
```java
public static Pair<String> minmax(String[] a) {...}
```
위와 같이 제네릭 하지 않고 오직 String 객체만 받도록 제한할 수 있다.

하지만 이렇게 제한 해버리면 generic한 이유가 없다...

아래 예제를 다시 보자.

```java
public static <T extends Comparable<T>> Pair<T> minmax (T[] a)  {
  T min = a[0], max = a[0]; 

  for (int i = 1; i < a.length; i++) {
    if (min.compareTo(a[i]) > 0) min = a[i];
    if (max.compareTo(a[i]) < 0) max = a[i];
  } 
  return new Pair<T>(min, max);
}
```
타입 매개변수 <T>를 비교 가능한 Comparable 객체를 상속 받는 객체로만 제한 하였다.

이렇게 한다면 compareTo() 함수는 항상 보장받게 되어 generic하면서도 안정적인 메소드를 설계하였다.

## Wild Card 와일드카드 (UnBounded)
---

와일드 카드란 제네릭을 사용하는 코드에서 타입 매개변수를 **?** 로 표현하며, 어떠한 타입이던지 나타낼 수 있다.

```java
public static void foo(List<?> list) {...};
```

와일드 카드는 매개변수, 필드, 지역변수의 타입을 나타내는 등으로 사용된다.

#### Upper Bounded 상한이 있는 와일드 카드

마찬가지로 `<? extends Class>`와 같이 제한을 걸 수 있다.

예를 들면
```java
public static void foo(List<? extends Number> list) {...};
```

와 같이 사용한다면 Number클래스와 이를 상속받는 어떠한 클래스도 ? 부분에 올 수 있다는 뜻이다.

#### Lower Bounded 하한이 있는 와일드 카드

반대로 `<? super Class>` 와 같이 쓴다면

Class를 포함하여 자식 클래스로 두는 모든 클래스가 ? 자리에 올 수 있다.


#### 유의사항

와일드 카드에서`List<?>`와 `List<Object>`와 구분할 필요가 있다.

Object를 사용할 경우 `List<Interger>`, `List<String>` 같은 객체는 오지 못한다.

Object이 String의 super이지, 
`List<Object>`가 `List<String>`의 super가 아니기 때문.

### Generic vs WildCard

제네릭으로 구현된 메소드의 경우 선언된 타입으로만 매개변수를 입력해야한다.

이를 상속 받은 클래스나 부모 클래스를 사용하고 싶어도 불가능하다.

와일드 카드의 경우 그 어떤 타입이 와도 대응 가능하기에 조금 더 유연하다고 볼 수 있다.

사실 나도 포스팅하면서도 헷갈리는데 이번 기회에 확실히 구분해두자.